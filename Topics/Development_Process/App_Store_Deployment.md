# Apple App Store Deployment

## Introduction
After working towards a useable version of your mobile app, your last step would be to handle the deployment side. The main difficulties faced with submitting an app to the App Store is that they set high standards for privacy and security. You would need various certificates in order to distribute your app to the App Store as well as use certain features like: Push Notifications, Apple Pay, etc.. These are some possible hurdles to keep in mind when working on a project to release an iOS app, but they certainly help with raising the quality of your project.

## Requirements
- Apple Developer Account
- Apple Certificates
- Xcode (Requires a MacBook)


### Apple Developer Program
The most crucial component you will need to be able to deploy to the App Store is to enroll in the Apple Developer Program. You may enroll as an individual or as an organization, but keep in mind that they have different requirements for each option.


**REQUIREMENTS**:

    Individual
    - Verified Two Factor Authentication
    - Basic Personal Information

    Organization
    - Verified Two Factor Authentication
    - D-U-N-S Number
    - Legal Entity Status
    - Legal Binding Authority
    - Organization Website

The full details are available on the Apple Developer Program enrollment page: [Apple Developer Program](https://developer.apple.com/programs/enroll/)
    

### iOS-Related Certificates


- **Apple Push Notification Service** Certificate (Notifications)
- **Apple Pay Payment** Processing Certificate (Apple Pay)
- **Apple Pay Merchant** Identity Certificate (Apple Pay)
- **Pass Type** ID Certificate (Apple Wallet)
- **iOS Distribution** Certificate (Auto-Generated on Account Creation)

The full details as well as all Apple Certifications are available on the Apple Certificates page: 
[Apple Certificates](https://developer.apple.com/support/certificates/)


### Beta Testing
Prior to releasing the app for review, it would be good practice to beta test the app
for any possibly new bugs.

**For exampel:** a common error that many people find at this stage is with the push notifications. As this requires a certificate of its own, the first step should be to verify that the certificate is valid and that you have handled the distribution part of this testing stage correctly.

Below are some ways you can beta-test your app prior to releasing it onto the App Store:

#### TestFlight
TestFlight can be considered the 'App Store' for beta testing your apps. It is considered its own 'app market' and as the developer(s), you can decide whether to release your app for public testing, or keep it internal for select testers. You should also make note of the fact that submitting an app onto TestFlight will also go through a review process just like the App Store, albeit with more lenient standards which could result in a quicker review time.

#### Ad-Hoc



For further clarification about App Distribution, you can refer to these **Apple's Documentation** links below:

[Distributing your app for beta testing and releases](https://developer.apple.com/documentation/xcode/distributing-your-app-for-beta-testing-and-releases)

[Distributing your app to registered devices](https://developer.apple.com/documentation/xcode/distributing-your-app-to-registered-devices)

### App Store Submission 
There will be a full review process
<!-- TODO -->
