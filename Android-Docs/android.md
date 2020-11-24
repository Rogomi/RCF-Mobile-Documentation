[Back](../index.md)

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

- **RetrofitBuilder** - a class which contains the network settings (i.e timeout span).

  ##### Methods

  - `buildAuth(appPreferences: AppPreferences): Retrofit`
  - `build(): Retrofit`
  - `build(appPreferences: AppPreferences): Retrofit`

- **AppPreferences** - handles the storing of simple data such as user name, if user login, etc.
  ##### Methods
  -
- **ApiService** - a class which contains the endpoints call. what kind of httprequest, the parameters to be passed, response type.
- **ApiEndpoint** - a class which contains the constant endpoint strings

#### Activities/Fragments

- **SplashActivity** - handles the Splash page
- **LoginActivity** - handles the Login Page
  ##### Methods
  - `printKeyHash()`
  - `signIn()`
  - `initFacebookLogin()`
  - `initGoogleLogin()`
  - `signInGoogle()`
  - `handleSignInResult(completedTask: Task<GoogleSignInAccount>)`
- **RegistrationActivity** - handles the registration
  ##### Methods
  - `initPresenter()`
  - `saveInformation()`
  - `onRegistered()`
  - `onProvinces(provinces: List<Province>)`
  - `onCities(cities: List<City>)`
- **ForgotPasswordActivity** - handles the forgot password
  ##### Methods
  - `initLayout()`
  - `resetPassword()`
  - `onResetPassword()`
- **MainActivity** - container of all fragments after login
  ##### Methods
  - `initNavigation()`
  - `replaceFragment(fragment: BaseFragment)`
  - `addFragment(fragment: BaseFragment)`
  - `addFragmentNoBackStack(fragment: BaseFragment)`
- **ProfileFragment** - handles the profile page
  ##### Methods
  - `initProfile()`
  - `initActions()`
  - `shareApp()`
- **WalletFragment** - handles the wallet page
  ##### Methods
  - `initContainers()`
  - `initFields()`
  - `loginWallet()`
  - `onWalletLoggedIn(walletLoginData: WalletLoginData)`
  - `onGetWalletBalance(walletBalanceData: WalletBalanceData)`
  - `onLock()`
  - `showTransactions()`
  - `onRenderTransactions(transactions: List<Transaction>)`
- **LoanDashboardFragment** - handles the dashboard
  ##### Methods
  - `initContainers()`
  - `showTransactions()`
  - `onRenderLoans(data: List<LoanResponse>?)`
  - `onRenderLoanCredit(loanCredit: LoanCredit)`
  - `getActiveLoans(): List<LoanResponse>`
  - `getOtherLoans(): List<LoanResponse>`
  - `getDueLoans(): List<LoanResponse>`
  - `createDataSeries(currentValue: Float, maxValue: Float)`
- **FundsFragment** - handles the wallet transactions
- **CashAdvanceHrisAdapter** -
- **CashAdvanceHrisAllFragment** -
  ##### Methods
  - `onSearch(keyword: String)`
  - `initCashAdvance()`
  - `onRenderCashAdvances(cashAdvanceList: List<CashAdvance>)`
  - `onSelectedCashAdvance(cashAdvance: CashAdvance)`
- **CashAdvanceHrisDashboardFragment** -
  ##### Methods
  - `initEmployeeFragment()`
  - `initCashAdvance()`
  - `onRenderCashAdvances(cashAdvances: List<CashAdvance>)`
  - `onSelectedCashAdvance(cashAdvance: CashAdvance)`
- **CashAdvanceHrisPresenter** -
  ##### Methods
  - `getCashAdvance()`
- **CashAdvanceDetailsHrisFragment** -
  ##### Methods
  - `initCashAdvances()`
- **CashAdvanceDetailsPresenter** -
  ##### Methods
  - `approveCashAdvance(id: Int)`
  - `declineCashAdvance(id: Int)`
- **EmployeeHrisDashboardFragment** -
  ##### Methods
  - `onRenderEmployees(employees: List<Employee>)`
  - `getTotalEmployeeSize(): Int`
- **EmployeeHrisFragment** -
  ##### Methods
  - `initEmployee()`
  - `onSearch(keyword: String)`
  - `onRenderEmployees(employees: List<Employee>)`
- **EmployeeHrisPresenter** -
  ##### Methods
  - `getEmployee()`
- **LeaveHrisAllFragment** -
  ##### Methods
  - `onSearch(fromDate: Date?, toDate: Date?)`
  - `onSelectedLeave(leave: Leave)`
- **LeaveHrisDashboardFragment** -
  ##### Methods
  - `initLeave()`
  - `onRenderLeaves(leaves: List<Leave>)`
  - `onSelectedLeave(leave: Leave)`
- **LeaveDetailsHrisFragment** -
  ##### Methods
  - `initLeaves()`
- **OvertimeHrisAllFragment** -
  ##### Methods
  - `onSearch(fromDate: Date?, toDate: Date?)`
  - `onSelectedOvertime(overtime: Overtime)`
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
- **PayslipsPresenter** -
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
- **TimesheetHrisPresenter** -
  ##### Methods
  - `getTimesheets()`
  - `getTimesheetsByEmployee(employeeCode : String)`
