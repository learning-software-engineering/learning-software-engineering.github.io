# Apple App Store Deployment

## Introduction
After working towards a useable version of your mobile app, your last step would be to handle the deployment side. 
The main difficulties faced with submitting an app to the App Store is that they set high standards for privacy and security. 
You would need various certificates in order to distribute your app to the App Store as well as use certain features like: Push Notifications, Apple Pay, etc.. 
These are some possible hurdles to keep in mind when working on a project to release an iOS app, but they certainly help with raising the quality of your project.

## Requirements
- Apple Developer Account
- Apple Certificates
- Xcode (Requires a MacBook)
- Established Privacy Policy & Terms and Conditions


### Apple Developer Program
The most crucial component you will need to be able to deploy to the App Store is to enroll in the Apple Developer Program. 
You may enroll as an individual or as an organization, but keep in mind that they have different requirements for each option.


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

The full details are available on the Apple Developer Program enrollment page: [Apple Developer Program](https://developer.apple.com/programs/enroll/)
    

### iOS-Related Certificates


- **Apple Push Notification Service** Certificate (Notifications)
- **Apple Pay Payment** Processing Certificate (Apple Pay)
- **Apple Pay Merchant** Identity Certificate (Apple Pay)
- **Pass Type** ID Certificate (Apple Wallet)
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
Prior to releasing the app for review, it would be good practice to beta test the app
for any possibly new bugs.

**For exampel:** a common error that many people find at this stage is with the push notifications. 
As this requires a certificate of its own, the first step should be to verify that the certificate is valid and that you have handled the distribution part of this testing stage correctly.

In terms of beta testing, the two main choices are:

#### TestFlight
TestFlight can be considered the 'App Store' for beta testing your apps. 
It is considered its own 'app market' and as the developer(s), you can decide whether to release your app for public testing, or keep it internal for select testers. This makes use of App Store connect, which eases the process of uploading your apps onto the App Store. 
From there, you will be able to submit your app to both TestFlight and the App Store if you'd like. 
You should also make note of the fact that submitting an app onto TestFlight will also go through a review process just like the App Store, albeit with more lenient standards which could result in a quicker review time.

#### Ad-Hoc
Ad-Hoc allows you to distribute your app to a limited number (100) of registered devices. 
Unlike TestFlight, this cannot release it for 'public testing' to all beta testers, so you would have to register the devices you wish to use in the devices section on the Apple Developer Page. This means that you would have to register their device first by entering it's UDID (Unique Device Identifier) onto the App Developer page. 

- This can be found by plugging in your iPhone to your MacBook, going onto Xcode, then clicking Window tab to Devices and Simulators. 
From there you can select your iPhone and copy its UDID (make sure to include the '-' that is found after the 8th character).

The benefit of using Ad hoc is that you would not need the app to be reviewed before distributing it out for testing. This means that you would be able to get your app to your testers immediately and possibly avoid getting the app rejected during the review process.

#### Distribution Process
After your generate all your needed certificates, you would then need to generate your Provisioning Profile, selecting the app you wish to use as well as all the devices you want to access it. 

You would then proceed to complete the rest of the fields on the provisioning profile page and download the profile to import onto Xcode to build the app.

Now you can decide how you wouild like distribute the app, where you can choose between the following options for distribution:
- App Store Connect (TestFlight/App Store)
- Ad Hoc
- Enterprise
- Development

Should you choose TestFlight in App Store Connect, your process would be simple and you can follow further directions online on how your testers can download your app on the TestFligth app market. 
Following the steps would allow you to easily upload your .ipa onto App Store Connect where you can manage your next steps online.

If you chose to use Ad Hoc, however, you would build a .ipa which you can send to your testers to install onto their device or device simulator on Xcode.

For further clarification about App Distribution, you can refer to these **Apple's Documentation** links below:

- [Distributing your app for beta testing and releases](https://developer.apple.com/documentation/xcode/distributing-your-app-for-beta-testing-and-releases)

- [Distributing your app to registered devices](https://developer.apple.com/documentation/xcode/distributing-your-app-to-registered-devices)

### App Store Submission 
There will be a full review process, which should be completed within 24 hours according to Apple, but it may take longer depending on your app.
In comparison to TestFlight's review process, since this would go to the official App Store, they will be enforcing stricter standards.

It would be good practice to continously develop your app keeping proper safety and privacy guidelines in mind, but in case you would like to assess on your own prior to submission, you could refer to these specific review guidlines:

- [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)

- [Human Interface Design Guidelines](https://developer.apple.com/design/human-interface-guidelines/)

- [Guidelines for Using Apple Trademarks and Copyrights](https://www.apple.com/legal/intellectual-property/guidelinesfor3rdparties.html)


If you used TestFlight for beta testing earlier, you should be familiar with this process as it is very similar for the App Store Review. If you used Ad hoc to test, then you may refer to the steps mentioned in the TestFlight process in getting the .ipa uploaded onto App Store Connect.

Now you are ready to submit your app for review in App Store Connect. 
This is what you can consider to be your dashboard in managing your apps. 
You are able to view sales, access app analytics, as well as submit your app for App Store Review.

After selecting the app to 'Add for Review' you must also provide:

- Information to provide App Store Reviewers:
    - Contact information
    - Notes/Documentation
    - Demo Account (if applicable)
- Describtion and Features
- Any extra information that pertains to how you would like your app to be presented
    - App banners, app promotions, etc.

Congratulations! From this point on, all you have to do is sit back and wait for the review decision to come out. Make sure to make the appropriate changes if they were requested or download your app from the official App Store if it was approved!

For further information on the App Review process, please consult Apple's [App Review Docs](https://developer.apple.com/app-store/review/#:~:text=On%20average%2C%2090%25%20of%20submissions,app%20for%20iPhone%20and%20iPad.). This contains all the steps, common issues, as well as contact information if you need further help in the app review process.
