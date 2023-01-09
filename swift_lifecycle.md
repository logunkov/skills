# Swift UIKit

## AppDelegate
### Загрузка приложения завершена
```swift
func application(_ application: UIApplication, 
	didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
		return true
}
```

### Вызвается перед переходом в состояние в фоновый режим
```swift
func applicationWillResignActive(_ application: UIApplication) { }
```
    
### Вызвается при переходе в фоновый режим
```swift
func applicationDidEnterBackground(_ application: UIApplication) { }
```
    
### Вызвается перед переходом на Передний план
```swift
func applicationWillEnterForeground(_ application: UIApplication) { }
```
    
### Вызвается при переходе на Передний план
```swift
func applicationDidBecomeActive(_ application: UIApplication) { }
```

### Вызвается при завершении работы
```swift
func applicationWillTerminate(_ application: UIApplication) { }
```

## SceneDelegate
### Загрузка сцены завершена
```swift
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
	guard let _ = (scene as? UIWindowScene) else { return }
}
```

### Вызвается перед переходом в состояние в фоновый режим
```swift
func sceneWillResignActive(_ scene: UIScene) { }
```

### Вызвается при переходе в фоновый режим
```swift
func sceneDidEnterBackground(_ scene: UIScene) { }
``` 

### Вызвается перед переходом на Передний план 
```swift
func sceneWillEnterForeground(_ scene: UIScene) { }
```

### Вызвается при переходе на Передний план
```swift
func sceneDidBecomeActive(_ scene: UIScene) { }
```



### Вызвается при завершении работы
```swift
func sceneDidDisconnect(_ scene: UIScene) { }
```

## ViewController
### Инициализация view
```swift
func init() {
	super.init()
}
```

### Срабаьтывает после инициализация view
```swift
func awakeFromNib() {
	super.awakeFromNib()
}
```

### Загрузка и создание view
```swift
func loadView() {
	super.viewDidLoad()
}
```

### Срабатывает после загрузки view
```swift
func viewDidLoad() {
	super.viewDidLoad()
}
```

### Срабатывает перед появленем view на экране
```swift
func viewWillAppear(_ animated: Bool) {
	super.viewWillAppear(animated)
}
```

### Срабатывает перед тем, как размер view поменяется под размер экрана
```swift
func viewWillLayoutSubviews() { }
```

### Срабатывает после того, как размер view изменился под размер экрана
```swift
func viewDidLayoutSubviews() { }
```

### Срабатывает после появления view на экране
```swift
func viewDidAppear(_ animated: Bool) {
	super.viewDidAppear(animated)
}
```

### Срабатывает при повороте экрана
```swift
func viewWillTransition(to size: CGSize, with coordinator: UIViewControllerTransitionCoordinator) {
	super.viewWillTransition(to: size, with: coordinator)
}
```

### Срабатывает перед тем, как view закроется
```swift
func viewWillDisappear(_ animated: Bool) {
	super.viewWillDisappear(animated)
}
```

### Срабатывает после закрытия view
```swift
func viewDidDisappear(_ animated: Bool) {
	super.viewDidDisappear(animated)
}
```

