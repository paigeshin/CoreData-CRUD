# CoreData-CRUD

# Copy & Paste Core Data Code in AppDelegate

```swift
// MARK: - Core Data stack

lazy var persistentContainer: NSPersistentContainer = {
    /*
     The persistent container for the application. This implementation
     creates and returns a container, having loaded the store for the
     application to it. This property is optional since there are legitimate
     error conditions that could cause the creation of the store to fail.
    */
    let container = NSPersistentContainer(name: "ToDoListApp")
    container.loadPersistentStores(completionHandler: { (storeDescription, error) in
        if let error = error as NSError? {
            // Replace this implementation with code to handle the error appropriately.
            // fatalError() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
             
            /*
             Typical reasons for an error here include:
             * The parent directory does not exist, cannot be created, or disallows writing.
             * The persistent store is not accessible, due to permissions or data protection when the device is locked.
             * The device is out of space.
             * The store could not be migrated to the current model version.
             Check the error message to determine what the actual problem was.
             */
            fatalError("Unresolved error \(error), \(error.userInfo)")
        }
    })
    return container
}()

// MARK: - Core Data Saving support

func saveContext () {
    let context = persistentContainer.viewContext
    if context.hasChanges {
        do {
            try context.save()
        } catch {
            // Replace this implementation with code to handle the error appropriately.
            // fatalError() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
            let nserror = error as NSError
            fatalError("Unresolved error \(nserror), \(nserror.userInfo)")
        }
    }
}
```

# Save

```swift
// MARK: SAVE
let context = (UIApplication.shared.delegate as! AppDelegate).persistentContainer.viewContext
let toDoItem = ToDoItem(context: context)
toDoItem.name = taskName
toDoItem.details = taskDetails
toDoItem.isComplete = false
toDoItem.startDate = Date()
(UIApplication.shared.delegate as! AppDelegate).saveContext()
```

# Read

```swift
var toDoItems: [ToDoItem]  {   
    do {
        let context = (UIApplication.shared.delegate as! AppDelegate).persistentContainer.viewContext
        return try context.fetch(ToDoItem.fetchRequest())
    } catch {
        print("Couldn't fetch data")
    }
    return []
}
```

# Delete

```swift
// MARK: DELETE
let context = (UIApplication.shared.delegate as! AppDelegate).persistentContainer.viewContext
context.delete(toDoItem)
(UIApplication.shared.delegate as! AppDelegate).saveContext()
```

# Update

```swift
// MARK: UPDATE
toDoItem.isComplete = true
(UIApplication.shared.delegate as! AppDelegate).saveContext()
```
