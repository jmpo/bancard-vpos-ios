# BancardVposConnector

[![Version](https://img.shields.io/cocoapods/v/BancardVposConnector.svg?style=flat)](https://cocoapods.org/pods/BancardVposConnector)
[![License](https://img.shields.io/cocoapods/l/BancardVposConnector.svg?style=flat)](https://cocoapods.org/pods/BancardVposConnector)
[![Platform](https://img.shields.io/cocoapods/p/BancardVposConnector.svg?style=flat)](https://cocoapods.org/pods/BancardVposConnector)

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Requirements

* Swift 4.
* Xcode 9+.

## Installation

BancardVposConnector is available through [CocoaPods](https://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'BancardVposConnector'
```

## Usage
Using this connector is straightforward:

1- Import `BancardVposConnector` on your swift file.

2- Create either a new `CardVPOSView` or `CheckoutVPOSView` and add it to your view hierarchy. These views work as any other UIView, so feel free to create it via storyboard, xib or code.

3- Set your view's `mode` to `.sandbox` or `.production`

4- Implement it's delegate (`CardVPOSDelegate` or `CheckoutVPOSDelegate`) to listen to the success and failure callbacks.

5- You are now good to go! Just call `myView.load(with: processId, styles: [:])` to start using it.

### Example

```swift
import BancardVposConnector

class ViewController: UIViewController {
  /*
    The container view where we are going to add our VPOSView,
    in this case, a CheckoutVPOSView to make a payment.
    You could use a direct outlet yo the CheckoutVPOSView,
    or init it completely by code.
  */
  @IBOutlet weak var vPOSContainer: UIView!
  // Here we init our VPOSView in sandbox mode.
  lazy var vPView: VPOSView = {
    let vpView = CheckoutVPOSView()
    vpView.delegate = self
    vpView.mode = .sandbox
    return vpView
  }()

  override func viewDidLoad() {
    super.viewDidLoad()
    vPOSContainer.addSubview(vPView)
    // Add the neccessary constraints and other code of your own ....
  }

  //Your VC's code .....
}
// Here we implement the CheckoutVPOSDelegate
extension ViewController: CheckoutVPOSDelegate {
  func paymentFailed(with returnURL: String) {
    // Continue with your own logic for processing the returnURL when the payment fails.
  }
  func paymentSuccess(with returnURL: String) {
    // Continue with your own logic for processing the returnURL when the payment succeeds.
  }
}
```

If you needs more details, please check out the example project in this repository.

## Author

Mauricio Cousillas, mauricio.cousillas@moove-it.com

## License

BancardVposConnector is available under the MIT license. See the LICENSE file for more info.
