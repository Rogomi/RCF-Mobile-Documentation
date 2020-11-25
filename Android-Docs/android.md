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
  - `signIn() - trigger when tap the sign in button `
  - `initFacebookLogin() - initialize the facebook login`
  - `initGoogleLogin() - initialize google sign in`
  - `signInGoogle() - trigger when sign in to google`
  - `handleSignInResult(completedTask: Task<GoogleSignInAccount>) - called when receive response from google sign in `
- **RegistrationActivity** - handles the registration
  ##### Methods
  - `saveInformation() - saves information to serve`
  - `onRegistered() - called when successfully saved to serve`
  - `onProvinces(provinces: List<Province>) - call when receive response when getting the list of province from the server`
  - `onCities(cities: List<City>) -  call when receive response when getting the list of city from the server`
- **ForgotPasswordActivity** - handles the forgot password
  ##### Methods
  - `resetPassword() - request to reset password to the server`
  - `onResetPassword() - called when successfully reset the password`
- **MainActivity** - container of all fragments after login
  ##### Methods
  - `initNavigation() - initialize the list of menus`
  - `replaceFragment(fragment: BaseFragment) - when replacing a fragment in the container for navigation`
  - `addFragment(fragment: BaseFragment) - when adding a fragment in the container for navigation`
  - `addFragmentNoBackStack(fragment: BaseFragment) - when adding a fragment with back stack in the container for navigation`
- **ProfileFragment** - handles the profile page
  ##### Methods
  - `initProfile() - populate all information in profile page`
  - `shareApp() - trigger when sharing the app`
- **WalletFragment** - handles the wallet page
  ##### Methods
  - `loginWallet() - trigger when login to wallet`
  - `onWalletLoggedIn(walletLoginData: WalletLoginData) - called when successfully logged in to wallet`
  - `onGetWalletBalance(walletBalanceData: WalletBalanceData) - display the wallet balance from the server`
  - `onLock() - lock the wallet page`
  - `showTransactions() - call the list of transactions to the server`
  - `onRenderTransactions(transactions: List<Transaction>) - display the list of transaction from the server`
- **LoanDashboardFragment** - handles the dashboard
  ##### Methods
  - `showTransactions() - show all transactions`
  - `onRenderLoans(data: List<LoanResponse>?) - render all types of loans list `
  - `onRenderLoanCredit(loanCredit: LoanCredit) - display the available and limit credit`
  - `getActiveLoans(): List<LoanResponse> - filter all the active loans`
  - `getOtherLoans(): List<LoanResponse> - filter all the other loans`
  - `getDueLoans(): List<LoanResponse> - filter all due loans`
  - `createDataSeries(currentValue: Float, maxValue: Float) - initialize the UI progress circle`
- **CashAdvanceHrisAllFragment** - handles the list of all cash advances (HR Admin)
  ##### Methods
  - `onSearch(keyword: String) - filter the list of cash advance`
  - `initCashAdvance() - initialize the list of cash advances`
  - `onRenderCashAdvances(cashAdvanceList: List<CashAdvance>) - display the list of cash advances`
  - `onSelectedCashAdvance(cashAdvance: CashAdvance) - show the details of cash advance`
- **CashAdvanceHrisDashboardFragment** - handles the cash advances dashboard(HR Admin) 
  ##### Methods
  - `initEmployeeFragment() - show the list of employees in the header`
  - `initCashAdvance() - initialize the list of cash advances`
  - `onRenderCashAdvances(cashAdvanceList: List<CashAdvance>) - display the list of cash advances`
  - `onSelectedCashAdvance(cashAdvance: CashAdvance) - show the details of cash advance`
- **CashAdvanceDetailsHrisFragment** - - handles the display of cash advance detail(HR Admin) 
  ##### Methods
  - `initCashAdvances() - display the details of cash advance`
  - `approveCashAdvance(id: Int) - server call to approve the cash advance`
  - `declineCashAdvance(id: Int) - server call to decline the cash advance`
- **EmployeeHrisDashboardFragment** - handles the display of employees in the dashboard (HR Admin)
  ##### Methods
  - `onRenderEmployees(employees: List<Employee>) - show the list of employees`
  - `getTotalEmployeeSize(): Int - get the size of employees`
- **EmployeeHrisFragment** - handles the display of all employees (HR Admin)
  ##### Methods
  - `initEmployee() - prepare the adapter and recyclerview`
  - `onSearch(keyword: String) - filter the list of employees`
  - `onRenderEmployees(employees: List<Employee>) - display the list of employees`
- **LeaveHrisAllFragment** - display the list of all leave applications
  ##### Methods
  - `onSearch(fromDate: Date?, toDate: Date?) - filter the list by date range`
  - `onSelectedLeave(leave: Leave) - show the details of leave application`
  - `onRenderLeaves(leaves: List<Leave>) - show the list of leave application`
- **LeaveHrisDashboardFragment** -
  ##### Methods
  - `initLeave() - initialize the leave list adapter and recyclerview`
  - `onSelectedLeave(leave: Leave) - show the details of leave application`
  - `onRenderLeaves(leaves: List<Leave>) - show the list of leave application`
- **LeaveDetailsHrisFragment** - display the details of leave application
  ##### Methods
  - `initLeaves() - show the details of leave application`
- **OvertimeHrisAllFragment** - display the list of overtime requests (HR Admin)
  ##### Methods
  - `onSearch(fromDate: Date?, toDate: Date?) - filter the list by date range`
  - `onSelectedOvertime(overtime: Overtime) - to show the details of overtime request`
- **OvertimeHrisDashboardFragment** -
  ##### Methods
  - `onRenderOvertimes(overtimes: List<Overtime>)`
  - `onSelectedOvertime(overtime: Overtime)s`
- **OvertimeDetailsHrisFragment** -
  ##### Methods
  - `initOvertimes()`
- **PayslipDetailsHrisFragment** -
  ##### Methods
  - `initPayslips()`
- **PayslipDetailsHrisFragment** -
  ##### Methods
  - `initPayslips()`
- **PayslipsHrisAllFragment** -
  ##### Methods
  - `onSearch(keyword: String)`
  - `initPayslips()`
  - `onRenderPayslips(payslips: List<Payslip>)`
  - `onSelectedPayslip(payslips: Payslip)`
  ##### Methods
  - `getPayslips()`
  - `getPayslipsByEmployee(employeeCode : String)`
- **TimesheetDetailsHrisFragment** -
  ##### Methods
  - `initTimelogs()`
- **TimesheetHrisAllFragment** -
  ##### Methods
  - `onSearch(keyword: String)`
  - `onRenderTimesheets(timesheets: List<TimeLog>)`
  - `onSelectedTimesheet(timesheet: TimeLog)`
- **BankListFragment** -
  ##### Methods
  - `initBanks()`
  - `onSearch(keyword: String)`
  - `onRenderBanks(banks: List<Bank>)`
  - `onSelectedBank(bank: Bank)`
- **BillerListFragment** -
  ##### Methods
  - `initBillers()`
  - `onSearch(keyword: String)`
  - `onRenderBillers(billers: List<Biller>)`
  - `onSelectedBiller(biller: Biller)`
- **CashAdvanceFragment** -
  ##### Methods
  - `onApplyCashAdvance()`
- **AddContactFragment** -
  ##### Methods
  - `checkValidEmail()`
  - `onAddContact()`
- **RecipientsListFragment** -
  ##### Methods
  - `initRecipients()`
  - `onRenderWalletContacts(walletContacts: List<WalletContact>)`
  - `onSelectedRecipient(walletContact: WalletContact)`
- **SendFundFragment** -
  ##### Methods
  - `addField()`
- **SendIndividualFundFragment** -
  ##### Methods
  - `getValueRequest(): SendFundRequest`
- **AddFundsFragment** -
  ##### Methods
  - `openUrl(url: String)`
- **InvestmentsFragment** -
  ##### Methods
  - `checkWallet()`
  - `initInvestments()`
  - `onGetInvestments(investments: List<Investment>)`
- **NewInvestmentFragment** -
  ##### Methods
  - `checkApplication()`
  - `onApplyInvestmentRequest()`
- **ApplyLeaveFragment** -
  ##### Methods
  - `onApplyLeaveRequest()`
- **LoanSignFragment** -
  ##### Methods
  - `submit()`
  - `onLoanActivated()`
- **DocumentFragment** -
  ##### Methods
  - `initFileField(file: File)`
  - `getDocumentInputs() : DocumentRequest`
  - `openFileExplorer()`
  - `showPictureDialog()`
  - `choosePhotoFromGallery()`
  - `takePhotoFromCamera()`
  - `saveImage(myBitmap: Bitmap): File?`
- **LoanDocumentFragment** -
  ##### Methods
  - `save()`
  - `addDocumentField()`
