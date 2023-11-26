# Apple App Store Deployment

## Introduction
After working towards a useable version of your mobile app, your last step would be to handle the deployment side. The main difficulties faced with submitting an app to the App Store is that they set high standards for privacy and security. You would need various certificates in order to distribute your app to the App Store as well as use certain features like: Push Notifications, Apple Pay, etc.. These are some possible hurdles to keep in mind when working on a project to release an iOS app, but they certainly help with raising the quality of your project.

## Requirements
- Apple Developer Account
- Certificates
<!-- TODO -->


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
    

### Certificates
- Apple Push Notification Service Certificate
- Apple Pay Payment Processing Certificate
- Apple Pay Merchant Identity Certificate
- Pass Type ID Certificate
- iOS Distribution Certificate

The full details are available on the Apple Certificates page: 
[Apple Certificates](https://developer.apple.com/support/certificates/)


### TestFlight Beta Testing
Prior to releasing the app for review, it would be good practice to beta test the app
for any possibly new bugs. A common error that many people find at this stage is with the push notifications. As this requires a certificate of its own, the first step should be to verify that the certificate is valid and that you have handled the distribution part of this testing stage correctly.
<!-- TODO? More Examples? More Explanation? -->

### Review 
There will be a full review process
<!-- TODO -->
