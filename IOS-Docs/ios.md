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

- **ApplyLoanViewController** - 
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
  
- **ApplyLoanReviewViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  
- **ApplyLoanStep2ViewController** - 
  ##### Methods
  - `didTapAddDocumentButton(_ sender: Any)`
  - `didTapBackButton(_ sender: Any)`
  - `didTapSaveButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `refreshFields()`
  - `addDocumentFormView(hidesRemoveButton: Bool = false) -> DocumentFormView?`
  - `documentPicker(_ controller: UIDocumentPickerViewController, didPickDocumentsAt urls: [URL])`
  - `documentPickerWasCancelled(_ controller: UIDocumentPickerViewController)`
  
- **ApplyLoanStep3StartViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadButton(_ sender: Any)`
  - `didTapAmortizationButton(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `savePDF(name: String,from url: URL)`
  
- **ApplyLoanStep3SignatureViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapRedoButton(_ sender: Any)`
  - `didTapStartSigningView(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`

- **ApplyLoanStep3SubmitViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapDownloadButton(_ sender: Any)`
  - `didTapAmortizationButton(_ sender: Any)`
  - `didTapSubmitButton(_ sender: Any)`
  - `savePDF(name: String,from url: URL)`
  
- **PayLoanWalletViewController** - 
  ##### Methods
  - `didUpdateWalletSession(_ sender: Any)`
  - `didTapNextButton(_ sender: Any)`
  - `updateBalance()`
  
- **LoanDetailsViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **ApplyCashAdvanceViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **ApplyCashAdvanceReviewViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **ApplyCashAdvanceAgreementViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **ApplyCashAdvanceSignatureViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **ApplyCashAdvanceSubmitViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **ApplyPaydayLoanViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **PayrollViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **PayslipsViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  
- **PayslipDetailsViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **TimesheetViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **ApplyOvertimeViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  
- **LeavesViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **OvertimeRequestsViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  
- **ApplyLeaveViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`  

- **CashAdvanceListViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

- **PaydayLoansListViewController** - 
  ##### Methods
  - `didTapBackButton(_ sender: Any)`

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

  ### DIAGRAM

  ![Application Architecture](diagram.png 'Application Architecture')

  #### **Model**

  Models encapsulates a particular set of data, and contains logic to manipulate the data. Models are contained within the Models folder of the RCF application source code

  #### **View**

  Views are the interface/s the user can see and interact with. Objects like UI Button, UIView and UILabel are examples of views. Views can be found in the Storyboards folder of the RCF application source code

  #### **Controller**

  Controllers controlls all logic that goes between the View and the Model. Objects like UIViewController, CLLocationManager and UINavigationController are examples of controllers. Controllers can be found in the ViewControllers folder of the RCF application source code
