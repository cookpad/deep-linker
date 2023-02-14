# DeepLinker

A very simple static page to help test Universal Links in E2E automation - <https://cookpad.github.io/deep-linker>

# Usage

## XCUITest

```swift
extension XCTestCase {
    func openUniversalLink(_ link: String) throws {
        // Create the DeepLinker URL for the target universal link
        var components = URLComponents()
        components.scheme = "https"
        components.host = "cookpad.github.io"
        components.path = "deep-linker"
        components.queryItems = [
            URLQueryItem(name: "link", value: link)
        ]
        let url = try XCTUnwrap(components.url)

        // Open Safari and and navigate to the Deep Link test page
        let safari = XCUIApplication(bundleIdentifier: "com.apple.mobilesafari")
        safari.launch()
        safari.textFields["Address"].tap()
        safari.typeText(url.absoluteString)
        safari.keyboards.buttons["Go"].tap()

        // Invoke the deep link on the page
        safari.links["deep-link"].safeTap()
    }
}
```
