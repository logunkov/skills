# Swift UIKit

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

## Swift keyboard

### Скрытие клавиатуры по тапу за пределами Text View
```swift
override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
    super.touchesBegan(touches, with: event)
    view.endEditing(true)
}
```

### Скрываем клавиатуру нажатием на "Done"
```swift
func textFieldShouldReturn(_ textField: UITextField) -> Bool {
    textField.resignFirstResponder()
    return true
}
```
    
### Метод для отображения кнопки "Готово" на цифровой клавиатуре
```swift
private func addDoneButtonTo(_ textField: UITextField) {
    
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