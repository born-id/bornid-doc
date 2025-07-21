---
title: SDKs
sidebar_position: 4
---

# Software Development Kits (SDKs)

We provide an iOS SDK to facilitate the easy integration of the DigiCAP Content Authenticity service. The SDK includes features for C2PA signing, media verification, fingerprint recognition, and content authentication.

## Supported Platforms

| Platform    | Version | Status       | Installation Method |
| ----------- | ------- | ------------ | ------------------- |
| **iOS**     | v0.0.1  | ✅ Supported | .a file             |
| **Android** | -       | 🔄 Planned   | -                   |

## iOS SDK (BornIDSDK)

### Installation

Currently, the SDK is planned to be provided as an `.a` file.
For detailed installation instructions, please inquire at the email address below.

**Contact**: info.bornid@digicaps.com

### Initialization

```swift
import BornIDSDK

// Configure the SDK
BornIDSDK.shared.configure(baseURL: URL, apiKey: String)
```

## API Reference

### User Authentication

Log in with your user account to access all features of the SDK.

```swift
// Login
BornIDSDK.shared.login(email: String, password: String) async throws -> User

// Usage
let user = try await BornIDSDK.shared.login(email: "user@example.com", password: "password")
```

Terminates the session of the currently logged-in user.

```swift
// Logout
BornIDSDK.shared.logout() async

// Usage
await BornIDSDK.shared.logout()
```

Checks if a user is currently logged in.

```swift
// Check login status
BornIDSDK.shared.isLoggedIn() async -> Bool

// Usage
let isLoggedIn = await BornIDSDK.shared.isLoggedIn()
```

Fetches the latest user information.

```swift
// Fetch user profile
BornIDSDK.shared.fetchMyProfile() async throws -> User

// Usage
let user = try await BornIDSDK.shared.fetchMyProfile()
```

### Media Upload

Uploads an image or video file to the server. You can include location information and a description, and optionally generate a media fingerprint.

```swift
// Upload Media
BornIDSDK.shared.uploadMedia(
    companyId: String,
    data: Data,
    mediaType: MediaType,
    location: CLLocation,
    description: String? = nil,
    fingerprint: Bool? = nil
) async throws -> URL

// Usage
let uploadURL = try await BornIDSDK.shared.uploadMedia(
    companyId: "company-id",
    data: imageData,
    mediaType: .image,
    location: currentLocation,
    description: "Description",
    fingerprint: true
)
```

### List Media

Retrieves a paginated list of media uploaded by a specific user. You can specify the number of items to fetch and the starting point.

```swift
// List Media
BornIDSDK.shared.listMedia(
    userId: String,
    limit: Int = 20,
    offset: Int = 0
) async throws -> MediaListResponse

// Usage
let mediaList = try await BornIDSDK.shared.listMedia(userId: "user-id", limit: 10)
```

### Media Verification

Analyzes the C2PA signature and metadata contained in a media file to verify the content's authenticity. It can check for manipulation and aenti provenance information.

Verifies the authenticity of media data in memory. The result is returned in JSON format.

```swift
// Verify Data
BornIDSDK.shared.verifyMedia(data: Data, ext: String) -> String?

// Usage
let result = BornIDSDK.shared.verifyMedia(data: imageData, ext: "jpg")
```

Verifies the authenticity of a media file stored in the file system. It accesses and analyzes the file via its path.

```swift
// Verify File
BornIDSDK.shared.verifyMedia(fileURL: URL, ext: String) -> String?

// Usage
let result = BornIDSDK.shared.verifyMedia(fileURL: imageURL, ext: "jpg")
```

### Location Information

Manages location permissions within the app and retrieves the current location information.

```swift
// Check location authorization status
BornIDSDK.shared.locationAuthorizationStatus() -> CLAuthorizationStatus

// Request location permission
BornIDSDK.shared.requestLocationPermission()

// Usage
if BornIDSDK.shared.locationAuthorizationStatus() == .notDetermined {
    BornIDSDK.shared.requestLocationPermission()
}
```

### Settings Management

Allows you to manage various settings of the SDK.

```swift
// Access settings manager
BornIDSDK.shared.getSettingsManager() -> SettingsManager

// Usage
let settingsManager = BornIDSDK.shared.getSettingsManager()
```

### Camera Functionality

Displays the SDK's built-in camera screen to capture photos. It can collect metadata and apply a C2PA signature simultaneously with the capture.

```swift
// Present Camera
BornIDSDK.shared.presentCamera(from: UIViewController, delegate: CameraViewControllerDelegate)

// Usage
BornIDSDK.shared.presentCamera(from: self, delegate: self)
```

## Delegate Protocol

### CameraViewControllerDelegate

```swift
protocol CameraViewControllerDelegate {
    func cameraViewController(_ controller: UIViewController, didCaptureImage image: UIImage, with metadata: [String: Any])
    func cameraViewControllerDidCancel(_ controller: UIViewController)
}
```

## Data Model

### MediaType

```swift
enum MediaType {
    case image
    case video
}
```

## Error Handling

All asynchronous functions in the SDK use Swift's standard error handling mechanism:

```swift
do {
    let user = try await BornIDSDK.shared.login(email: email, password: password)
    // Handle success
} catch {
    // Handle error
    print("Error: \(error.localizedDescription)")
}
```

## Support and Inquiries

### Technical Support

- **Email**: [info.bornid@digicaps.com](mailto:info.bornid@digicaps.com)

### System Requirements

- **iOS**: 15.0 or later
- **Xcode**: 14.0 or later
- **Swift**: 5.0 or later

---
