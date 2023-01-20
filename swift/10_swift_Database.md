# Swift Core Data
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
}

// MARK: - Setup Alert Controller
extension ViewController {
    private func showAlert(title: String, message: String) {
        let alert = UIAlertController(title: title,
                                      message: message,
                                      preferredStyle: .alert)
        
        // Save action
        let saveAction = UIAlertAction(title: "Save", style: .default) { _ in
            
            guard let newValue = alert.textFields?.first?.text else { return }
            guard !newValue.isEmpty else { return }
            
            self.saveTask(newValue)
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
        
        present(alert, animated: true)
    }
}
```