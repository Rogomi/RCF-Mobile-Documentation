[Back](../index.md)
## Right Choice Finance iOS
### Technical Documentation


#### GETTING STARTED

Right Choice Finance iOS requires Xcode 11.0 and above for development. This project uses Swift 5 as the Programming Language, Storyboard for the Interface and CocoaPods for Third Party Libraries. The current Xcode version used for development is 11.5. The minimum iOS Version required is iOS 12.0


#### INSTALLATION AND DEVELOPMENT

In order to start with the development, first, you will need an Apple account for development. It must be under the team **Rogomi, Inc.**. Then, open the **RightChoiceFinance-iOS.xcworkspace** under the repository root directory. If possible, do a **pods repo update** in order to avoid missing library errors.


#### PROGRAMMING LANGUAGE

RCF iOS uses the latest Swift version, Swift 5, for development.


#### MINIMUM VERSION

RCF iOS requires devices with at least iOS 12.0


#### APPLICATION ID

ph.rightchoicefinance.app


#### DEBUGGING

We use a few debugging tools to test RCF’s functionalities.
For the Native App, we use Xcode's debugging console to create breakpoints and test variables, API responses, and identify null objects which sometimes causes the crash.
To test the API before integrating for app usage, we use [Postman](https://www.getpostman.com/). Postman is a very reliable REST API tool. We can test different HTTP Methods especially POST, PATCH, PUT, DELETE and GET. We can also add header variables to test SSO and token authentications.
We also use iOS Simulator in order to test the apps in different screen sizes and iOS Versions.


#### WEB API

[Test URL](http://testapi.rcf.ph/api/v1/clients)  
[Production URL](https://api.rightchoicefinance.ph/api/v1/clients)

#### THIRD PARTY LIBRARIES
Most of the third party libraries are installed using CocoaPods. They can be added by searching library names found in [https://cocoapods.org/](https://cocoapods.org/), inserting them in the Podfile and running the pod install command in the Terminal.

#### Important Libraries

**Alamofire** - used to handle app communication with the Web API.  
**SwiftyJSON** - used to handle JSON objects and have the fields be easily checked for nulls before converting to swift objects.  
**SwiftDate** - used to handle Dates to have an ease of adding days and comparing dates.  
**ObjectMapper** - used alongside SwiftyJSON in order to convert JSON objects to swift objects.  
**Reachability** - used to check internet connection before loading the API and prevent users from further actions.  
**Firebase/Analytics** - a mobile SDK library for Google Analytics platform used to analyze usage data from users.  
**Firebase/Crashlytics** - used to report crashes from Users that are not encountered during development and debugging.  
**SwiftSignatureView** - used to implement signing on loan applications  
**Charts** - used to implement displaying of credit status on loan dashboard  
BiometricAuthentication - used to allow user to log in using Touch ID or Face ID  
**SAMKeychain** - used to store user’s device ID to identify when logging in using biometrics  
QRCodeReader.swift - used to scan QR codes from other user when sending funds  


#### SSO Libraries

**FBSDKLoginKit** - used for authentication using Facebook accounts.  
**GoogleSignIn** - used for authentication using Google accounts.


#### UI Libraries

**IBAnimatable** - used to customize UI Views to match the designs more accurately.  
**MBProgressHUD** - used to indicate that the items are loading and prevent user interaction until the items are loaded.  
**IQKeyboardManager** - used to implement Keyboard avoiding when entering data into text-fields that are covered by the iOS On-screen Keyboard.  
**SDWebImage** - used to set images on UIImageViews using URLs.  
**SDWebImagePDFCoder** - used to set PDF images on UIImageViews using URLs. 

#### ACTIVITIES AND CONTROLLERS
**Core Classes**    
- **AppDelegate** - contains handlers for application states for devices with iOS 12 and below. It also handles deep linking to direct users to specific screens depending on the URL specified.  
- **RCFViewDelegate** - most of the view controllers in the app conforms to this protocol and it contains global functions that are accessible throughout the development and avoid redundant functionalities.  
- **PickerDelegate** - view controllers that conforms to this protocol are able open pickers with specified list of items for selection or date.  
- **HUDDelegate** - view controllers that conforms to this protocol are able to show HUDs to indicate that a request is being made to the Web API.  
- **RCFInterface** - contains functions that manage the app sessions and checks for specific variables saved on UserDefaults.  
- **RCFWeb** - contains functions that enable the app to communicate with the web API.  
- **RCFWeb.Endpoint** - a customized enum type that enlists the routes interfaced from the web API and makes use of Alamofire to connect. It dynamically loads the endpoints with set parameters, methods and headers.  
- **Models Swift Files** - contains the model classes with their functions that returns different values and statements to be used as output for views.
 
 
**View Controllers**

- **RCFViewController** - child view controllers will inherit this class to avoid code rewrites when the views are loading or about to appear. It also contains global functions to be reused throughout the development.  

- **AppTabBarController** - contains functions to handle the startup operations.  
SignInViewController - contains functions that handles user’s authentication. It has different ways to login besides using email & password, such as Logging in with Facebook, Google or Apple ID. It also handles logins using TouchID/FaceID.  
  ##### Methods
  - `reloadTabs()`
  - `openAuthVC(animated: Bool = true)`
  - `tabBarController(_ tabBarController: UITabBarController, shouldSelect viewController: UIViewController) -> Bool`
  - `triggerWillSwitchEventOnLoansTab()`
  - `triggerWillSwitchEventOnInvestmentTab()`

- **SignUpViewController** - contains functions that handles user’s registration. It contains the form fields where the user can fill their information up.  
  ##### Methods
  - `signUp()`
  - `validate()`
  - `getEmptyMessage()`
  - `getEmptyError()`
  - `showTNCVC(withTitle title: String, content: String)()`
  - `refreshSelectionFields()`
  - `refreshEyecons()`
  - `addTapGestureToSelectionFields()`
  - `textFieldShouldBeginEditing()`
  - `textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String)`

- **TNCContainerViewController** - a view controller where the user can read the Terms of Usage/Privacy Policy upon signing up.  
  ##### Methods
  - `addOverlay()`
  - `removeOverlay()`

- **VerifyEmailViewController** - contains a message that is indicated after the user signs up. The user can also resend the verification email using this page.  
  ##### Methods
  - `didTapResendLabel(_ sender: Any)`
  - `didTapBackToLoginButton(_ sender: Any)`

- **ForgotPasswordViewController** - a view controller where the user can choose to reset their password. After inserting the email address, the app will connect with the Web API to send the reset password email to the user.  
  ##### Methods
  - `didTapResetPassword(_ sender: Any)`
  - `didTapBackToLoginButton(_ sender: Any)`

- **CheckInboxViewController** - contains a message that is indicated after the users use the Forgot Password feature.  
  ##### Methods
  - `didTapBackToLoginButton(_ sender: Any)`

- **WalletViewController** - contains functions where the user can unlock their wallet, check their balance, recent transactions, open specific features of the app like sending funds, withdrawing funds, paying bills and other options.  
  ##### Methods
  - `viewDidLayoutSubviews()`
  - `didUpdateWalletSession(_ sender: Any)`
  - `didRefreshDashboard(_ sender: Any)`
  - `didTapCreateWalletButton(_ sender: Any)`
  - `didTapUnlockWalletButton(_ sender: Any)`
  - `didTapYourTransactionsLabel(_ sender: Any)`
  - `didTapSeeMoreButton(_ sender: Any)`
  - `refreshOptionsCollection()`
  - `refreshTransactionsTable()`
  - `resetWalletValues()`
  - `updateWalletScreen()`
  - `updateWalletBalance()`
  - `updateTransactions()`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, heightForRowAt) -> CGFloat`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`
  - `collectionView(_, numberOfItemsInSection) -> Int`
  - `collectionView(_, cellForItemAt) -> UICollectionViewCell`
  - `collectionView(_, didSelectItemAt)`
  - `collectionView(_, layout, sizeForItemAt) -> CGSize`

- **AddFundsViewController** - a view controller that contains a form where the user can specify the amount and type of service to be used when adding funds.  
  ##### Methods
  - `getLabel()`
  - `didUpdateWalletSession(_ sender: Any)`
  - `openPINAlert(request: AddFundRequest, completion: @escaping(URL) -> Void)`
  - `textFieldShouldBeginEditing(_ textField: UITextField)`

- **AddFundsWebViewController** - a view controller that contains the web view where Dragon pay is opened and the user specifies their banks where to get the funds from.  
  ##### Methods
  - `didUpdateWalletSession(_ sender: Any)`
  - `webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping (WKNavigationActionPolicy) -> Void)`

- **SendFundsViewController** - a view controller where the user can send specific amount to other users  
  ##### Methods
  - `didUpdateWalletSession(_ sender: Any)`
  - `didTapAddRecipient(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `sendRequest(index: Int = 0, pin: String,  prerequests: [SendFundsPrerequest], reviewVC: TransactionReviewViewController, completion: @escaping TransactionClosure)`
  - `updateBalance()`
  - `addRecipientView(hidesRemoveButton: Bool = false)`
  - `refreshSeparators()`
  - `textFieldShouldBeginEditing(_ textField: UITextField)`

- **PayBillsViewController** - a view controller where the user can choose to pay bills on specific billers. 
  ##### Methods
  - `didUpdateWalletSession(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `updateBalance()`
  - `selectBiller(_ biller: Biller)`
  - `textFieldShouldBeginEditing(_ textField: UITextField)`
  
- **WithdrawViewController** - a view controller where the user can choose specific banks to transfer their money from their wallet account.  
  ##### Methods
  - `didUpdateWalletSession(_ sender: Any)`
  - `updateBalance()`
  - `loadBanks()`
  - `loadPurposes()`

- **RequestFundsViewController** - a view controller where the user can request funds from other users.  
  ##### Methods
  - `didUpdateWalletSession(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **MyCodeViewController** - a view controller where the user can see their QR Code image and be able to save or share it with other people.  
  ##### Methods
  - `didUpdateWalletSession(_ sender: Any)`
  - `didSaveImageToPhotoLibrary(_ image: UIImage, didFinishSavingWithError error: Error?, contextInfo: UnsafeRawPointer)`
  - `didTapSaveToDevice(_ sender: Any)`
  - `didTapShare(_ sender: Any)`
  - `refreshScreen()`

- **TransactionsViewController** - a view controller where the user can see the list of transactions they have made. It can also filter the list by date or specific categories.  
  ##### Methods
  - `getTransactionType()`
  - `updateTransactions()`
  - `getFilteredTransactions()`
  - `selectCategoryFilter(_ category: CategoryFilter)`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  
- **TransactionDetailsViewController** - a view controller where the user can see the details of the transaction they selected from the transactions list. It is also reused on specific transactions in the Wallet dashboard.  
  ##### Methods
  - `numberOfSections(in tableView: UITableView)`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`

- **TransactionReviewViewController** - a view controller where the user can see a preview of their transaction before they are carried out.  
  ##### Methods
  -  `openPINAlert(completion: @escaping TransactionClosure)`
  - `numberOfSections(in tableView: UITableView)`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `hideSeparator()`
  - `showSeparator()`
  - `restoreSeparatorSpace()`
  - `expandSeparatorSpaceForLastField()`
  - `expandSeparatorSpaceForFirstField()`

- **ContactListViewController** - a view where the user can choose specific contacts to send or request funds from.  
  ##### Methods
  -  `updateRecipients()`
  - `refreshRecipientsTable()`
  - `numberOfSections(in tableView: UITableView)`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `searchBar(_ searchBar: UISearchBar, textDidChange searchText: String)` 
  - `searchBarSearchButtonClicked(_ searchBar: UISearchBar)`
  - `didTapAddNewContactButton(_ sender: Any)`

- **AddContactViewController** - a view where the user can input another user’s information so they can add them as contact. 
  ##### Methods
  - `didTapNextButton(_ sender: Any)`

- **ScanQRContactViewController** - a view that contains a QR Scanner and is used when adding other users using their respective QR Codes as displayed from MyCodeViewController. 
  ##### Methods
  - `checkScanPermissions()`

- **CWStep1ViewController** - a view where the user can start their wallet activation. It contains fields that mostly hold the user’s personal information for wallet activation.  
  ##### Methods
  - `didTapNextButton(_ sender: Any)`
  - `refreshFields()`
  - `textFieldShouldBeginEditing(_ textField: UITextField)`

- **CWStep2ViewController** - a view where the user can input their contact numbers for wallet activation.  
  ##### Methods
  - `didTapNextButton(_ sender: Any)`
  - `refreshFields()`
  - `textFieldShouldBeginEditing(_ textField: UITextField)`

- **CWStep3ViewController** - a view where the user can input their address information for wallet activation.  
  ##### Methods
  - `didTapNextButton(_ sender: Any)`
  - `refreshFields()`
  - `textFieldShouldBeginEditing(_ textField: UITextField)`

- **CWStep4ViewController** - a view where the user can input their employment information for wallet activation.  
  ##### Methods
  - `didTapNextButton(_ sender: Any)`
  - `refreshFields()`
  - `textFieldShouldBeginEditing(_ textField: UITextField)`
  
- **CWStep5ViewController** - a view where the user can upload their documents for wallet activation.  
  ##### Methods
  - `didTapSubmitButton(_ sender: Any)`
  - `refreshFields()`
  - `textFieldShouldBeginEditing(_ textField: UITextField)`
  - `addDocumentFormView(hidesRemoveButton: Bool = false)`
  - `openPasswordAlert(completion: @escaping(String?) -> Void)`
  - `documentPicker(_ controller: UIDocumentPickerViewController, didPickDocumentsAt urls: [URL])`
  - `documentPickerWasCancelled(_ controller: UIDocumentPickerViewController)`

- **LoanViewController** - contains functions where the user can see their list of active loans, know their upcoming due dates, know their credit limits and apply for loans.
  ##### Methods
  - `didRefreshDashboard(_ sender: Any)`
  - `didTapApplyForALoan(_ sender: Any)`
  - `refreshLoanSchedulesTable()`
  - `refreshLoansTable()`
  - `resetLoanValues()`
  - `updateLoanScreen()`
  - `loadLoanTypes()`
  - `updateCreditLimit()`
  - `updateLoanSchedules()`
  - `updateLoans()`
  - `applyBalanceOnChart()`
  - `numberOfSections()`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, estimatedHeightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`

- **LoanInactiveViewController** - a view which is only displayed if the user has not activated their loan account yet. It contains functions where user can choose to activate their application.  
  ##### Methods
  - `didTapApplyForALoan(_ sender: Any)`
  - `didTapCreateLoanAccountButton(_ sender: Any)`
  - `applyBalanceOnChart(_ usedBalance: Double, creditLimit: Double)`
  - `collectionView(_, numberOfItemsInSection section: Int) -> Int`
  - `collectionView(_, cellForItemAt) -> UICollectionViewCell`
  - `collectionView(_, sizeForItemAt) -> CGSize`

- **CLAStep1ViewController** - a view where the user can upload their documents for loan account activation.  
  ##### Methods
  - `refreshFields()`
  - `addDocumentFormView(hidesRemoveButton: Bool = false) -> DocumentFormView?`
  - `documentPicker(_ controller: UIDocumentPickerViewController, didPickDocumentsAt urls: [URL])`
  - `documentPickerWasCancelled(_ controller: UIDocumentPickerViewController)`

- **CLAStep2a1SignatureAgreementViewController** - a view where the user is prompted for the terms and conditions when activating their loan accounts.  
  ##### Methods
  - `didTapSaveButton(_ sender: Any)`
  - `didTapTNCLabel(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **CLAStep2a2SignatureSignViewController** - a view where the user can sign for loan activation.
  ##### Methods
  - `backupSignature()`
  - `retrieveBackup()`
  - `removeBackup()`
  - `didTapSaveButton(_ sender: Any)`
  - `didTapRedoButton(_ sender: Any)`
  - `didTapStartSigningView(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **CLAStep2a3SignatureReviewViewController** - a view where the user can finalize their signature for loan activation. Upon submission, the user is prompted to wait for approval.  
  ##### Methods
  - `didTapTNCLabel(_ sender: Any)`
  - `didTapSaveButton(_ sender: Any)`
  - `didTapSubmitButton(_ sender: Any)`

- **ApplyLoanViewController** - a view where the user can start applying for a loan.
  ##### Methods
  - `didTapPencilButton(_ sender: Any)`
  - `didChangeSliderValue(_ sender: Any)`
  - `didTapSubmitButton(_ sender: Any)`
  - `setTextFieldsTappable(in view: UIView)`
  - `didTapTextField(_ tap: UITapGestureRecognizer)`
  - `updateCurrentAmount(_ amount: Float, sender: UIView)`
  - `refreshTimer(_ sender: UIView? = nil)`
  - `refreshCalculation(_ sender: UIView? = nil)`
  - `resetCalculatorView()`
  
- **ApplyLoanReviewViewController** - a view where the user can review the information they inputted.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  
- **ApplyLoanStep2ViewController** - a view where the user can upload their documents for loan application.  
  ##### Methods
  - `didTapAddDocumentButton(_ sender: Any)`
  - `didTapBackButton(_ sender: Any)`
  - `didTapSaveButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `refreshFields()`
  - `addDocumentFormView(hidesRemoveButton: Bool = false) -> DocumentFormView?`
  - `documentPicker(_ controller: UIDocumentPickerViewController, didPickDocumentsAt urls: [URL])`
  - `documentPickerWasCancelled(_ controller: UIDocumentPickerViewController)`
  
- **ApplyLoanStep3StartViewController** - a view where the user can download and view agreements for loan application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadButton(_ sender: Any)`
  - `didTapAmortizationButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `savePDF(name: String,from url: URL)`
  
- **ApplyLoanStep3SignatureViewController** - a view where the user can input their signature for loan application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapRedoButton(_ sender: Any)`
  - `didTapStartSigningView(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **ApplyLoanStep3SubmitViewController** - a view where can download and view their signed agreements in the loan application. Has functions to submit the application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadButton(_ sender: Any)`
  - `didTapAmortizationButton(_ sender: Any)`
  - `didTapSubmitButton(_ sender: Any)`
  - `savePDF(name: String,from url: URL)`
  
- **PayLoanWalletViewController** - contains functions to pay loans.
  ##### Methods
  - `didUpdateWalletSession(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `updateBalance()`
  
- **LoanDetailsViewController** - a view that contains information for the loan.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **ApplyCashAdvanceViewController** - a view where the user can apply for a cash advance.
  ##### Methods
  - `loadAmountCap()`
  - `didTapPencilButton(_ sender: Any)`
  - `didChangeSliderValue(_ sender: UISlider)`
  - `didTapSubmitButton(_ sender: Any)`
  - `updateCurrentAmount(_ amount: Float, sender: UIView)`
  - `refreshTimer(_ sender: UIView? = nil)`
  - `refreshCalculation(_ sender: UIView? = nil)`
  - `resetCalculatorView()`
  
- **ApplyCashAdvanceReviewViewController** - a view where the user can review their cash advance application information.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `proceedToAgreement()`

- **ApplyCashAdvanceAgreementViewController** - a view where the user can download and view the cash advance agreement.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadButton(_ sender: Any)`
  - `didTapStartSigningButton(_ sender: Any)`
  - `savePDF(from url: URL)`

- **ApplyCashAdvanceSignatureViewController** - a view where the user can input their signature for the cash advance application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapRedoButton(_ sender: Any)`
  - `didTapStartSigningView(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **ApplyCashAdvanceSubmitViewController** - a view where the user can download and view the signed cash advance agreement as well as containing functions that submit the cash advance application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadButton(_ sender: Any)`
  - `savePDF(from url: URL)`
  - `didTapSubmitButton(_ sender: Any)`

- **ApplyPaydayLoanViewController** - a view where the user can apply for a payday loan.
  ##### Methods
  - `didTapPencilButton(_ sender: Any)`
  - `didChangeSliderValue(_ sender: UISlider)`
  - `didTapSubmitButton(_ sender: Any)`
  - `setTextFieldsTappable(in view: UIView)`
  - `didTapTextField(_ tap: UITapGestureRecognizer)`
  - `updateCurrentAmount(_ amount: Float, sender: UIView)`
  - `refreshTimer(_ sender: UIView? = nil)`
  - `refreshCalculation(_ sender: UIView? = nil)`
  - `resetCalculatorView()`

- **ApplyPaydayLoanReviewViewController** - a view where the user can review their information for the payday loan application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `proceedToAgreement()`

- **ApplyPaydayLoanAgreementViewController** - a view where the user can download and view payday loan agreements.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadPromissoryNoteButton(_ sender: Any)`
  - `didTapDownloadAmortizationScheduleButton(_ sender: Any)`
  - `didTapStartSigningButton(_ sender: Any)`
  - `savePDF(from url: URL)`

- **ApplyPaydayLoanSignatureViewController** - a view where the user can input their signature for payday loan application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapRedoButton(_ sender: Any)`
  - `didTapStartSigningView(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **ApplyPaydayLoanSubmitViewController** - a view where the user can download and view the signed payday loan agreements, contains functions that allow the user to submit the payday loan application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadPromissoryNoteButton(_ sender: Any)`
  - `didTapDownloadAmortizationScheduleButton(_ sender: Any)`
  - `didTapSubmitButton(_ sender: Any)`
  - `savePDF(from url: URL)`

- **PayrollViewController** - a view that contains multiple payroll functionalities.
  ##### Methods
  - `didRefreshDashboard(_ sender: Any)`
  - `updatePayrollScreen()`
  - `updatePayslip(only: Bool = false)`
  - `updateTimesheet(only: Bool = false)`
  - `updatePendingOvertime(only: Bool = false)`
  - `updateCashAdvances(only: Bool = false)`
  - `updatePaydayLoans(only: Bool = false)`
  - `updateLeaves()`
  - `clockIn()`
  - `clockOut()`
  - `cancelOvertime(tranNo: Int)`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, heightForRowAt) -> CGFloat`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`
  - `tableView(_, estimatedHeightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForFooterInSection) -> CGFloat`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`

- **PayslipsViewController** - a view that displays the user's payslips.
  ##### Methods
  - `updatePayslips()`
  - `getFilteredPayslips()`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`
  
- **PayslipDetailsViewController** - a view that displays the payslip details.
  ##### Methods
  - `openAndReloadSection(index: Int, section:String)`
  - `closeAndReloadSection(index: Int, section:String)`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`

- **TimesheetViewController** - a view that contains the user's past timesheets.
  ##### Methods
  - `updateTimesheet()`
  - `getFilteredTimesheet()`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`

- **ApplyOvertimeViewController** - a view where the user can apply for an overtime, contains functions that submit the application.
  ##### Methods
  - `didTapCloseButton(_ sender: Any)`
  - `didTapSubmitButton(_ sender: Any)`
  - `setTextFieldsTappable(in view: UIView)`
  - `didTapTextField(_ tap: UITapGestureRecognizer)`
  
- **LeavesViewController** - a view that displays the user's leave applications.
  ##### Methods
  - `refreshLeaveCredits(only: Bool = false)`
  - `refreshLeaves()`
  - `getApprovedLeaves()`
  - `getPendingLeaves()`
  - `getDeclinedLeaves()`
  - `getFilteredLeaves()`
  - `cancelLeave(tranNo: Int)`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  
- **OvertimeRequestsViewController** - a view that displays the user's overtime requests.
  ##### Methods
  - `refreshRequests()`
  - `getPendingOvertimeRequests()`
  - `getApprovedOvertimeRequests()`
  - `getDeclinedOvertimeRequests()`
  - `getFilteredRequests()`
  - `cancelOvertime()`  
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`

- **ApplyLeaveViewController** - a view where the user can apply for a leave.
  ##### Methods
  - `didTapCloseButton(_ sender: Any)`  
  - `didTapSubmitButton(_ sender: Any)`  
  - `exitLeaveApplication()`  
  - `setTextFieldsTappable(in view: UIView)`
  - `didTapTextField(_ tap: UITapGestureRecognizer)`

- **CashAdvanceListViewController** - a view that lists down the user's cash advance applications.
  ##### Methods
  - `updateCashAdvanceItems()`
  - `getFilteredCashAdvances()`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`  

- **PaydayLoansListViewController** - a view that list's down the user's payday loan applications.
  ##### Methods
  - `updateCashAdvanceItems()`
  - `getFilteredLoans()`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`  

- **ProfileViewController** - contains functions where the user can update their information.
  ##### Methods 
  - `didTapManageProfileButton(_ sender: Any)`
  - `didTapChangePasswordButton(_ sender: Any)`
  - `didTapNotificationButton(_ sender: Any)`
  - `didTapSupportButton(_ sender: Any)`
  - `didTapTermsNPrivacyButton(_ sender: Any)`
  - `didTapDigitalSignOnButton(_ sender: Any)`
  - `didTapShareToFriendButton(_ sender: Any)`
  - `didTapLogoutButton(_ sender: Any)`
  - `shareTextButton()`
  - `presentVC(withIdentifier identifier: String)`

- **ManageProfileViewController** - contains functions where the user can edit their profile information and image.  
  ##### Methods
  - `didTapCameraButton(_ sender: UIButton)`
  - `didTapSaveButton(_ sender: Any)`
  - `refreshFields()`
  - `updateFields(with userInfo: UserInfo, refreshAddress: Bool = true)`
  - `refreshSelectionFields()`
  - `addTapGestureToSelectionFields()`
  - `didTapTextField(_ tap: UITapGestureRecognizer)`
  - `selectImage(sender: UIButton)`
  - `saveProfile()`
  - `textFieldShouldBeginEditing(_ textField: UITextField) -> Bool`
  - `image(_ image: UIImage, didFinishSavingWithError error: Error?, contextInfo: UnsafeRawPointer)`
  - `imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [UIImagePickerController.InfoKey : Any])`

- **ChangePasswordViewController** - contains functions where the user can update their password.  
  ##### Methods
  - `didTapChangePasswordButton(_ sender: Any)`
  - `saveNewPassword()`

- **ChangePINViewController** - contains functions where the user can update their PIN. 
  ##### Methods
  - `didTapChangePINButton(_ sender: Any)`
  - `saveNewPIN()`
  
- **TermsPrivacyViewController** - contains a page of terms and conditions/privacy policy for the users to read.  
  ##### Methods
  - `viewDidLayoutSubviews()`
  - `didTapBackBarButtonItem(_ sender: Any)`

- **DigitalSignOnSettingsViewController** - contains functions where the user can choose to enable signing in using their TouchID/FaceID.  
  ##### Methods
  - `didTapBackBarButtonItem(_ sender: Any)`
  - `didChangeSwitchState(_ sender: UISwitch)`
  - `toggleSwitchControl()`
  - `func turnOnDigitalSignOn()`
  - `turnOffDigitalSignOn()`

- **NotificationSettingsViewController** - contains functions where the user can choose to enable push notifications.  
  ##### Methods
  - `didTapBackBarButtonItem(_ sender: Any)`
  - `didChangeSwitchState(_ sender: UISwitch)`
  - `setSwitchControls()`
  - `togglePushNotification(willOn: Bool)`
  - `togglePaymentReminder(willOn: Bool)`
  - `toggleInvestments(willOn: Bool)`
  - `toggleApplicationStatus(willOn: Bool)`
  - `updateSettings()`
  - `getSettings()`

- **InvestmentViewController** - a view that displays the user's current investments.
  ##### Methods
  - `didTapApplyForInvestment(_ sender: Any)`
  - `refreshInvestments()`
  - `numberOfSections()`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, didSelectRowAt) -> CGFloat`
  
- **InactiveInvestmentViewController** - a view that is displayed if the user has no activated wallet or investments.
  ##### Methods
  - `didTapApplyForInvestment(_ sender: Any)`
  - `showNotice()`

- **ApplyInvestmentViewController** - a view where the user can apply for an investment.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `setTextFieldsTappable(in view: UIView)`
  - `didTapTextField(_ tap: UITapGestureRecognizer)`
  - `calculateInvestment()`

- **ApplyInvestmentSummaryViewController** - a view that show's a summary of the information inputted by the user.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **ApplyInvestmentStep2ViewController** - a view where the user can upload documents for the investment application.
  ##### Methods
  - `didTapAddDocumentButton(_ sender: Any)`
  - `didTapBackButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `refreshFields()`
  - `addDocumentFormView(hidesRemoveButton: Bool = false) -> DocumentFormView?`
  - `documentPicker(_ controller: UIDocumentPickerViewController, didPickDocumentsAt urls: [URL])`
  - `documentPickerWasCancelled(_ controller: UIDocumentPickerViewController)`

- **ApplyInvestmentStep3StartViewController** - a view that displays the investment agreements, contains functions where the user can download or view the agreements.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadPromissoryNoteButton(_ sender: Any)`
  - `didTapDownloadAmortizationScheduleButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `savePDF(name: String,from url: URL)`

- **ApplyInvestmentStep3SignatureViewController** - a view where the user can input their signature for an investment application.
  - `didTapBackButton(_ sender: Any)`
  - `didTapRedoButton(_ sender: Any)`
  - `didTapStartSigningView(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **ApplyInvestmentStep3SubmitViewController** - a view where the user can download and view the signed invesment agreement,contains functions that submit the investment application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadPromissoryNoteButton(_ sender: Any)`
  - `didTapDownloadAmortizationScheduleButton(_ sender: Any)`
  - `didTapSubmitButton(_ sender: Any)`
  - `savePDF(name: String,from url: URL)`
  
- **InvestmentDetailsViewController** - a view that displays the user's investment details.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **HRAdminViewController** - a view that displays both cash advance and payday loans.
  ##### Methods
  - `refreshDashboard(_ sender: Any)`
  - `refreshList(only: Bool = false)`
  - `refreshCashAdvances(only: Bool = false)`
  - `refreshPaydayLoans(only: Bool = false)`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`  
  
- **HRCashAdvanceReviewViewController** - a view that displays a selected cash advance's information, contains functions that can approve/decline an application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDeclineButton(_ sender: Any)`
  - `didTapApproveButton(_ sender: Any)`
  - `reloadLabels()`
  - `updateCashAdvance(with status: CashAdvanceStatus)`

- **HRPaydayLoanReviewViewController** - a view that displays a selected payday loan's information, contains functions that can approve/decline an application.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDeclineButton(_ sender: Any)`
  - `didTapApproveButton(_ sender: Any)`
  - `reloadLabels()`
  - `updateCashAdvance(with status: CashAdvanceStatus)`

- **HRPaydayLoansListingViewController** - a view that displays the list of payday loans for multiple users.
  ##### Methods
  - `didTapCloseBarButtonItem(_ sender: Any)`
  - `refreshList(_ sender: Any)`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `setupPaydayLoanCell()`  
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`

- **HRTimesheetDashboardViewController** - a view that displays the employee timesheets for the current day.
  ##### Methods
  - `refreshList(only: Bool = false)`
  - `refreshTimesheet(only: Bool = false)`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`  
  
- **HRTimesheetSearchViewController** - a view that allows the user to search employees past payslips.
  ##### Methods
  - `updateTimesheet()` 
  - `getFilteredTimelogs()` 
  - `refreshGroups()` 
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  
- **HREmployeeTimesheetViewController** - a view that displays an employee's past timesheets.
  ##### Methods
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  
- **HRTimelogDetailsViewController** - a view that displays information about a selected employee timesheet.
  ##### Methods
  - `didTapWholeView(_ sender: Any)`
  - `didTapCloseButton(_ sender: Any)`
  - `reloadLabels()`
  - `didTapBackButton(_ sender: Any)`
  
- **HREmployeeTimsheetFilterViewController** - a view that displays all of the selected user's timesheets, contains functions to filter the date.
  ##### Methods
  - `didTapWholeView(_ sender: Any)`
  - `didTapCancelButton(_ sender: Any)`
  - `didTapSearchButton(_ sender: Any)`
  
- **HRLeavesDashboardViewController** - a view that displays the most recent employee leave applications.
  ##### Methods
  - `refreshList(only: Bool = false)`
  - `refreshLeaves(only: Bool = false)`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`  
  
- **HRLeavesFilterViewController** - a view where the user can search for employees with leaves.
  ##### Methods
  - `updateLeaves()`
  - `getFilteredLeaves()`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`  

- **HRLeaveReviewViewController** - a view that displays a user's leave application, contains functions that can approve/decline an applications.
  ##### Methods
  - `didTapWholeView(_ sender: Any)`
  - `didTapDeclineButton(_ sender: Any)`
  - `didTapApproveButton(_ sender: Any)`
  - `reloadLabels()`
  - `updateLeaves(approved: Bool)`

- **HROvertimeDashboardViewController** - a view that displays the most recent overtime requests.
  ##### Methods
  - `refreshList(only: Bool = false)`
  - `refreshOvertimes()`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`  

- **HROvertimeListViewController** - a view where the user can search for the past overtime requests of a suer.
  ##### Methods
  - `updateOvertimes()`
  - `getFilteredOvertimes()`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat`  

- **HROvertimeReviewViewController** - 
  ##### Methods
  - `didTapWholeView(_ sender: Any)`
  - `didTapDeclineButton(_ sender: Any)`
  - `didTapApproveButton(_ sender: Any)`
  - `reloadLabels()`
  - `updateOvertime(approved: Bool)`

- **HRPayslipDashboardViewController** - 
  ##### Methods
  - `refreshList(only: Bool = false)`
  - `refreshPayslips(only: Bool = false)`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, estimatedHeightForRowAt) -> CGFloat`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  - `tableView(_, heightForFooterInSection) -> CGFloat` 

- **HRPayslipListViewController** - 
  ##### Methods
  - `refreshPayslips()` 
  - `getFilteredPayslips()` 
  - `refreshData()` 
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  
- **HRPayslipDetailsViewController** - 
  ##### Methods
  - `openAndReloadSection(index: Int, section:String)`
  - `closeAndReloadSection(index: Int, section:String)`
  - `numberOfSections(in tableView: UITableView) -> Int`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`

- **HRPastPayslipsListViewController** - 
  ##### Methods
  - `refreshPayslips(id: String)`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`

- **HRAdminEmployeesViewController** - a view that displays all the employees with a search box.
  ##### Methods
  - `refreshList()`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`
  
- **HRCashAdvanceListViewController** - a view that displays more cash advances in a list, is used by both active list and application list.
  ##### Methods
  - `didTapCloseBarButtonItem(_ sender: Any)`
  - `refreshList(_ sender: Any)`
  - `tableView(_, numberOfRowsInSection) -> Int`
  - `tableView(_, cellForRowAt) -> UITableViewCell`
  - `tableView(_, viewForHeaderInSection) -> UIView?`
  - `tableView(_, heightForHeaderInSection) -> CGFloat`

  ### DIAGRAM

  ![Application Architecture](diagram.png 'Application Architecture')

  #### **Model**

  Models encapsulates a particular set of data, and contains logic to manipulate the data. Models are contained within the Models folder of the RCF application source code

  #### **View**

  Views are the interface/s the user can see and interact with. Objects like UI Button, UIView and UILabel are examples of views. Views can be found in the Storyboards folder of the RCF application source code

  #### **Controller**

  Controllers controlls all logic that goes between the View and the Model. Objects like UIViewController, CLLocationManager and UINavigationController are examples of controllers. Controllers can be found in the ViewControllers folder of the RCF application source code
