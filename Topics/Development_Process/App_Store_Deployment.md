# Apple App Store Deployment

## Table of Contents
### [Introduction](#introduction-1)
### [Requirements](#requirements-1)
### [Certificates](#certificates-1)
- [iOS Related Certificates](#ios-related-certificates)
- [Certificate Creation](#certificate-creation)
### [Beta Testing](#beta-testing-1)
- [TestFlight](#testflight)
- [Ad hoc](#ad-hoc)
### [Distribution Process](#distribution-process-1)
### [App Store Submission](#app-store-submission-1)
### [Additional Information](#additional-information-1)

## Introduction
After working towards a useable version of your mobile app, your last step would be to manage the deployment side. 
The main difficulties faced with submitting an app to the App Store is that they set high standards for privacy and security. 
You would need various certificates in order to distribute your app to the App Store as well as use certain features like: Push Notifications, Apple Pay, etc. 
These are some possible hurdles to keep in mind when working on a project to release an iOS app, but they certainly help with raising the quality of your project.

## Requirements
- Apple Developer Account
    - The most crucial component you will need to be able to deploy to the App Store is to enroll in the Apple Developer Program. 
    You may enroll as an individual or as an organization, but keep in mind that they have different requirements for each option, as listed below.
- Apple Certificates
- Xcode (Requires a MacBook)
- Established Privacy Policy & Terms and Conditions


**EXTRA REQUIREMENTS**:

    Individual
    - Verified Two Factor Authentication
    - Basic Personal Information

    Organization
    - Verified Two Factor Authentication
    - D-U-N-S Number
    - Legal Entity Status
    - Legal Binding Authority
    - Organization Website

The full details of the Apple Developer Account requirements are available on the Apple Developer Program enrollment page: [Apple Developer Program](https://developer.apple.com/programs/enroll/)
    

### Certificates

#### iOS Related Certificates
- **Apple Push Notification Service** Certificate (Notifications)
    - Handles push notifications that you would receive when you're not currently using the app (i.e., New Message from ________).
- **Apple Pay Payment** Processing Certificate (Apple Pay)
    - Uses your certificate's key to encrypt the payment data to enhance security.
- **Apple Pay Merchant** Identity Certificate (Apple Pay)
    - Allows you to register as a valid merchant that can accept Apple Pay as a payment option.
- **Pass Type** ID Certificate (Apple Wallet)
    - Sign Apple Wallet passes.
- **iOS Distribution** Certificate (Auto-Generated on Account Creation)

#### Certificate Creation
To create certificates, you can head to the Certifications tab on the Apple Developer Website and choose which ones are applicable to your app. After, you would need to generate a CSR (Certificate Signing Request) on your MacBook.
Apple's Certificates job states to follow [these steps](https://developer.apple.com/help/account/create-certificates/create-a-certificate-signing-request/) in order to generate the certificate:
1. Launch Keychain Access located in /Applications/Utilities.

2. Choose Keychain Access > Certificate Assistant > Request a Certificate from a Certificate Authority.

3. In the Certificate Assistant dialog, enter an email address in the User Email Address field.

4. In the Common Name field, enter a name for the key (for example, Gita Kumar Dev Key).

5. Leave the CA Email Address field empty.

6. Choose “Saved to disk,” then click Continue.

Now you can upload this CSR onto the website to generate your certificate.

The full details on all of Apple's Certifications are available on the Apple Certificates page: 
[Apple Certificates](https://developer.apple.com/support/certificates/)


### Beta Testing
Prior to releasing the app for review, it would be good practice to beta test the app for any possibly new bugs.

**For example:** a common error that many people find at this stage is with the push notifications. 
As this requires a certificate of its own, the first step should be to verify that the certificate is valid and that you have managed the distribution part of this testing stage correctly.

In terms of beta testing, the two main choices are [TestFlight](#testflight-1) and [Ad-Hoc](#ad-hoc-1). They are two ways of distributing your app to your testers and while they will get both get the job done it is best to choose the one that best suits your needs. You will need to decide whether you prefer to keep your testing internal and only for those involved in the development process (limited access) or external and open to the public. 

#### TestFlight
TestFlight can be considered the 'App Store' for beta testing your apps. 
It is considered its own 'app market' and as the developer(s), you can decide whether to release your app for public testing or keep it internal for select testers. This makes use of App Store connect, which eases the process of uploading your apps onto the App Store. 
From there, you will be able to submit your app to both TestFlight and the App Store if you'd like. 
You should also make note of the fact that submitting an app onto TestFlight will also go through a review process just like the App Store, albeit with more lenient standards which could result in a quicker review time.

#### Ad Hoc
Ad hoc allows you to distribute your app to a limited number (100) of registered devices. 
Unlike TestFlight, this cannot release it for 'public testing' to all beta testers, so you would have to register the devices you wish to use in the devices section on the Apple Developer Page. This means that you would have to register their device first by entering it's UDID (Unique Device Identifier) onto the App Developer page. 

- This can be found by plugging in your iPhone to your MacBook, going onto Xcode, then clicking Window tab to Devices and Simulators. 
From there you can select your iPhone and copy its UDID (make sure to include the '-' that is found after the eighth character).

The benefit of using Ad hoc is that you would not need the app to be reviewed before distributing it out for testing. This means that you would be able to get your app to your testers immediately and possibly avoid getting the app rejected during the review process.

### Distribution Process
After you generate all your needed certificates, you would then need to register your **Provisioning Profile**, which grants you the permission to use, develop and distribute your app on Apple services. This is another security measure that verifies if your provisioning profile's App ID matches both your app and a valid distribution certificate. 

To complete your provisioning profile, you would select the profiles page on the Apple Developer website and select the **iOS App Development** option. Then, you would select the app you wish to distribute as well as whether or not you would like to have offline support. After this, you would select all the certifications required in order for the app to function as well as all of the devices (iPhone/iPad/Mac) you want accessing it (if you chose to use [Ad-Hoc](#ad-hoc-1)). 
You would then complete the registration process and download the profile to import onto Xcode where you will proceed to build the app.

Now you can decide how you would like to distribute the app, where you can choose between the following options for distribution:
- App Store Connect ([TestFlight](#testflight-1)/App Store)
- [Ad-Hoc](#ad-hoc-1)
- Enterprise
- Development

Should you choose [TestFlight](#testflight-1) in App Store Connect, your process would be simple, and you can follow further directions online on how your testers can download your app on the TestFlight app market. 
Following the steps would allow you to easily upload your .ipa onto App Store Connect where you can manage your next steps online.

If you chose to use [Ad-Hoc](#ad-hoc-1), however, you would build a .ipa which you can send to your testers to install onto their device or device simulator on Xcode.

For further clarification about App Distribution, you can refer to these **Apple's Documentation** links below:

- [Distributing your app for beta testing and releases](https://developer.apple.com/documentation/xcode/distributing-your-app-for-beta-testing-and-releases)

- [Distributing your app to registered devices](https://developer.apple.com/documentation/xcode/distributing-your-app-to-registered-devices)

### App Store Submission 
There will be a full review process, which should be completed within 24 hours according to Apple, but it may take longer depending on your app.
In comparison to TestFlight's review process, since this would go to the official App Store, they will be enforcing stricter standards.

It would be good practice to continuously develop your app keeping proper safety and privacy guidelines in mind, but in case you would like to assess on your own prior to submission, you could refer to these specific review guidelines:

- [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)

- [Human Interface Design Guidelines](https://developer.apple.com/design/human-interface-guidelines/)

- [Guidelines for Using Apple Trademarks and Copyrights](https://www.apple.com/legal/intellectual-property/guidelinesfor3rdparties.html)


If you used [TestFlight](#testflight) for beta testing earlier, you should be familiar with this process as it is very similar for the App Store Review. If you used Ad hoc to test, then you may refer to the steps mentioned in the TestFlight process in getting the .ipa uploaded onto App Store Connect.

Now you are ready to submit your app for review in App Store Connect. 
This is what you can consider to be your dashboard in managing your apps. 
You are able to view sales, access app analytics, as well as submit your app for App Store Review.

After selecting the app to 'Add for Review' you must also provide:

- Information to provide App Store Reviewers:
    - Contact information
    - Notes/Documentation
    - Demo Account (if applicable)
- Description and Features
- Any extra information that pertains to how you would like your app to be presented:
    - App banners, app promotions, etc.

Congratulations! From this point on, all you have to do is sit back and wait for the review decision to come out. Make sure to make the appropriate changes if they were requested or download your app from the official App Store if it was approved!

### Additional Information

For further information on the App Review process, please consult Apple's [App Review Docs](https://developer.apple.com/app-store/review/#:~:text=On%20average%2C%2090%25%20of%20submissions,app%20for%20iPhone%20and%20iPad.). This contains all the steps, common issues, as well as contact information if you need further help in the app review process.
