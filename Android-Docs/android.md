[Back](../index.md)

# Right Choice Finance Android

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

- **Firebase/Crashlytics** - used to report crashes from Users that are not encountered during development and debugging.
- **Coroutine** - is a concurrency design pattern that you can use on Android to simplify code that executes asynchronously.
- **Retrofit** - is type-safe REST client for Android and Java which aims to make it easier to consume RESTful web services.

### IMPORTANT CLASSES

#### Main Utilities

- **RetrofitBuilder** - a class which contains the network settings (i.e timeout span).
- **AppPreferences** - handles the storing of simple data such as user name, if user login, etc.
- **ApiService** - a class which contains the endpoints call. what kind of httprequest, the parameters to be passed, response type.
- **ApiEndpoint** - a class which contains the constant endpoint strings

#### Activities/Fragments

- **SplashActivity** - handles the Splash page
- **LoginActivity** - handles the Login Page
  ##### Methods
  - `signIn()` - trigger when tap the sign in button
  - `initFacebookLogin()` - initialize the Facebook login
  - `initGoogleLogin()` - initialize Google sign in
  - `signInGoogle()` - trigger when sign in to google
  - `handleSignInResult(completedTask: Task<GoogleSignInAccount>)` - called when receive response from google sign in
- **RegistrationActivity** - handles the registration
  ##### Methods
  - `saveInformation() ` - saves information to serve
  - `onRegistered() ` - called when successfully saved to serve
  - `onProvinces(provinces: List<Province>) ` - call when receive response when getting the list of province from the server
  - `onCities(cities: List<City>) ` - call when receive response when getting the list of city from the server
- **ForgotPasswordActivity** - handles the forgot password
  ##### Methods
  - `resetPassword() ` - request to reset password to the server
  - `onResetPassword() ` - called when successfully reset the password
- **MainActivity** - container of all fragments after login
  ##### Methods
  - `initNavigation() ` - initialize the list of menus
  - `replaceFragment(fragment: BaseFragment) ` - when replacing a fragment in the container for navigation
  - `addFragment(fragment: BaseFragment) ` - when adding a fragment in the container for navigation
  - `addFragmentNoBackStack(fragment: BaseFragment) ` - when adding a fragment with back stack in the container for navigation
- **ProfileFragment** - handles the profile page
  ##### Methods
  - `initProfile() ` - populate all information in profile page
  - `shareApp() ` - trigger when sharing the app
- **WalletFragment** - handles the wallet page
  ##### Methods
  - `loginWallet() ` - trigger when login to wallet
  - `onWalletLoggedIn(walletLoginData: WalletLoginData) ` - called when successfully logged in to wallet
  - `onGetWalletBalance(walletBalanceData: WalletBalanceData) ` - display the wallet balance from the server
  - `onLock() ` - lock the wallet page
  - `showTransactions() ` - call the list of transactions to the server
  - `onRenderTransactions(transactions: List<Transaction>) ` - display the list of transaction from the server
- **LoanDashboardFragment** - handles the dashboard
  ##### Methods
  - `showTransactions() ` - show all transactions
  - `onRenderLoans(data: List<LoanResponse>?) ` - render all types of loans list
  - `onRenderLoanCredit(loanCredit: LoanCredit) ` - display the available and limit credit
  - `getActiveLoans(): List<LoanResponse> ` - filter all the active loans
  - `getOtherLoans(): List<LoanResponse> ` - filter all the other loans
  - `getDueLoans(): List<LoanResponse> ` - filter all due loans
  - `createDataSeries(currentValue: Float, maxValue: Float) ` - initialize the UI progress circle
- **CashAdvanceHrisAllFragment** - handles the list of all cash advances (HR Admin)
  ##### Methods
  - `onSearch(keyword: String) ` - filter the list of cash advance
  - `initCashAdvance() ` - initialize the list of cash advances
  - `onRenderCashAdvances(cashAdvanceList: List<CashAdvance>) ` - display the list of cash advances
  - `onSelectedCashAdvance(cashAdvance: CashAdvance) ` - show the details of cash advance
- **CashAdvanceHrisDashboardFragment** - handles the cash advances dashboard(HR Admin)
  ##### Methods
  - `initEmployeeFragment() ` - show the list of employees in the header
  - `initCashAdvance() ` - initialize the list of cash advances
  - `onRenderCashAdvances(cashAdvanceList: List<CashAdvance>) ` - display the list of cash advances
  - `onSelectedCashAdvance(cashAdvance: CashAdvance) ` - show the details of cash advance
- **CashAdvanceDetailsHrisFragment** - - handles the display of cash advance detail(HR Admin)
  ##### Methods
  - `initCashAdvances() ` - display the details of cash advance
  - `approveCashAdvance(id: Int) ` - server call to approve the cash advance
  - `declineCashAdvance(id: Int) ` - server call to decline the cash advance
- **EmployeeHrisDashboardFragment** - handles the display of employees in the dashboard (HR Admin)
  ##### Methods
  - `onRenderEmployees(employees: List<Employee>) ` - show the list of employees
  - `getTotalEmployeeSize(): Int ` - get the size of employees
- **EmployeeHrisFragment** - handles the display of all employees (HR Admin)
  ##### Methods
  - `initEmployee() ` - prepare the adapter and recyclerview
  - `onSearch(keyword: String) ` - filter the list of employees
  - `onRenderEmployees(employees: List<Employee>) ` - display the list of employees
- **LeaveHrisAllFragment** - display the list of all leave applications
  ##### Methods
  - `onSearch(fromDate: Date?, toDate: Date?) ` - filter the list by date range
  - `onSelectedLeave(leave: Leave) ` - show the details of leave application
  - `onRenderLeaves(leaves: List<Leave>) ` - show the list of leave application
- **LeaveHrisDashboardFragment** -
  ##### Methods
  - `initLeave() ` - initialize the leave list adapter and recyclerview
  - `onSelectedLeave(leave: Leave) ` - show the details of leave application
  - `onRenderLeaves(leaves: List<Leave>) ` - show the list of leave application
- **LeaveDetailsHrisFragment** - display the details of leave application
  ##### Methods
  - `initLeaves() ` - show the details of leave application
- **OvertimeHrisAllFragment** - display the list of overtime requests (HR Admin)
  ##### Methods
  - `onSearch(fromDate: Date?, toDate: Date?) ` - filter the list by date range
  - `onSelectedOvertime(overtime: Overtime) ` - to show the details of overtime request
- **OvertimeHrisDashboardFragment** - handles the Overtime request dashboard (HR Admin)
  ##### Methods
  - `onRenderOvertimes(overtimes: List<Overtime>) ` - display the list of overtime requests
  - `onSelectedOvertime(overtime: Overtime) ` - to show the details of overtime request
- **OvertimeDetailsHrisFragment** - handles the overtime details page (HR Admin)
  ##### Methods
  - `initOvertimes() ` - show the details of overtime
- **PayslipDetailsHrisFragment** - handles the display of payslip details
  ##### Methods
  - `initPayslips() ` - show payslip details
- **PayslipsHrisAllFragment** - display all the list of payslips
  ##### Methods
  - `onSearch(keyword: String) ` - filter the list of payslip
  - `initPayslips() ` - initialize adpater and recyclerview
  - `onRenderPayslips(payslips: List<Payslip>) ` - display the list of payslips
  - `onSelectedPayslip(payslips: Payslip) ` - to show payslip details
- **TimesheetDetailsHrisFragment** - handles the display of timelog details
  ##### Methods
  - `initTimelogs() ` - populate the details of timesheet
- **TimesheetHrisAllFragment** - handles the listing of all timelogs (HR Admin)
  ##### Methods
  - `onSearch(keyword: String) ` - filter the list of timelogs
  - `onRenderTimesheets(timesheets: List<TimeLog>) ` - render the list of timesheets
  - `onSelectedTimesheet(timesheet: TimeLog) ` - to display the list of selected timesheet
- **BankListFragment** - handles the display of bank list
  ##### Methods
  - `initBanks() ` - initialize adapter and recyclerview
  - `onSearch(keyword: String) ` - filter the list of banks
  - `onRenderBanks(banks: List<Bank>) ` - render the list of bank
  - `onSelectedBank(bank: Bank) ` - trigger when selecting a bank
- **BillerListFragment** - handles the list of billers
  ##### Methods
  - `initBillers() ` - initialize the adapter and recyclerview
  - `onSearch(keyword: String) ` - filter the list of billers
  - `onRenderBillers(billers: List<Biller>) ` - render the list of billers
  - `onSelectedBiller(biller: Biller) ` - trigger when selecting a biller
- **CashAdvanceFragment** - handle the cash advance form
  ##### Methods
  - `onApplyCashAdvance() ` - submit the application to server
- **AddContactFragment** - handle the adding of contact
  ##### Methods
  - `checkValidEmail() ` - validate the inputted email
  - `onAddContact() ` - trigger when successfully added the contact
- **RecipientsListFragment** - handles the list of recipients
  ##### Methods
  - `initRecipients() ` - initialize the adapter and recyclerview
  - `onRenderWalletContacts(walletContacts: List<WalletContact>) ` - list all wallet contacts
  - `onSelectedRecipient(walletContact: WalletContact) ` - trigger when selecting a contact
- **SendFundFragment** - handles the send fund page

  ##### Methods

  - `addField() ` - trigger when adding multiple recipients

- **AddFundsFragment** - handles the add fund page
  ##### Methods
  - `openUrl(url: String) ` - load the webview of adding fund
- **InvestmentsFragment** - handles the investments page
  ##### Methods
  - `checkWallet() ` - check if wallet is active
  - `initInvestments() ` - initailize adapter and recyclerview
  - `onGetInvestments(investments: List<Investment>) ` - display the list of investments
- **NewInvestmentFragment** - handles the investment form
  ##### Methods
  - `checkApplication() ` - display the application details
  - `onApplyInvestmentRequest() ` - submit application to server
- **ApplyLeaveFragment** - handles apply leave form
  ##### Methods
  - `onApplyLeaveRequest() ` - submit application to server
- **LoanSignFragment** - handles the loan signature form
  ##### Methods
  - `submit() ` - submit the loan application
  - `onLoanActivated() ` - receive the response of the application from the server
- **DocumentFragment** - handles upload documents form
  ##### Methods
  - `initFileField(file: File) ` - initialize form
  - `getDocumentInputs() : DocumentRequest ` - get the documents input to be sent to server
  - `openFileExplorer() ` - show file explorer
  - `showPictureDialog() ` - show dialog chooser
  - `choosePhotoFromGallery() ` - open photo gallery
  - `takePhotoFromCamera() ` - open camera
  - `saveImage(myBitmap: Bitmap): File? ` - save image to memory
- **LoanDocumentFragment** - handles the list of documents to be uploaded

  ##### Methods

  - `save() ` - save the documents to sever
  - `addDocumentField() ` - handles the dynamic adding of document fragments

  ### DIAGRAM

  ![Application Architecture](dia.png 'Application Architecture')

  #### **Model**

  In an application with a good layered architecture, this model would only be the gateway to the domain layer or business logic. See it as the provider of the data we want to display in the view. Model’s responsibilities include using APIs, caching data, managing databases and so on.

  #### **View**

  The View, usually implemented by an Activity, will contain a reference to the presenter. The only thing that the view will do is to call a method from the Presenter every time there is an interface action.

  #### **Presenter**

  The Presenter is responsible to act as the middle man between View and Model. It retrieves data from the Model and returns it formatted to the View. But unlike the typical MVC, it also decides what happens when you interact with the View.
