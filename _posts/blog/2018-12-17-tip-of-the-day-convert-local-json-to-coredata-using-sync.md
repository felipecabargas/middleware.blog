---
author: juanpintoduran
title: '[Daily Tip] Convert Local JSON to CoreData using Sync'
excerpt:
layout: post
category:
  - Tips
tags:
  - swift
  - development
post_format: [ ]
---

[Sync](https://github.com/3lvis/Sync) is a Swift library that uses a convention-over-configuration paradigm to facilitate JSON-2-CoreData operations.

Sync uses a wrapper for CoreData called DataStack which allows us to skip dealing with NSPersistentStoreCoordinator and NSManageObjectContext.

First, we need to create a custom Fetcher class to fetch data from our JSON file and populate the DB. 

```swift
import CoreData
import Sync

class Fetcher {
    private let dataStack: DataStack
    
    init() {
        self.dataStack = DataStack(modelName: "ENTITY")
    }
}
```

Moving forward, replace all instances of _`ENTITY`_ with the name of your entity class.

Now, let’s create a `fetchLocalEntities()` function that processes the NSFetchRequest and sorts our info by a given _`KEY`_

```swift
    func fetchLocalEntities() -> [ENTITY] {
        let request: NSFetchRequest<ENTITY> = ENTITY.fetchRequest()
        let sortDescriptor = NSSortDescriptor(key: "KEY", ascending: true)
        let sortDescriptors = [sortDescriptor]
        request.sortDescriptors = sortDescriptors

        return try! self.dataStack.viewContext.fetch(request)
    }
```

Now the fun part. Let’s add a `syncUsingLocalJSON()` function that parses our JSON file. The code goes as follows:

```swift    
    func syncUsingLocalJSON(completion: @escaping (_ result: VoidResult) -> ()) {
        let fileName = "JSON-FILE"
        guard let url = URL(string: fileName) else { return }
        guard let filePath = Bundle.main.path(forResource: url.deletingPathExtension().absoluteString, ofType: url.pathExtension) else { return }
        guard let data = try? Data(contentsOf: URL(fileURLWithPath: filePath)) else { return }
        guard let json = try! JSONSerialization.jsonObject(with: data, options: []) as? [[String: Any]] else { return }
        print("Syncing")
        self.dataStack.sync(json, inEntityNamed: EntityClass.entity().name!) { error in
            completion(.success)
        }
    }
```

Remember to replace _`JSON-FILE`_ with the name of your `.json` file.

Lastly, add an enumerator that returns the correct case for our functions.

``` swift
enum VoidResult {
    case success
    case failure(NSError)
}
```