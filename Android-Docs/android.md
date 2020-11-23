# Right Choice Finance

## Technical Documentation

### GETTING STARTED

Right Choice Finance Android is using Android Studio. This project uses Kotlin as the Programming Language, Android Studio Layout Editor for the Interface, and Gradle for connecting different Third-Party Libraries. The target and compile SDK Version is 29 with a minimum SDK version of 26.
For more information on the IDE and system requirements to enable you to work on the source code, it is available [here](https://developer.android.com/)

### INSTALLATION AND DEVELOPMENT

In order to start the development, first, you need to start Android Studio. Import the RCD-Mobile Android project and then wait for the build to finish.

### PROGRAMMING LANGUAGE

RCF Mobile Android uses Kotlin for development

### MINIMUM VERSION

RCF Mobile can run on Android Systems with minimum SDK version 26. It may encounter multiple issues on lower SDK versions.

### APPLICATION ID

ph.rightchoicefinance.app

### WEB API

Test URL: http://testapi.rcf.ph/api/v1/clients/login \
Prod URL: https://api.rightchoicefinance.ph/api/v1/clients/login

### DEBUGGING

We use Android Virtual Device in Android Studio in order to test the Native Apps in different screen sizes and SDK Versions.

### THIRD-PARTY LIBRARIES

Most of the third-party libraries are integrated using Gradle. They can be added by searching library names found in the Dependencies tab in the Project Structure window.

#### Important Libraries

- Firebase/Crashlytics - used to report crashes from Users that are not encountered during development and debugging.
- Coroutine - is a concurrency design pattern that you can use on Android to simplify code that executes asynchronously.
- Retrofit - is type-safe REST client for Android and Java which aims to make it easier to consume RESTful web services.

### IMPORTANT CLASSES

#### Main Utilities

- RetrofitBuilder - a class which contains the network settings (i.e timeout span).
- AppPreferences - handles the storing of simple data such as user name, if user login, etc.
- ApiService - a class which contains the endpoints call. what kind of httprequest, the parameters to be passed, response type.
- ApiEndpoint - a class which contains the constant endpoint strings

#### Activities/Fragments

- SplashActivity - handles the Splash page
- LoginActivity - handles the Login Page
- RegistrationActivity - handles the registration
- ForgotPasswordActivity - handles the forgot password
- MainActivity - container of all fragments after login
- ProfileFragment - handles the profile page
- WalletFragment - handles the wallet page
- LoanDashboardFragment - handles the dashboard
- FundsFragment - handles the wallet transactions
