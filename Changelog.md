Changelog

v1.5.0 (3-6-20)

## Frontend Changes
 - Always show the arrested date even if there is no disposition (#877)
 - Hide the time eligibility if the charge is type-ineligible
 - Link case IDs in error banners (#920)
 - Show an error and force a reload if any case page fetches fail (#914)
 - Add-User panel is operational (#889)

## Expungement Logic Fixes

- Remove Subsection 12 (#898)
- New Marijuana Eligible type (#892)
- Fixed Manufacture/Delivery type (#892)
- Overhaul Person Felony (#870, #884)
- Don't apply the friendly rule if conviction needs more analysis (#882)
- Show type eligibility when missing/unrecognized disposition, if possible (#844)

v1.4.8 (2-23-20)

## Frontend Changes

- Allow multiple aliases in search (#823, #852)
- New logo (#855, #858)
- Summary panel excludes parking tickets and traffic violations (#841)
- Rewrite Time eligibility reasons ("X years from most recent _ ", etc.) (#872)

## Expungement Logic Fixes

- Fix the friendly rule: Compute correct date if the "conviction" is two violations; only change arrest date if it's an improvement (#773)

## Other Changes

- Add rules documentation for more charge types. (#843, #853, #856)


v1.4.5 (2-10-20)

## Frontend Changes

- Middle name field added to record search (#802)
- Navbar doesn't show "Admin" button if user is not admin (#783)
- Time eligibility is hidden from results if the charge is type-ineligible (#798)
- "Forgot password" link is removed until feature gets implemented (#799)

## Expungement Logic Fixes

- Time eligibility is "never" if the charge is type-ineligible (#771)
- Non-blocking charge types (like Juvenile) still receive time analysis (#772)
- Traffic offenses are distinguished between violation and non-violation types (#792)
- Civil Offenses are identified by statute chapters 1-99 and are distinguished from Parking Tickets (#794)
- Subsection 6 charge type created with the subsection's list of "needs more analysis" charges (#813)
- Subsection 12 charge type fixed to only match the subsection's list (#813)

## Other changes
- User-readable documentation for Class B Felony, Subsection 12, and Subsection 6 charge types available in project docs folder (#814)

v1.4.0 (never released)

## Frontend Changes

- Result Summary Panel added to search results. Each case number is an in-page link to that case's details (#756)
- Adjusted Case header format to match prototype, and include the County (#766)
- Website landing page added with a link to app login (#744)
- Add User and Edit User components added, but are not yet functional (#729)
- Minor tweak to the error banner for an unrecognized ruling (#759)

## Expungement Logic Fixes

- Amended Disposition gets parsed as an additional disposition event. The last disposition event for each charge determines that charge's final ruling (#758)
- Rewrite of time analysis logic that correctly handles a pair of non-blocking violations, in addition to preventing other potential bugs  (#742)

## Other Bug Fixes

- Navigating to the app on Http will redirect silently to Https (preventing a possible login error) (#740)

v1.3.0 (1-17-20)

## Frontend Changes

- "Arrested" date field is renamed to "Charged" because parking tickets etc. don't involve an arrest (#730)
- A missing disposition is not reported as an error if the case is open (#715)
- A missing disposition is reported as "Missing", not "Unknown" (#713)

## Expungement Logic Fixes

- If a case has a single conviction and it's eligibile, all arrests on that case are also eligible (#716)
- A charge that's time-ineligible forever (e.g. certain Class B felony convictions) properly display the "Ineligible" label (#714, #720)
- If an open case still has charges with valid dispositions, run analysis on those charges (#707)

v1.2.0 (1-8-20)

## Frontend Changes

- Display error message in the results if the record has open cases or missing/unrecognized dispositions (#685, #686)
- Show the arrest date for both dismissals and convictions (#683)
- Show the time analysis even if there is an error due to open cases (open cases are ignored in the analysis) (#649)
- Show the "type" of charge as it is understood for the purposes expungement logic (#698)
- Minor display format fixes (#669)

## Expungement Logic Fixes

- Make violation charge identification more robust (#668)
- Class B Felony convictions are ineligible if there are any subsequent charges (#653)
- Class B Felony convictions follow the usual rules for affecting other charges' time eligibility (#653)
- Fixed the time eligibility for a single non-traffic violation conviction (3 years) (#682)
- The dispositions "accusatory instrument filed" and "removed from charging instrument" are both interpreted as dismissals (#696)

v1.1.0 (12-19-19)

## Frontend Changes

- More flexible date format (leading zeros e.g. 01/01/2000 are no longer required) (#615)
- Birth date field is optional for record search (#589)
- Dismissed charge correctly shows arrest date rather than dismissal date (#622)
- Arrest and eligibility dates no longer include time of day (#629)
- OECI login expires after 2 hours (extended from 15 minutes) (#659)

## Expungement Logic Fixes

- Unclassified charge is always labeled with "needs more analysis" (#623)
- "Diverted", "Finding - Guilty", and other irregular dispositions are identified correctly. (#648, #637)

## Other Bug Fixes

- Fix an OECI page parsing error for some records (#646)
- App will not log out when the user enters wrong OECI credentials (#664)

## Enhancement

- Read OECI pages in parallel, speeding search (#632)

v1.0.0

## Features

- Add search page and search endpoint (#341, #434, #439, #446, #533, #564, #570, #572)
- Add group component (only w/ mock data) (#445)
- Add /api/users PUT (update user) (#459)
- Add mocked oeci endpoints (#484, #526)
- Update case parser to check if probation revoked (#490)
- Add logout endpoint (#521, #529)
- Save anonymized search results to database (#576)
- Integrate user component with /api/users GET endpoint (#583)

## Fixes

- Ensure HTTP cookies are secure=True on production (#563)
- Fix case where disposition is not set (#579)
- Handle case status "Bankruptcy Pending" as closed (#585)
- Redirect to OECI login from search page (#587)
- Allow empty birth date upon search form submission (#589)
- Check for oeci_token before attempting search (#590)
- Add new DUII charge class (#607)

v0.3.3

## Bug Fixes

 - The function to check if a case is closed now returns true when the term `Purgable` is encountered in the status. (386)
 - Fixed issue where parking tickets that were acquitted were being tagged as type eligible. Parking tickets are never type eligible. (369)
 - Fixed issue where some parking tickets were being missed due to the difference in reporting statute codes. Parking tickets are now created by case type `Municipal Parking` after statute creation fails. (#427)
 - Fixed issue where a single violation would count as a recent conviction. Updated rules for MRC and second mrc to only apply a violation if there is a second violation. (429)


________________________________________________________________________________________________

v0.3.2

## Bug Fixes

 - Fixed issue where infractions were affecting the analysis. Now it explicitely checks whether or not the level is felony or misdemeanor. (#290)
 - Fixed issue where 800 level charges were incorrectly being set as type eligible. Charges are only set as type eligible if they're dismissed and either a misdemeanor or felony. (#319)


________________________________________________________________________________________________

v0.3.1

## Enhancements

 - Small speed improvement. Pinging the logging server to wake it up is now done asynchronously.
 - The results file now contains a list of eligible cases under the header of the file.
 - "END OF FILE" is now printed at the bottom of the results file
 - For each charge that is displayed it also prints out how the type analyzer classified the charge type. For example: Level800Charge, Misdemeanor, FelonyClassC, etc... is now shown above each charge. This can be used to determine the exit point of the expungement analysis for the charge so that it can be shown why it is or isn't type eligible. And can be helpful in providing feedback/bug reports if a charge is classified incorrectly. Currently any charge that cannot be classified will be classified as an 'Unclassified Charge', the long term goal is to have zero charges falling into this classification.

## Bug Fixes

 - Fixed issue where some parking tickets were not being classified correctly. (#250)

 - Charges without a disposition are marked as 'Disposition not found' and skipped. (#255)

 - Juvenile charges are marked appropriately and skipped by the expunger. (#258)

 - Fixed issue where Case Parser threw a ValueError exception when encountering a disposition transaction being used to log a comment. (#263)

 - Fixed issue where expungment analysis was not ran when open violation level & parking cases exist. They're now treated as being closed cases. (#264)

 - Fixed traffic charge type eligibility. Felonies and misdemeanors are now type eligibile, violations are not. (#268)

 - Fixed issue that MRD was blocking convictions. MRD now only blocks arrests. (#280)

 - Fixed issue where motor vehicle violations were affecting the time analysis. Parking tickets and level 800 "violations" are no longer included in the time analysis. (#286)

 - Fixed issue that an incorrect eligibility date could be calculated when a 2nd mrc exists. (#288)
