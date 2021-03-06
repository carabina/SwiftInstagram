<p align="center">
    <a href="https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html">
        <img src="https://rawgit.com/AnderGoig/SwiftInstagram/master/images/SwiftInstagram-Logo.png" alt="SwiftInstagram Logo" width="700" height="200">
    </a>
</p>

<p align="center">
    <a href="https://cocoapods.org/pods/SwiftInstagram">
        <img src="https://img.shields.io/cocoapods/p/SwiftInstagram.svg"
             alt="Platforms">
    </a>
    <a href="https://developer.apple.com/swift" target="_blank">
        <img src="https://img.shields.io/badge/Swift-4.0-orange.svg?style=flat"
             alt="Swift 4.0">
    </a>
    <a href="https://travis-ci.org/AnderGoig/SwiftInstagram/branches">
        <img src="https://img.shields.io/travis/AnderGoig/SwiftInstagram/master.svg"
             alt="Travis">
    </a>
    <a href="https://andergoig.github.io/SwiftInstagram/" target="_blank">
        <img src="https://img.shields.io/badge/Documentation-available-blue.svg"
             alt="Documentation">
    </a>
    <a href="https://raw.githubusercontent.com/AnderGoig/SwiftInstagram/master/LICENSE">
        <img src="https://img.shields.io/cocoapods/l/SwiftInstagram.svg"
             alt="License">
    </a>
</p>

<p align="center">
    <a href="https://cocoapods.org/pods/SwiftInstagram">
        <img src="https://img.shields.io/cocoapods/v/SwiftInstagram.svg"
             alt="CocoaPods compatible">
    </a>
    <a href="https://github.com/Carthage/Carthage">
        <img src="https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat"
             alt="Carthage compatible">
    </a>
    <a href="https://github.com/apple/swift-package-manager">
        <img src="https://img.shields.io/badge/Swift%20Package%20Manager-compatible-brightgreen.svg"
             alt="Swift Package Manager">
    </a>
</p>

---

A Swift wrapper for the Instagram API.

- [Requirements](#requirements)
- [Installation](#installation)
    - [CocoaPods](#cocoapods)
    - [Carthage](#carthage)
    - [Swift Package Manager](#swift-package-manager)
    - [Manually](#manually)
- [Usage](#usage)
    - [Authentication](#authentication---swiftinstagram-docs)
    - [Data retrieval](#data-retrieval)
- [Contributing](#contributing)
- [Credits](#credits)
- [License](#license)
- [Author](#author)

## Requirements

- iOS 9.0+
- Xcode 9.0+

## Installation

### CocoaPods

[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects. You can install it with the following command:

```bash
$ gem install cocoapods
```

> CocoaPods 1.1.0+ is required to build SwiftInstagram 1.0.0+.

To integrate SwiftInstagram into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '9.0'
use_frameworks!

pod 'SwiftInstagram', '~> 1.0.2'
```

Then, run the following command:

```bash
$ pod install
```

### Carthage

[Carthage](https://github.com/Carthage/Carthage) is a decentralized dependency manager that automates the process of adding frameworks to your Cocoa application.

You can install Carthage with [Homebrew](http://brew.sh/) using the following command:

```bash
$ brew update
$ brew install carthage
```

To integrate SwiftInstagram into your Xcode project using Carthage, specify it in your `Cartfile`:

```ogdl
github "AnderGoig/SwiftInstagram" ~> 1.0.2
```
### Swift Package Manager

To use SwiftInstagram as a [Swift Package Manager](https://swift.org/package-manager/) package just add the following in your Package.swift file.

``` swift
import PackageDescription

let package = Package(
    name: "HelloSwiftInstagram",
    dependencies: [
        .Package(url: "https://github.com/AnderGoig/SwiftInstagram.git", "1.0.2")
    ]
)
```

### Manually

If you prefer not to use either of the aforementioned dependency managers, you can integrate SwiftInstagram into your project manually.

#### Git Submodules

- Open up Terminal, `cd` into your top-level project directory, and run the following command "if" your project is not initialized as a git repository:

```bash
$ git init
```

- Add SwiftInstagram as a git [submodule](http://git-scm.com/docs/git-submodule) by running the following command:

```bash
$ git submodule add https://github.com/AnderGoig/SwiftInstagram.git
$ git submodule update --init --recursive
```

- Open the new `SwiftInstagram` folder, and drag the `SwiftInstagram.xcodeproj` into the Project Navigator of your application's Xcode project.

    > It should appear nested underneath your application's blue project icon. Whether it is above or below all the other Xcode groups does not matter.

- Select the `SwiftInstagram.xcodeproj` in the Project Navigator and verify the deployment target matches that of your application target.
- Next, select your application project in the Project Navigator (blue project icon) to navigate to the target configuration window and select the application target under the "Targets" heading in the sidebar.
- In the tab bar at the top of that window, open the "General" panel.
- Click on the `+` button under the "Embedded Binaries" section.
- You will see two different `SwiftInstagram.xcodeproj` folders each with two different versions of the `SwiftInstagram.framework` nested inside a `Products` folder.

    > It does not matter which `Products` folder you choose from.

- Select the `SwiftInstagram.framework`.

- And that's it!

> The `SwiftInstagram.framework` is automagically added as a target dependency, linked framework and embedded framework in a copy files build phase which is all you need to build on the simulator and a device.

#### Embeded Binaries

- Download the latest release from https://github.com/AnderGoig/SwiftInstagram/releases
- Next, select your application project in the Project Navigator (blue project icon) to navigate to the target configuration window and select the application target under the "Targets" heading in the sidebar.
- In the tab bar at the top of that window, open the "General" panel.
- Click on the `+` button under the "Embedded Binaries" section.
- Add the downloaded `SwiftInstagram.framework`.
- And that's it!

## Usage

SwiftInstagram uses client side (implicit) authentication, so you must **uncheck** the option "**Disable implicit OAuth**" from the _Security_ tab of your [Instagram client](https://www.instagr.am/developer/clients/manage/).

Also, copy the **Client ID** from your client and paste it inside your `Info.plist` file with `InstagramClientId` as the key.

<p align="center">
    <img src="https://rawgit.com/AnderGoig/SwiftInstagram/master/images/Info.plist-File.png" alt="Info.plist" width="735" height="40">
</p>

### Authentication - [SwiftInstagram docs](https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html#/Authentication)

```swift
let api = Instagram.shared

// Login
api.login(navController: navigationController!, redirectURI: "YOUR REDIRECTION URI GOES HERE", success: {
    // Do your stuff here ...
}, failure: { error in
    print(error)
})

// Returns whether a session is currently available or not
let _ = api.isSessionValid()

// Logout
api.logout()
```

You can also specify the [login permissions](https://www.instagram.com/developer/authorization/) with the optional parameter `scopes`, by default, it is set to basic access. To request multiple scopes at once:

```swift
api.login(navController: ..., scopes: [.likes, .comments], redirectURI: ... )
```

### Data retrieval

All of the following functions are very similar and straightforward, here's an example of retrieving recent media:

```swift
let api = Instagram.shared

api.recentMedia(fromUser: "self", count: 5, success: { (mediaSet) in
    // Do your stuff here ...
}, failure: { (error) in
    print(error.localizedDescription)
})
```

#### Users - [SwiftInstagram docs](https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html#/User%20Endpoints) - [Official docs](http://instagr.am/developer/endpoints/users/)

```swift
api.user(_ userId: String, success: SuccessHandler<InstagramUser>? = default, failure: FailureHandler? = default)
api.recentMedia(fromUser userId: String, maxId: String = default, minId: String = default, count: Int = default, success: SuccessHandler<[InstagramMedia]>? = default, failure: FailureHandler? = default)
api.userLikedMedia(maxLikeId: String = default, count: Int = default, success: SuccessHandler<[InstagramMedia]>? = default, failure: FailureHandler? = default)
api.search(user query: String, count: Int = default, success: SuccessHandler<[InstagramUser]>? = default, failure: FailureHandler? = default)
```

#### Relationships - [SwiftInstagram docs](https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html#/Relationship%20Endpoints) - [Official docs](http://instagr.am/developer/endpoints/relationships/)

```swift
api.userFollows(success: SuccessHandler<[InstagramUser]>? = default, failure: FailureHandler? = default)
api.userFollowers(success: SuccessHandler<[InstagramUser]>? = default, failure: FailureHandler? = default)
api.userRequestedBy(success: SuccessHandler<[InstagramUser]>? = default, failure: FailureHandler? = default)
api.userRelationship(withUser userId: String, success: SuccessHandler<InstagramRelationship>? = default, failure: FailureHandler? = default)
api.follow(user userId: String, success: SuccessHandler<InstagramRelationship>? = default, failure: FailureHandler? = default)
api.unfollow(user userId: String, success: SuccessHandler<InstagramRelationship>? = default, failure: FailureHandler? = default)
api.approveRequest(fromUser userId: String, success: SuccessHandler<InstagramRelationship>? = default, failure: FailureHandler? = default)
api.ignoreRequest(fromUser userId: String, success: SuccessHandler<InstagramRelationship>? = default, failure: FailureHandler? = default)
```

#### Media - [SwiftInstagram docs](https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html#/Media%20Endpoints) - [Official docs](http://instagr.am/developer/endpoints/media/)

```swift
api.media(withId id: String, success: SuccessHandler<InstagramMedia>? = default, failure: FailureHandler? = default)
api.media(withShortcode shortcode: String, success: SuccessHandler<InstagramMedia>? = default, failure: FailureHandler? = default)
api.searchMedia(lat: Double = default, lng: Double = default, distance: Int = default, success: SuccessHandler<[InstagramMedia]>? = default, failure: FailureHandler? = default)
```

#### Comments - [SwiftInstagram docs](https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html#/Comment%20Endpoints) - [Official docs](http://instagr.am/developer/endpoints/comments/)

```swift
api.comments(fromMedia mediaId: String, success: SuccessHandler<[InstagramComment]>? = default, failure: FailureHandler? = default)
api.createComment(onMedia mediaId: String, text: String, failure: FailureHandler? = default)
api.deleteComment(_ commentId: String, onMedia mediaId: String, failure: FailureHandler? = default)
```

#### Likes - [SwiftInstagram docs](https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html#/Like%20Endpoints) - [Official docs](http://instagr.am/developer/endpoints/likes/)

```swift
api.likes(inMedia mediaId: String, success: SuccessHandler<[InstagramUser]>? = default, failure: FailureHandler? = default)
api.like(media mediaId: String, failure: FailureHandler? = default)
api.unlike(media mediaId: String, failure: FailureHandler? = default)
```

#### Tags - [SwiftInstagram docs](https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html#/Tag%20Endpoints) - [Official docs](http://instagr.am/developer/endpoints/tags/)

```swift
api.tag(_ tagName: String, success: SuccessHandler<InstagramTag>? = default, failure: FailureHandler? = default)
api.recentMedia(withTag tagName: String, maxTagId: String = default, minTagId: String = default, count: Int = default, success: SuccessHandler<[InstagramMedia]>? = default, failure: FailureHandler? = default)
api.search(tag query: String, success: SuccessHandler<[InstagramTag]>? = default, failure: FailureHandler? = default)
```

#### Locations - [SwiftInstagram docs](https://andergoig.github.io/SwiftInstagram/Classes/Instagram.html#/Location%20Endpoints) - [Official docs](http://instagr.am/developer/endpoints/locations/)

```swift
api.location(_ locationId: String, success: SuccessHandler<InstagramLocation>? = default, failure: FailureHandler? = default)
api.recentMedia(forLocation locationId: String, maxId: String = default, minId: String = default, success: SuccessHandler<[InstagramMedia]>? = default, failure: FailureHandler? = default)
api.searchLocation(lat: Double = default, lng: Double = default, distance: Int = default, facebookPlacesId: String = default, success: SuccessHandler<[InstagramLocation]>? = default, failure: FailureHandler? = default)
```

## Contributing

If you have feature requests or bug reports, feel free to help out by sending pull requests or by [creating new issues](https://github.com/AnderGoig/IGAuth/issues/new). Please take a moment to
review the [CONTRIBUTING](.github/CONTRIBUTING.md) guidelines.

## Credits

SwiftInstagram is brought to you by [Ander Goig](https://github.com/AnderGoig) and [contributors to the project](https://github.com/AnderGoig/SwiftInstagram/contributors). If you're using SwiftInstagram in your project, attribution would be very appreciated.

#### Companion libraries

SwiftInstagram uses [keychain-swift](https://github.com/evgenyneu/keychain-swift) by [@evgenyneu](https://github.com/evgenyneu) to safely store the access token retrieved by the authentication process.

## License

SwiftInstagram is released under the MIT license. See [LICENSE](LICENSE) for details.

## Author

Ander Goig, [goig.ander@gmail.com](mailto:goig.ander@gmail.com)

[https://github.com/AnderGoig/SwiftInstagram](https://github.com/AnderGoig/SwiftInstagram)
