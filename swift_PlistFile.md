# Swift PlistFile
### Model
```swift
struct User: Encodable, Decodable {
    var name = "User"
    var surname = "Name"
    
    var encoded: Data? {
        let encoder = PropertyListEncoder()
        return try? encoder.encode(self)
    }
    
    init?(from data: Data) {
        let decoder = PropertyListDecoder()
        guard let user = try? decoder.decode(User.self, from: data) else { return nil }
        name = user.name
        surname = user.surname
    }
    
    init() {}
}
```

### Storage
```swift
class StorageMager {
    static let shared = StorageMager()
    
    private var user = User()
    private let defaults = UserDefaults.standard
    
    private let documentDirectory = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask).first!
    private var archiveURL: URL!
    
    init() {
        archiveURL = documentDirectory.appendingPathComponent("User").appendingPathExtension("plist")
    }
    
    func getUser() -> User {
        guard let savedUser = defaults.object(forKey: "savedUser") as? Data else { return user }
        guard let loadedUser = try? JSONDecoder().decode(User.self, from: savedUser) else { return user }
        user = loadedUser
        return user
    }
    
    func saveUser(_ user: User) {
        guard let userEncoded = try? JSONEncoder().encode(user) else { return }
        defaults.set(userEncoded, forKey: "savedUser")
    }
    
    func saveUserToFile(_ user: User) {
        let encoder = PropertyListEncoder()
        guard let encodedUser = try? encoder.encode(user) else { return }
        try? encodedUser.write(to: archiveURL, options: .noFileProtection)
    }
    
    func getUserFromFile() -> User {
        guard let savedUser = try? Data(contentsOf: archiveURL) else { return user }
        let decoder = PropertyListDecoder()
        guard let loadedUser = try? decoder.decode(User.self, from: savedUser) else { return user }
        user = loadedUser
        return user
    }
}
```