# Swift NSCache
### Image Caching
```swift
class ImageView: UIImageView {
    func fetchImage(with url: String?) {
        guard let url = url else { return }
        guard let imageURL = url.getURL() else {
            image = #imageLiteral(resourceName: "picture")
            return
        }
        
        // Если изображение есть в кэше, то используем его
        if let cachedImage = getCachedImage(url: imageURL) {
            image = cachedImage
            return
        }
        
        URLSession.shared.dataTask(with: imageURL) { data, response, error in
            if let error = error { print(error); return }
            guard let data = data, let response = response else { return }
            guard let responseURL = response.url else { return }
            
            if responseURL.absoluteString != url { return }
            
            DispatchQueue.main.async {
                self.image = UIImage(data: data)
            }
            
            // Сохраняем изображение в кэш
            self.saveImageToCache(data: data, response: response)
        }.resume()
    }
    
    private func saveImageToCache(data: Data, response: URLResponse) {
        guard let responseURL = response.url else { return }
        let cashedResponse = CachedURLResponse(response: response, data: data)
        URLCache.shared.storeCachedResponse(cashedResponse, for: URLRequest(url: responseURL)) 
    }
    
    private func getCachedImage(url: URL) -> UIImage? {
        if let cacheResponse = URLCache.shared.cachedResponse(for: URLRequest(url: url)) {
            return UIImage(data: cacheResponse.data)
        }
        
        return nil
    }
}
```

### extension String
```swift
fileprivate extension String {
    func getURL() -> URL? {
        guard let url = URL(string: self) else { return nil}
        return url
    }
}
```