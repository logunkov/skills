# Swift Core Data

### Data Base
```swift
// MARK: - Work with Data Base
extension ViewController {
    // Fetch data
    private func fetchData() {
        let fetchRequest: NSFetchRequest<Task> = Task.fetchRequest() // Запрос выборки по ключу Task
        
        do {
            tasks = try managedContext.fetch(fetchRequest) // Заполнение массива данными из базы
        } catch let error {
            print("Failed to fetch data", error)
        }
    }
    
    // Save data
    private func saveTask(_ taskName: String) {
        guard let entity = NSEntityDescription.entity(
            forEntityName: "Task",
            in: managedContext
            ) else { return } // Create entity
        
        let task = NSManagedObject(entity: entity,
                                   insertInto: managedContext) as! Task // Task instace
        task.name = taskName // New value for task name
        
        do {
            try managedContext.save()
            tasks.append(task)
            tableView.insertRows(
                at: [IndexPath(row: tasks.count - 1, section: 0)],
                with: .automatic
            )
        } catch let error {
            print("Failed to save task", error.localizedDescription)
        }
    }
    
    // Edit data
    private func editTask(_ task: Task, newName: String) {
        do {
            task.name = newName
            try managedContext.save()
        } catch let error {
            print("Failed to save task", error)
        }
    }
    
    // Delete data
    private func deleteTask(_ task: Task, indexPath: IndexPath) {
        
        managedContext.delete(task)
        
        do {
            try managedContext.save()
            tasks.remove(at: indexPath.row)
            tableView.deleteRows(at: [indexPath], with: .automatic)
        } catch let error {
            print("Error: \(error)")
        }
    }
}
```

### AppDelegate
```swift
import UIKit
import CoreData
@UIApplicationMain

class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        window = UIWindow(frame: UIScreen.main.bounds)
        window?.makeKeyAndVisible()
        window?.rootViewController = UINavigationController(rootViewController: ViewController())
        return true
    }

    func applicationWillTerminate(_ application: UIApplication) {
        self.saveContext()
    }

    // MARK: - Core Data stack
    lazy var persistentContainer: NSPersistentContainer = {
        let container = NSPersistentContainer(name: "CoreDataDemo")
        container.loadPersistentStores(completionHandler: { (storeDescription, error) in
            if let error = error as NSError? {
                fatalError("Unresolved error \(error), \(error.userInfo)")
            }
        })
        return container
    }()

    // MARK: - Core Data Saving support
    func saveContext() {
        let context = persistentContainer.viewContext
        if context.hasChanges {
            do {
                try context.save()
            } catch {
                let nserror = error as NSError
                fatalError("Unresolved error \(nserror), \(nserror.userInfo)")
            }
        }
    }
}
```

### ViewController
```swift
import UIKit
import CoreData

class ViewController: UITableViewController {
    private let cellID = "cell"
    private var tasks: [Task] = []
    private let managedContext = (
        UIApplication.shared.delegate as! AppDelegate
        )
        .persistentContainer.viewContext

    override func viewDidLoad() {
        super.viewDidLoad()
        setupView()
        
        // Table view cell register
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: cellID)
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        fetchData()
    }

    /// Setup view
    private func setupView() {
        view.backgroundColor = .white
        setupNavigationBar()
    }
    
    /// Setup navigation bar
    private func setupNavigationBar() {
        // Set title for navigation bar
        title = "Tasks list"
        
        // Title color
        navigationController?.navigationBar.largeTitleTextAttributes = [
            .foregroundColor: UIColor.white
        ]
        navigationController?.navigationBar.titleTextAttributes = [
            .foregroundColor: UIColor.white
        ]
        
        // Navigation bar color
        navigationController?.navigationBar.barTintColor = UIColor(
            displayP3Red: 21/255,
            green: 101/255,
            blue: 192/255,
            alpha: 194/255
        )
        
        // Set large title
        navigationController?.navigationBar.prefersLargeTitles = true
        
        // Add button to navigation bar
        navigationItem.rightBarButtonItem = UIBarButtonItem(
            title: "Add",
            style: .plain,
            target: self,
            action: #selector(addNewTask)
        )
        
        navigationController?.navigationBar.tintColor = .white
    }
    
    @objc private func addNewTask() {
        showAlert(title: "New Task", message: "What do you want to do?")
    }
    
    // Edit task
    override func tableView(_ tableView: UITableView,
                            didSelectRowAt indexPath: IndexPath) {
        
        let cell = tableView.dequeueReusableCell(withIdentifier: cellID,
                                                 for: indexPath)
        let task = tasks[indexPath.row]
        showAlert(title: "Edit task",
                  message: "Enter new value",
                  currentTask: task) { (newValue) in
                    
            cell.textLabel?.text = newValue
            self.tableView.reloadRows(at: [indexPath], with: .automatic)
        }
    }
    
    // Delete task
    override func tableView(_ tableView: UITableView,
                            commit editingStyle: UITableViewCell.EditingStyle,
                            forRowAt indexPath: IndexPath) {
        
        let task = tasks[indexPath.row]
        
        if editingStyle == .delete {
            deleteTask(task, indexPath: indexPath)
        }
    }
}

// MARK: - UITableViewDataSource
extension ViewController {
    override func tableView(
        _ tableView: UITableView,
        numberOfRowsInSection section: Int
        ) -> Int {
        
        return tasks.count
    }
    
    override func tableView(
        _ tableView: UITableView,
        cellForRowAt indexPath: IndexPath
        ) -> UITableViewCell {
        
        let cell = tableView.dequeueReusableCell(withIdentifier: cellID,
                                                 for: indexPath)
        let task = tasks[indexPath.row]
        cell.textLabel?.text = task.name
        
        return cell
    }
}
```

### Alert Controller
```swift
// MARK: - Setup Alert Controller
extension ViewController {
    private func showAlert(title: String,
                           message: String,
                           currentTask: Task? = nil,
                           completion: ((String) -> Void)? = nil) {
        
        let alert = UIAlertController(title: title,
                                      message: message,
                                      preferredStyle: .alert)
        
        // Save action
        let saveAction = UIAlertAction(title: "Save", style: .default) { _ in
            
            guard let newValue = alert.textFields?.first?.text else { return }
            guard !newValue.isEmpty else { return }
            
            // Edit current task or add new task
            currentTask != nil ? self.editTask(currentTask!, newName: newValue) : self.saveTask(newValue)
            if completion != nil { completion!(newValue) }
        }
        
        // Cancel action
        let cancelAction = UIAlertAction(title: "Cancel", style: .destructive) { _ in
            if let indexPath = self.tableView.indexPathForSelectedRow {
                self.tableView.deselectRow(at: indexPath, animated: true)
            }
        }
        
        alert.addTextField()
        alert.addAction(saveAction)
        alert.addAction(cancelAction)
        
        // Подставляем текущую задачу в текстовое поле при редактировании задачи
        if currentTask != nil {
            alert.textFields?.first?.text = currentTask?.name
        }
        
        present(alert, animated: true)
    }
}
```

# Realm CocoaPods

### Model
```swift
import RealmSwift

class TasksList: Object {
    
    @objc dynamic var name = ""
    @objc dynamic var date = Date()
    let tasks = List<Task>()
}
```

### Data Base
```swift
import RealmSwift

let realm = try! Realm()

class StorageManager {
    static func saveTasksList(_ tasksList: TasksList) {
        try! realm.write {
            realm.add(tasksList)
        }
    }
    
    static func deleteList(_ tasksList: TasksList) {
        try! realm.write {
            let tasks = tasksList.tasks
            realm.delete(tasks)
            realm.delete(tasksList)
        }
    }
    
    static func editList(_ tasksList: TasksList, newListName: String) {
        try! realm.write {
            tasksList.name = newListName
        }
    }
    
    static func makeAllDone(_ tasksList: TasksList) {
        try! realm.write {
            tasksList.tasks.setValue(true, forKey: "isComplete")
        }
    }
}
```

### ViewControlle
```swift
import UIKit
import RealmSwift

class TasksListViewController: UITableViewController {
    var tasksLists: Results<TasksList>!

    override func viewDidLoad() {
        super.viewDidLoad()
        
        tasksLists = realm.objects(TasksList.self)
        navigationItem.leftBarButtonItem = editButtonItem
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        tableView.reloadData()
    }
    
    @IBAction func  addButtonPressed(_ sender: Any) {
        alerForAddAndUpdateList()
    }
    
    @IBAction func sortingList(_ sender: UISegmentedControl) {
        if sender.selectedSegmentIndex == 0 {
            tasksLists = tasksLists.sorted(byKeyPath: "name")
        } else {
            tasksLists = tasksLists.sorted(byKeyPath: "date")
        }
        
        tableView.reloadData()
    }
    
    // MARK: - Table view data source
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return tasksLists.count
    }
    
    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "TaskListCell", for: indexPath)
        
        let tasksList = tasksLists[indexPath.row]
        cell.configure(with: tasksList)
        
        return cell
    }
    
    // MARK: - Table view delegate
    override func tableView(_ tableView: UITableView, editActionsForRowAt indexPath: IndexPath) -> [UITableViewRowAction]? {
        
        let currentList = tasksLists[indexPath.row]
        
        let deleteAction = UITableViewRowAction(style: .default, title: "Delete") { _, _ in
            
            StorageManager.deleteList(currentList)
            tableView.deleteRows(at: [indexPath], with: .automatic)
        }
        
        let editAction = UITableViewRowAction(style: .normal, title: "Edit") { (_, _) in
            self.alerForAddAndUpdateList(currentList, complition: {
                tableView.reloadRows(at: [indexPath], with: .automatic)
            })
        }
        
        let doneAction = UITableViewRowAction(style: .normal, title: "Done") { (_, _) in
            StorageManager.makeAllDone(currentList)
            tableView.reloadRows(at: [indexPath], with: .automatic)
        }
        
        editAction.backgroundColor = .orange
        doneAction.backgroundColor = #colorLiteral(red: 0.3411764801, green: 0.6235294342, blue: 0.1686274558, alpha: 1)
        
        return [deleteAction, doneAction, editAction]
    }
    
    // MARK: - Navigation
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if let indexPath = tableView.indexPathForSelectedRow {
            let tasksList = tasksLists[indexPath.row]
            let tasksVC = segue.destination as! TasksViewController
            tasksVC.currentTasksList = tasksList
        }
    }
}
```

### Alert Controller
```swift
extension TasksListViewController {
    private func alerForAddAndUpdateList(_ listName: TasksList? = nil, complition: (() -> Void)? = nil) {
        
        var title = "New List"
        var doneButton = "Save"
        
        if listName != nil {
            title = "Edit List"
            doneButton = "Update"
        }
        
        let alert = UIAlertController(title: title, message: "Please insert new value", preferredStyle: .alert)
        var alertTextField: UITextField!
        
        let saveAction = UIAlertAction(title: doneButton, style: .default) { _ in
            guard let newList = alertTextField.text , !newList.isEmpty else { return }
            
            if let listName = listName {
                StorageManager.editList(listName, newListName: newList)
                if complition != nil { complition!() }
            } else {
                let tasksList = TasksList()
                tasksList.name = newList
                
                StorageManager.saveTasksList(tasksList)
                self.tableView.insertRows(at: [IndexPath(
                    row: self.tasksLists.count - 1, section: 0)], with: .automatic
                )
            }    
        }
        
        let cancelAction = UIAlertAction(title: "Cancel", style: .destructive)
        
        alert.addAction(saveAction)
        alert.addAction(cancelAction)
        
        alert.addTextField { textField in
            alertTextField = textField
            alertTextField.placeholder = "List Name"
        }
        
        if let listName = listName {
            alertTextField.text = listName.name
        }
        
        present(alert, animated: true)
    }
}
```