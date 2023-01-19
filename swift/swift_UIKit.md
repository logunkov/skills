# Swift UIKit

## Alert
```swift
func wrongFormatAlert() {
    let alert = UIAlertController(
        title: "Wrong Format!",
        message: "Please enter your name",
        preferredStyle: .alert)
    
    let okAction = UIAlertAction(title: "OK", style: .default, handler: nil)
    alert.addAction(okAction)
    present(alert, animated: true, completion: nil)
}
```

## Segue
### UIStoryboardSegue
```swift
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
    if segue.identifier == "edit" {
        let thirdVC = segue.destination as! ThirdViewController
        thirdVC.text = segue.identifier
    }
}
```

### unwindSegue
```swift
@IBAction func unwindSegue(segue: UIStoryboardSegue) {
    let thirdVC = segue.source as! ThirdViewController
    title = thirdVC.text
}
```

## Keyboard
### Скрытие клавиатуры по тапу за пределами Text View
```swift
override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
    super.touchesBegan(touches, with: event)
    view.endEditing(true)
}
```

### Скрытие клавиатуры
```swift
textField.delegate = self
    
NotificationCenter.default.addObserver(self,
    selector: #selector(adjustInsetForKeyboard(_:)),
    name: UIResponder.keyboardWillHideNotification,
    object: nil
)
NotificationCenter.default.addObserver(self,
    selector: #selector(adjustInsetForKeyboard(_:)),
    name: UIResponder.keyboardWillShowNotification,
    object: nil)
    
@objc func adjustInsetForKeyboard(_ notification: NSNotification) {
    guard let userInfo = notification.userInfo else { return }
    
    let keyboardFrame = (userInfo[UIResponder.keyboardFrameEndUserInfoKey] as! NSValue).cgRectValue
    
    let show = (notification.name == UIResponder.keyboardWillShowNotification) ? true : false
    
    let bottomInset = (keyboardFrame.height + 20) * (show ? 1 : 0)
    scrollView.contentInset.bottom = bottomInset
    scrollView.verticalScrollIndicatorInsets.bottom = bottomInset
}

extension ViewController: UITextFieldDelegate {
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        textField.resignFirstResponder()
        return true
    }
}
```
    
### Метод для отображения кнопки "Готово" на цифровой клавиатуре
```swift
func addDoneButtonTo(_ textField: UITextField) {
    
    let keyboardToolbar = UIToolbar()
    textField.inputAccessoryView = keyboardToolbar
    keyboardToolbar.sizeToFit()
    
    let doneButton = UIBarButtonItem(title:"Done",
                                     style: .done,
                                     target: self,
                                     action: #selector(didTapDone))
    
    let flexBarButton = UIBarButtonItem(barButtonSystemItem: .flexibleSpace,
                                        target: nil,
                                        action: nil)
    
    keyboardToolbar.items = [flexBarButton, doneButton]
}
    
@objc private func didTapDone() {
    view.endEditing(true)
}
```
