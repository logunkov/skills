# Swift URLSession

## URLSessionTask `cancel, resume, suspend`
* URLSessionDownloadTask `downloadTask(with:)`
* URLSessionDataTask `dataTask(with:)` ---> URLSessionUploadTask `uploadTask(with: from:)`

## URLSessionConfiguration
Быстро + Просто - Использование данных = URLSession Singelton `URLSession.shared.configuration`  
Просто + Использование данных = Default `URLSession.configuration.default`  
Dafault - Запись на диск  = Ephemeral `URLSession.configuration.ephemeral`  
Dafault + Фоновый режим  = Background`URLSession.configuration.background`

# URLSession

## Model
```swift
struct Course: Decodable {
    let name: String?
    let link: String?
    let imageUrl: String?
    let numberOfLessons: String?
    let numberOfTests: String?
    
    enum CodingKeys: String, CodingKey {
        case name = "Name"
        case link = "Link"
        case imageUrl = "ImageUrl"
        case numberOfLessons = "Number_of_lessons"
        case numberOfTests = "Number_of_tests"
    }
    
    init(dictCourse: [String: Any]) {
        name = dictCourse["name"] as? String
        link = dictCourse["link"] as? String
        imageUrl = dictCourse["imageUrl"] as? String
        numberOfLessons = dictCourse["numberOfLessons"] as? String
        numberOfTests = dictCourse["numberOfTests"] as? String
    }
    
    static func getCourses(from jsonData: Any) -> [Course] {
        guard let jsonData = jsonData as? Array<[String: Any]> else { return [] }

        // Version 1
        var courses: [Course] = []
        
        for dictCourse in jsonData {
            let course = Course(dictCourse: dictCourse)
            courses.append(course)
        }

        // Version 2
        return jsonData.compactMap { Course(dictCourse: $0) }
    }
}
```

## URL
```swift
class ViewController: UIViewController {
    private let imageUrl = "https://applelives.com/wp-content/uploads/2016/03/iPhone-SE-11.jpeg"

    @IBOutlet var imageView: UIImageView!
    @IBOutlet var activityIndicator: UIActivityIndicatorView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        fetchImage()
        activityIndicator.startAnimating()
        activityIndicator.hidesWhenStopped = true
    }

    private func fetchImage() {    
        guard let url = URL(string: imageUrl) else { return }
        
        URLSession.shared.dataTask(with: url) { (data, response, error) in
            if let error = error {
                print(error.localizedDescription)
                return
            }
            
            if let response = response {
                print(response)
            }
            
            if let data = data, let image = UIImage(data: data) {
                DispatchQueue.main.async {
                    self.activityIndicator.stopAnimating()
                    self.imageView.image = image
                }
            }
        }.resume()
    }
}
```

## Post URLSession
```swift
func postRequest() {
    guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts") else { return }
    
    let userData = [
        "course": "Networking",
        "lesson": "GET and POST"
    ]
    
    var request = URLRequest(url: url)
    request.httpMethod = "POST"
    request.addValue("application/json", forHTTPHeaderField: "Content-Type")
    
    guard let httpBody = try? JSONSerialization.data(withJSONObject: userData, options: []) else { return }
    request.httpBody = httpBody
    
    URLSession.shared.dataTask(with: request) { (data, response, _) in
        guard let response = response, let data = data else { return }
        
        print(response)
        
        do {
            let json = try JSONSerialization.jsonObject(with: data, options: [])
            print(json)
        } catch let error {
            print(error)
        }
        
    }.resume()
}
```

## Get URLSession
```swift
private let jsonUrl = "https://swiftbook.ru//wp-content/uploads/api/api_courses"
private var courses: [Course] = []

func fetchData() {
    guard let url = URL(string: jsonUrl) else { return }
    
    URLSession.shared.dataTask(with: url) { (data, _, _) in
        
        guard let data = data else { return }
        
        do {
            let decoder = JSONDecoder()
//            decoder.keyDecodingStrategy = .convertFromSnakeCase
            self.courses = try decoder.decode([Course].self, from: data)
            
            DispatchQueue.main.async {
                self.tableView.reloadData()
            }
        } catch let error {
            print(error)
        }
    }.resume()
}
```

# Alamofire
## Post Alamofire
```swift
func postRequestWithAlamofire() {
    guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts") else { return }
    
    let userData: [String: Any] = [
        "name": "Network Requests",
        "link": "https://swiftbook.ru/contents/our-first-applications/",
        "imageUrl": "https://swiftbook.ru/wp-content/uploads/sites/2/2018/08/notifications-course-with-background.png",
        "numberOfLessons": "18",
        "numberOfTests": "10"
    ]
    
    request(url, method: .post, parameters: userData).validate().responseJSON { responseData in
        switch responseData.result {
        case .success(let value):
            guard let jsonData = value as? [String: Any] else { return }
            
            let course = Course(dictCourse: jsonData)
            self.courses.append(course)
            DispatchQueue.main.async {
                self.tableView.reloadData()
            }
            
        case .failure(let error):
            print(error)
        }
    }
}
```

## Get Alamofire
```swift
private let jsonUrl = "https://swiftbook.ru//wp-content/uploads/api/api_courses"
private var courses: [Course] = []

func fetchDataWithAlamofire() {
    guard let url = URL(string: jsonUrl) else { return }
    
    request(url).validate().responseJSON { dataResponse in
        switch dataResponse.result {
        case .success(let value):
            self.courses = Course.getCourses(from: value)
            DispatchQueue.main.async {
                self.tableView.reloadData()
            }
        case .failure(let error):
            print(error)
        }
    }
}
```