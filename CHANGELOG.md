# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased] - 2021-3-3

### Added

### Changed

### Deprecated

### Removed

### Fixed

### CI/CD


## [2.0.1] - 2021-3-3

### Changed
* Changed the tag used to pull the base docker image from `latest`
  to the specific version number that is the latest. The reason for this change
  is to ensure that we have the opportunity to test against updates to
  the base image before such changes affect releases. Using the `latest`
  tag when pulling the base image runs the risk of a change in the base
  image breaking the action (although this risk is small).

### Fixed
* Fixed a bug related to permissions on the badges directory if it 
  didn't already exist prior to running the action. Bug only appeared to
  exhibit itself if the `jacoco-badge-generator` was used in combination with
  version 3.6 or later of the `peter-evans/create-pull-request` action, and only
  if the badges directory didn't already exist. This bug is now resolved.


## [2.0.0] - 2021-2-15

### Compatibility Notes
* If you are upgrading from an earlier version, and if 
  you were not using the `jacoco-badge-file` input (deprecated 
  since v1.2.0) to change the default location and name of the 
  badge file, then you can simply upgrade to v2.0.0 without need 
  to make any other changes to your workflow file.
* If you have been using the deprecated `jacoco-badge-file` input 
  to change the default location and name of the badge file, then 
  you will need to instead use the `badges-directory` and 
  the `coverage-badge-filename` inputs.

### Changed
* The documentation has been significantly revised to provide more 
  detail on the JaCoCo coverage metrics that are supported by 
  the jacoco-badge-generator.

### Removed
* Removed the previously deprecated input `jacoco-badge-file`.


## [1.2.1] - 2021-2-11

### Fixed
* Corrected division by zero error in the case when there are 
  either no instructions (e.g., running tests on an initially 
  empty class) or no branches (e.g., no if statements or switch 
  statements, etc). In such cases, badge generator will now 
  compute 100% coverage (e.g., if there aren't any instructions 
  to cover, your tests must have covered all 0 of the instructions).


## [1.2.0] - 2021-2-8

### Added
* Generation of a branches coverage badge (in addition to 
  the existing overall coverage badge).
* Inputs for finer grained control over the behavior of the 
  action (e.g., for controlling name and locations of generated 
  badges, as well as for controlling which badges are generated). 
  The default values for all of the new inputs are consistent 
  with the behavior of the previous release.

### Deprecated
* The `jacoco-badge-file` input is deprecated. In this release 
  it still functions as in prior releases, but it will be removed 
  in the next release. Users of the action should instead use the 
  combination of the new inputs `badges-directory` and 
  `coverage-badge-filename`. This change was made to simplify 
  configuration of badge file names now that the action generates 
  multiple badges.


## [1.1.0] - 2021-2-5

### Added
* An additional action output for the percentage of branches 
  covered. A future release will provide an option to generate 
  an additional badge for this.


## [1.0.0] - 2020-10-21

### Initial release
* The jacoco-badge-generator GitHub Action parses a `jacoco.csv` 
  from a Jacoco coverage report, computes the coverage percentage, 
  and generates a badge to provide an easy to read visual summary 
  of the code coverage of your test cases. The badge that is 
  generated is inspired by the style (including color palette) of 
  the badges of Shields.io, however, the badge is entirely 
  generated within the jacoco-badge-generator GitHub Action, 
  with no external calls.