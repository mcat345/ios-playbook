Inventory of Identified Technical Debt and known Legacy Code.
=============================================================

Technical debt and legacy code has a sad tendency to build up in any software project. As the iOS project has grown both in terms of team members and supported apps we have found that managing technical has become more difficult. Legacy code should be ideally be refactored to clear technical debt when changes are needed. Existing technical debt that should be addressed when working on a new feature should be included in the planning. There is an obvious risk that legacy code is maintained instead of refactored if it is not clear what the technical debt currently is.

## Objective-C code and GatewayManager.

GatewayManager supplies global dependencies to legacy Objective-C code. There was plenty of code in version one and two of the Babylon app that relied heavily on singletons.

| Objective-C view Controllers | Location | Comments |
| ---------------------------- | ---------| -------- |
| BillingInformationViewController | Clinical Records | CNSMR-930 |
| EditMembershipCodeViewController | Clinical Records | CNSMR-934 |
| MembershipTableViewController | Me Tab | CNSMR-926 |
| SurveyViewController | Clinical Records | CNSMR-937 |
| InsuranceViewController | Clinical Records | CNSMR-942 |
| BBAddAdditionalPatientInformationViewControllerV2 | Clinical Records | Might be dead code but will be deleted as part of CNSMR-947 |

Some additional information about [BBAddAdditionalPatientInformationViewControllerV2](./BBAddAdditionalPatientInformationViewControllerV2.md)

## Free Standing Swift View Controllers that should be Moved to Bento.

| View Controller | Comments |
| --------------- | -------- |
| InfoViewController | Could be replaced with a Bento Component for scrolling through a couple of info screens. Only used for the GP @ hand on-boarding so could be moved from BabylonUI. |
| SegmentedViewController | Currently only used in Healthcheck to show the the two bands with organs and layers. Should probably be moved from BabylonUI. |
| IntroViewController | Could potentially be merged with InfoViewController. |

## View Models and Controllers that use Forms V2.

Forms V2 is no longer maintained and we should refactor these view controllers to use Bento.
Porting these view controllers to Bento will also make it easier to apply an app wide style guide (design library).

| View Model | Comments |
| ---------- | -------- |
| AppointmentCancellationViewModel | CNSMR-950, CNSMR-951 |
| AppointmentConsultationNotesViewModel | CNSMR-952, CNSMR-953 |
| AppointmentDetailsViewModel | CNSMR-954, CNSMR-955 |
| AppointmentNotesViewModel | CNSMR-956, CNSMR-957 |
| AppointmentPrescriptionViewModel | CE-30 |
| AppointmentReferralViewModel | CNSMR-958, CNSMR-959 |
| AppointmentReferralsViewModel | CNSMR-960, CNSMR-961 |
| AppointmentReplayViewModel | CNSMR-962, CNSMR-963 |
| AppointmentListViewModel | CNSMR-964, CNSMR-965 |
| BookAppointmentViewModel | CNSMR-966, CNSMR-967 |
| PractitionerDetailsViewModel | CNSMR-968, CNSMR-969 |
| ChatHistoryViewModel | CNSMR-970, CNSMR-971 |
| MedicalHistoryViewModel | CNSMR-972, CNSMR-973 |
| PersonalDetailsViewModel | CNSMR-974, CNSMR-975 |
| InfoItemsViewModel | CNSMR-976, CNSMR-977 |
| GPDetailsViewModel | CNSMR-978, CNSMR-979 |
| AddAddressViewModel | CNSMR-980, CNSMR-981 |
| PrivacySettingsViewModel | AV-334 |
| ChooseCountryViewModel | AV-338 |
| ForgotPasswordViewModel | CNSMR-904 |
| NotificationsViewModel | AV-342 |
| ProfileViewModel | AV-340 |
| SignInViewModel | AV-332 |
| NHSRegistrationStep1ViewController | NRX-361 |
| NHSRegistrationStep2ViewController | NRX-186 |

## Accessing Business Controllers Directly instead of using the SDK.

Some of these business controllers are not defined inside the SDK. Most of them will be moved to the SDK, but some of them will stay in the Babylon project. Once the first, complete version of the SDK has been published there should not be any business controllers left in BabylonCore. Business controllers that are defined outside the SDK should have a documenting comment that explain why they are not part of the SDK.

| Business Controller | Accessed From |
| ------------------- | ------------- |
| AppointmentBusinessControllerProtocol | BabylonAppointmentsUI, Babylon |
| AddressBusinessControllerProtocol | BabylonAppointmentsUI, BabylonUI, Babylon |
| PractitionerBusinessController | BabylonAppointmentsUI |
| PatientBusinessControllerProtocol | BabylonAppointmentsUI, BabylonClinicalRecordsUI, BabylonUI, Babylon |
| PrescriptionBusinessControllerProtocol | BabylonAppointmentsUI, Babylon |
| PharmaciesBusinessControllerProtocol | BabylonAppointmentsUI, BabylonClinicalRecordsUI |
| ImageBusinessControllerProtocol | BabylonAppointmentsUI, BabylonClinicalRecordsUI, BabylonMonitor, Babylon |
| BookAppointmentBusinessControllerProtocol | BabylonAppointmentsUI |
| PrivacyBusinessControllerProtocol | BabylonAppointmentsUI, BabylonChatBotUI, BabylonUI |
| PublicHealthcareIdentifierBusinessController | BabylonAppointmentsUI, BabylonClinicalRecordsUI, BabylonUI, Babylon |
| SearchAssistantBusinessController | BabylonChatBotUI |
| MedicalHistoryBusinessController | BabylonClinicalRecordsUI |
| GenderBusinessControllerProtocol | BabylonClinicalRecordsUI, BabylonUI, Babylon |
| GeolocationBusinessController | BabylonClinicalRecordsUI, BabylonUI |
| InfoItemsBusinessControllerProtocol | BabylonClinicalRecordsUI |
| MapsBusinessControllerProtocol | BabylonClinicalRecordsUI |
| GPDetailsBusinessController | BabylonClinicalRecordsUI |
| HealthcheckReportBusinessControllerProtocol | BabylonMonitor, BabylonUI, Babylon |
| ReferAFriendBusinessControllerProtocol | BabylonUI, Babylon |
| RatingBusinessController | BabylonUI |
| FamilyBusinessControllerProtocol | BabylonUI |
| RedemptionBusinessController | Babylon |
| RegionBusinessControllerProtocol | Babylon |
| EligibilityCheckBusinessControllerProtocol | Babylon |
| NotificationPayloadBusinessControllerProtocol | Babylon |
| SignInPrivacyBusinessControllerProtocol | Babylon |
| PaymentsBusinessControllerProtocol | Babylon |
| PDSQueueBusinessControllerProtocol | Babylon |
| LocationEligibilityBusinessController | Babylon |
| PostCodeEligibilityBusinessControllerProtocol | Babylon |
| SignUpBusinessController | Babylon |
| SignUpPrivacyBusinessController | Babylon |
| ForgotPasswordBusinessControllerProtocol | Babylon |
| FamilyBusinessControllerProtocol | Babylon |
| OnfidoBusinessControllerProtocol | Babylon |
| PDSBusinessControllerProtocol | Babylon |
| NHSBusinessController | Babylon |
| CreditCardsBusinessControllerProtocol | Babylon |
| TestsAndKitsBusinessControllerProtocol | Babylon |
| RedemptionBusinessControllerProtocol | Babylon |
| ForgotPasswordBusinessController | Babylon|


## Main Tab Bar and Navigation.

Although much improved since version two was released, there is still a fair amount of confusing legacy code left in the tab bar flow controller and associated builders. Now that all content has been refactored to be based on reactive functional programming, flow controllers and builders it is possible to align `ExchangeableTabBarBuilder` and `TabContentBuilder` entities to follow our general design pattern. For historical reasons some flow controllers acts have logic for building view controllers. The `BabylonTabBarViewModel` should be able to forward all routing events to the appropriate flow controller. Some networking logic should be removed from `BabylonTabBarViewModel`. These deviations from our standard architecture makes it difficult to understand the code and changes often result in long and confusing discussions.

## Adapt the Code to Employ Current.

Entities that have been moved to Current are still accessed via `AppDependencies`. Our agreed approach was to inject entities from Current into builder initialisers as default arguments. Before we extend Current to include more app wide content we should refactor how what is already available is accessed.
