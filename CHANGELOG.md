# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## 5.17.0 - 2024.12.30
### Changed
 - Use `PackageLicenseExpression` in csproj file [#583], [#584]
### Added
 - Added mermaid graph support [#585]
 - Allow PermitDynamic destination state to be calculated with an async function (Task) [#595]
 - Updated readme to clarify re-entry behaviour of dynamic transitions [#604]
 - Added .NET 9.0 to build targets [#610]
### Fixed
 - Unexpected graph labels for internal transitions [#587]
 - Labels not escaped in `UmlDotGraphStyle` [#597]

## 5.16.0 - 2024.05.24
### Changed
 - Permit state reentry from dynamic transitions [#565]
   - This is a change in behavior from v5.15.0 (see [#544]); this version restores the previous behavior for `PermitDynamic` that allows reentry;
     if reentry is not the desired behavior, consider using a guard condition with `PermitDynamicIf`.
 - Remove getDestination, and use Destination property instead (internal refactor) [#575]
### Added
 - Add overloads to `FireAsync` to support parameterized trigger arguments [#570]
 - Add overloads to `CanFire` to support parameterized trigger arguments [#574]
### Fixed
 - Prevent `NullReferenceException` in the `InvocationInfo` class [#566]

## 5.15.0 - 2023.12.29
### Changed
 - Updated net6.0 build target to net8.0 [#551]
 - New abstract method, `GetInitialTransition`, added to `GraphStyleBase` to remove DOT graph implementation from `StateGraph` [#557]
   - Classes that are derived from `GraphStyleBase` and are being migrated from an earlier release of Stateless will need to implement this method.
### Added
 - Added license information and README file to NuGet package [#539], [#553]

## 5.14.0 - 2023.11.14
### Added
 - Enable Source Link & Deterministic Builds [#501]
 - Added optional `RetainSynchronizationContext` property [#519]
 - Update example apps to `net6.0` [#520]
 - Bump solution Visual Studio version to 2022 [#526]
 - Remove obsolete TargetFrameworks [#524]
 - Added `FireAsync(TriggerWithParameters, params object[])` overload [#536]
### Fixed
 - `StateMachineInfo.InitialState.Transitions` throws if `AddRelationships` not called [#514]
 - Trigger information is missing for `OnEntryFromAsync` [#511]
 - Fixed typos & redundant parentheses [#512], [#521], [#522]
 - Change mechanism for losing the synchronization context [#528]
 - `InvalidOperationException` thrown from call to `FireAsync` [#532]
 - Added missing guard function parameter support from `InternalTransitionAsyncIf` [#530]
 - Using `PermitIf` on a state with substates leads to reentry [#544]

## 5.13.0 - 2022.12.29
### Added
 - Add method to get permitted triggers with parameter information [#494]
### Fixed
 - Fix incorrect initial state in dotgraph after trigger fired [#495]

## 5.12.0 - 2022.10.17
### Added
 - Add explicit .NET 6.0 framework support [#479]
 - Stateless.Tests -> .NET 6 [#484]
 - Update Readme regarding state machine events [#488]
### Fixed
 - Typo in summary comment of class UmlDotGraph [#471]
 - Github workflows/dotnet pack: Fix project path casing and directory separators [#478]
 - Hardcode the AssemblyName attribute in the .csproj to "Stateless" [#480]
### Security
 - Bump Newtonsoft.Json from 10.0.3 to 13.0.1 in /example/JsonExample [#487]

## 5.11.0 - 2021.04.28
### Added
 - Added CanFire overload to return unmet guard descriptions [#443]
### Fixed
 - Inconsistency in sync/async statemachine execution [#444]
 - Added support for spaces in state/trigger names in Graphviz node graphs by wrapping them in escaped quotes [#447]

## 5.10.1
Re-releasing 5.2.0 as v5.10.1.
The version number was accidentally set to 5.10 when creating the 5.2 release.
Version 5.10.0 is now listed as the newest, since it has the highest version number.
5.2.0 and 5.10.0 are identical.

## 5.2.0
### Added
 - Added support for net50
### Changed
 - Only run tests under net50
 - Non-code change: Switch to using Github Actions
### Fixed
 - Fixed the bug "IgnoreIf Guard description is raised when PermitReentryIf Guard Fails". [#422]

## 5.1.8
### Fixed
- Fixed bug "When adding .PermitDynamicIf, call .PermitTriggers throw NullReferenceException" [#416]

## 5.1.7 - 2021.01.10
### Fixed
 - Fixed nullReferenceException when getting permitted triggers on a dynamic transition. [#413]

## 5.1.7 - 2021.01.10
### Fixed
 - Fixed OnTransitionCompletedEvent, it now has the correct Destination state when there is an initial transition. [#413]

## 5.1.6 - 2020.11.21
### Fixed
 - Added support for new OnTransitionCompletedEvent, which is run after all OnExit / OnEntry methods have run [#394]

## 5.1.5 - 2020.11.16
### Changed
 - Fixed spelling errors
 - Fixed analyser warnings (mostly null checks)
### Fixed
 - Added CLSCompliant attribute, which went missing in November 2019 [#401]

## 5.1.4 - 2020.11.07
### Fixed
 - Fixed Unmet guard collection not set by OnUnhandledTrigger if transition guard of substate fails [#398] (Thanks to the awesome DeepakParamkusam)
 
## 5.1.3 - 2020.08.12
### Fixed
 - Fixed ambiguos guard function call when trigger is a state [#380]
 
## 5.1.2 - 2020.04.27
### Fixed
 - Fixed wrong onTransitionEvent ordering in Async firing [#372]

## [5.1.1] - 2020.04.03
### Changed
- Inverted if (_firingMode.Equals(FiringMode.Immediate) into if (FiringMode.Immediate.Equals(_firingMode) to avoid VerificationException  when including assembly AllowPartiallyTrustedCallers [#365].

## [5.1.0] - 2020.03.24
### Added
- Added missing possible destination states to all PermitDynamic and PermitDynamicIf, see issue [#305].

### Fixed
- Fixed trigger execution order issue if there are uncaught exceptions. Ref issue [#267]
- Fixed issue #272 and #275. Triggers with no parameters threw exceptions when checking if they could be fired, or retrieved with GetPermittedTriggers.

## [5.0.1] - 2020.03.13
### Fixed
- Added missing initial transition, see PR #286.

## [5.0.0] - 2020.02.28
### Changed
- Activate and deactivate actions only runs on manual call to Activate / Deactivate. This breaks the v4.4 implementation, where activate/deactivate actions are run on every state transition.

## [4.4.0] - 2020.02.07
### Changed
- PR #348 Added trigger parameters to OnTransitioned event
### Fixed
- #342 StateMutator is called multiple times with the same state 
- #345 Wrong behavior with FiringMode.Immediate in version 4.3.0
- #339 OnEntry behavour different: Unit test broken when updated to 4.3.0 from 4.2.1
- #292 Nested InitialTransitions calls superstate onEntry twice

## [4.3.0] - 2019.11.11
### Changed
- Netstandard2.0 support

## [4.2.0] - 2018.06.01
### Added
 - PR #254 Add initial transitions
### Changed
- Simplified examples a bit and added comments 
### Fixed
- #261 Reentrant trigger in substate causes exit action to be executed twice
- #263 NullReferenceException bug introduced in commit c13e181b

## [4.1.0] - 2018-05-18
### Added
 - #246 Queuing should not be the default behavior
### Fixed
 - #191 Shouldn't Reentry fire OnEntry from substate?
 - #228 guard function called twice?
 - #214 Transition object holds parent state as source state instead of child
 - #249 Latest prerelease v4.0.1-dev-00294 bug (Internal transition handler not executing)

## [4.0.0] - 2017-09-30
### Added
 - #169 HTML format DOT graph output
 - #132 Conditional InternalTransition
 - #130 Support InternalTransition for all TriggerWithParams  
### Changed
 - #178 Replace calls to Enforce.ArgumentNotNull with in-place null checks, and other changes suggested by CodeCracker
 - #168 Modified the output of OnUnmute to display the correct message
 - #164 Reducing confusion, and fixing invalid cast in Reflection.  
 - #158 Create new ActionInfo class, start insinuating it
 - #156 TriggerInfo.Value -> UnderlyingTrigger  
 - #149 Moved StateType and TriggerType into StateMachineInfo, removed TriggerInfo
 - #147 Extracting common abstract base class for transition info
 - #142 Further reflection API refinement
 - #141 Update to RTM dotnet tooling/VS2017
 - #137 Replace magic string usages with nameof()
 - #125 Adding check for cyclic configuration
 - #123 Update for the current .NET Core version  
 

### Deprecated
### Removed
### Fixed
 - #175 Fix Multiple internal transition actions executed if defined in state hierarchy, and Renamed DynamicTransitionInfo.Destination to DestinationDescription  
 - #144 Fix unbounded recursion/fully initialize sub/super-states
 - #140 Adding recursive trigger processing to InternalFireAsync  

## [3.1.0] - 2016-12-15
### Added
### Changed
### Deprecated
### Removed
### Fixed

## [3.0.1] - 2016-11-23
### Added
### Changed
### Deprecated
### Removed
### Fixed

## [3.0.0] - 2016-11-03
### Added
### Changed
### Deprecated
### Removed
### Fixed

## Release template - version and date goes here
### Added
### Changed
### Deprecated
### Removed
### Fixed

[#610]: https://github.com/dotnet-state-machine/stateless/pull/610
[#604]: https://github.com/dotnet-state-machine/stateless/issues/604
[#597]: https://github.com/dotnet-state-machine/stateless/pull/597
[#595]: https://github.com/dotnet-state-machine/stateless/pull/595
[#587]: https://github.com/dotnet-state-machine/stateless/pull/589
[#585]: https://github.com/dotnet-state-machine/stateless/issues/585
[#584]: https://github.com/dotnet-state-machine/stateless/pull/584
[#583]: https://github.com/dotnet-state-machine/stateless/pull/583
[#575]: https://github.com/dotnet-state-machine/stateless/pull/575
[#574]: https://github.com/dotnet-state-machine/stateless/pull/574
[#570]: https://github.com/dotnet-state-machine/stateless/pull/570
[#566]: https://github.com/dotnet-state-machine/stateless/pull/566
[#565]: https://github.com/dotnet-state-machine/stateless/issues/565
[#551]: https://github.com/dotnet-state-machine/stateless/pull/551
[#557]: https://github.com/dotnet-state-machine/stateless/issues/557
[#553]: https://github.com/dotnet-state-machine/stateless/issues/553
[#539]: https://github.com/dotnet-state-machine/stateless/issues/539
[#501]: https://github.com/dotnet-state-machine/stateless/pull/501
[#519]: https://github.com/dotnet-state-machine/stateless/pull/519
[#520]: https://github.com/dotnet-state-machine/stateless/pull/520
[#526]: https://github.com/dotnet-state-machine/stateless/pull/526
[#524]: https://github.com/dotnet-state-machine/stateless/pull/524
[#536]: https://github.com/dotnet-state-machine/stateless/pull/536
[#514]: https://github.com/dotnet-state-machine/stateless/pull/514
[#511]: https://github.com/dotnet-state-machine/stateless/pull/511
[#522]: https://github.com/dotnet-state-machine/stateless/pull/522
[#521]: https://github.com/dotnet-state-machine/stateless/pull/521
[#512]: https://github.com/dotnet-state-machine/stateless/pull/512
[#528]: https://github.com/dotnet-state-machine/stateless/pull/528
[#532]: https://github.com/dotnet-state-machine/stateless/pull/532
[#530]: https://github.com/dotnet-state-machine/stateless/pull/530
[#544]: https://github.com/dotnet-state-machine/stateless/pull/544
[#494]: https://github.com/dotnet-state-machine/stateless/pull/494
[#495]: https://github.com/dotnet-state-machine/stateless/pull/495
[#479]: https://github.com/dotnet-state-machine/stateless/pull/479
[#484]: https://github.com/dotnet-state-machine/stateless/pull/484
[#488]: https://github.com/dotnet-state-machine/stateless/pull/488
[#471]: https://github.com/dotnet-state-machine/stateless/pull/471
[#478]: https://github.com/dotnet-state-machine/stateless/pull/478
[#480]: https://github.com/dotnet-state-machine/stateless/pull/480
[#487]: https://github.com/dotnet-state-machine/stateless/pull/487
[#443]: https://github.com/dotnet-state-machine/stateless/pull/443
[#444]: https://github.com/dotnet-state-machine/stateless/issues/444
[#447]: https://github.com/dotnet-state-machine/stateless/pull/447
[#422]: https://github.com/dotnet-state-machine/stateless/issues/422
[#416]: https://github.com/dotnet-state-machine/stateless/issues/416
[#413]: https://github.com/dotnet-state-machine/stateless/issues/413
[#394]: https://github.com/dotnet-state-machine/stateless/issues/394
[#401]: https://github.com/dotnet-state-machine/stateless/issues/401
[#398]: https://github.com/dotnet-state-machine/stateless/issues/398
[#380]: https://github.com/dotnet-state-machine/stateless/issues/380
[#373]: https://github.com/dotnet-state-machine/stateless/issues/372
[#365]: https://github.com/dotnet-state-machine/stateless/pull/365
[#272]: https://github.com/dotnet-state-machine/stateless/issues/272
[#275]: https://github.com/dotnet-state-machine/stateless/issues/275
[#267]: https://github.com/dotnet-state-machine/stateless/issues/267
[#305]: https://github.com/dotnet-state-machine/stateless/issues/305
[4.2.0]: https://github.com/dotnet-state-machine/stateless/commit/8933fe58a3d2ab63bdf47f523df0b9639cd65c97
[4.1.0]: https://github.com/dotnet-state-machine/stateless/compare/bb742e8d40ceaacb219695875dfe38670ac77e28...daef9cb2897e18f25e85dd27fb80e549369bdfac
[4.0.0]: https://github.com/dotnet-state-machine/stateless/compare/23624d88e684d9984e5b5fdbc3d4aba601bdd1a4...bb742e8d40ceaacb219695875dfe38670ac77e28
[3.1.0]: https://github.com/dotnet-state-machine/stateless/compare/6aa544c6a5e22b93fbe206513d79e15a3e2ef172...23624d88e684d9984e5b5fdbc3d4aba601bdd1a4
[3.0.1]: https://github.com/dotnet-state-machine/stateless/compare/6c44d2ae69f67606b5d979b2f0e353adccb1913c...6aa544c6a5e22b93fbe206513d79e15a3e2ef172
[3.0.0]: https://github.com/dotnet-state-machine/stateless/compare/4d4cc84bad583eaf8f983edc351179cef40bd093...6c44d2ae69f67606b5d979b2f0e353adccb1913c
