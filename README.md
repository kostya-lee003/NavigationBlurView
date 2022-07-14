# NavigationBlurView
UINavigationBlurView : TemplateView

## Description

![Simulator Screen Recording - iPhone 13 Pro Max - 2022-07-14 at 15 44 57](https://user-images.githubusercontent.com/72404363/178982281-5763ad9c-5bf5-42d7-a12b-261955460ce7.gif)


UIVisualEffectView is for creating blur effect and container (UINavigationBlurContainerView) is for backButton, titleLabel, titleView and rightBarButtons.


![navigationBar-2](https://user-images.githubusercontent.com/72404363/178979094-fc45a045-c218-4e39-89e8-b1c5869931ad.jpg)


## Usage

- In your controller declare a variable
```swift
var navigationBlurView: UINavigaitonBlurView = UINavigaitonBlurView()
```



- In initialize() method initialize container by using initializeContainer() method and assign back action for back button:
```swift
navigationBlurView.initializeContainer(title: "Your title", rightBarButtons: [Your buttons], buttonsSize: CGSize())
navigationBlurView.container.backButtonAction = backAct
```

There are several initializeContainer methods:

<img width="700" alt="Screen Shot 2022-07-14 at 17 20 41" src="https://user-images.githubusercontent.com/72404363/178981116-0515d7ca-9a42-4165-ad2a-4a09b9cd3125.png">

If back button is not needed then just:
```swift
navigationBlurView.container.backButton.isHidden = true
```

- add navigationBlurView as subview.
!!!Make sure that your navigationBlurView is above all other views!!!

To create such view:

![Group 27714](https://user-images.githubusercontent.com/72404363/178982447-82f70adc-b712-4bfa-afd8-f3cb91793fe0.jpg)

use titleView inside container.

## Search bar and chats/messages selection bar

![Simulator Screen Recording - iPhone 13 Pro Max - 2022-07-14 at 16 43 29](https://user-images.githubusercontent.com/72404363/178983925-c0804b4f-3a6e-480a-880d-0e1613cf2279.gif)
![Simulator Screen Recording - iPhone 13 Pro Max - 2022-07-14 at 16 43 55](https://user-images.githubusercontent.com/72404363/178983940-aedb54d7-71e4-44a9-99c4-84befdd37eeb.gif)


In a case of search bar you can use it as simple search bar assigning its delegate to your controller:
```swift
navigationBlurView.searchBar.delegate = self
```

Also create cancelButtonClicked() and make it @objc for your cancel button:
```swift
navigationBlurView.cancelButton.addTarget(self, action: #selector(cancelButtonClicked), for: .touchUpInside)
```

You have to configure your cancelButtonClicked method because you can have either message selection, search or both cases.
(code for both cases)

```swift
@objc func CancelButtonClicked() {
    if navigationBlurView.barStatus == .searchBar {
        navigationBlurView.hideSearchBar()
        navigationBlurView.searchBar.endEditing(true)   // hides keyboard
    } else if navigationBlurView.barStatus == .messageSelection {
        navigationBlurView.hideMessagesSelection(completion: nil)
    } else {
        fatalError()
    }
}
```

To show either of search bar or selection bar in your button's @objc method add:

```swift
navigationBlurView.showSearchBar()
```

or

```swift
navigationBlurView.messagesSelectedLabel.text = "0 messages, 0 selected"
navigationBlurView.showMessagesSelection(completion: nil)
```


