% Android Testing
% Patrick Sturm
% 24.11.2015

# Agenda

## Agenda

* Introduction into JUnit under Android (very basic)
* A few words on testing in general
* Introduction into espresso
* Example Code

# Introduction

## Introduction - Android Testing

* The Android test framework is build on top of JUnit
* The framework provides Android specific API that we can use to conduct more specialized tests
* In todays session, we are going to look at UI tests, since they are intrinsic to Android, we will not cover regular Unit Testing

## Introduction - "Testing" in general

* The order in which tests execute is not guaranteed
* Test must therefore not depend on one another
* Test must be deterministic and must not rely on other code then the code to be tested
    * use mocks
* Each test must run in a clean environment, reset the context before or after each test (I mean that quite literally!)
* Don't test external dependencies or framework / language fundamentals
    * One can assume that Boolean.TRUE is in fact Boolean.TRUE
* Only test a single thing (I dare to say Unit here, although it's not entirely true) at a time

## Android - Setup - 1

* Before we start:
    * Enable the developer mode on your test device (click "Build Number" several times)
    * Disable all animations:
        * Window
        * Transition
        * Animator

## Android - Setup - 2

* Android uses ```InstrumentationTestRunner```, actually an ```Instrumentation``` to execute ```TestCase```s
* We need to specify which ```InstrumentationTestRunner``` to use, e.g.:
    * android.test.InstrumentationTestRunner
         * For regular applications
    * com.android.test.runner.MultiDexTestRunner
         * For MultiDex applications (applications that exceed the initial Dex method limit of 65536)
    * android.support.test.runner.AndroidJUnitRunner
         * We will be working with this runner (support package!)

## Android - Setup - 3

* Since the time gradle became the primary Android build system, it's customary to provide the InstrumentationTestRunner instance to use within the build file (before Manifest) - It's all the same really
* ```testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"```

## Android - Setup - 4

* We also need to include the following dependencies in our project, include them with ```androidTestCompile```:

```
'junit:junit:4.12'
'com.android.support:support-annotations:23.1.1'
'com.android.support.test:runner:0.4.1'
'com.android.support.test:rules:0.4.1'
'com.android.support.test.espresso:espresso-core:2.2.1'

// optional, moar matchers

'org.hamcrest:hamcrest-library:1.3'

```

## Android - Espresso 1

![Source: https://google.github.io/](../espresso-cheat-sheet.png)

## Android - Espresso 2

* Espresso knows:
    * Matchers - find / (help) inspect views
    * Actions - perform actions on views (e.g. click)
    * Assertions - inspect views
    * Options (adapters only!) - Adapter specific options

## Android - Espresso 3

* onView(MATCHER)/onData(MATCHER) -> perform(ACTION) -> check(ASSERTION)
* onView(MATCHER)/onData(MATCHER) -> check(ASSERTION)

# [Example Code](https://github.com/SphericalElephant/android-example-androidtesting)

## More Resources

* https://google.github.io/android-testing-support-library/
* http://chiuki.github.io/advanced-android-espresso/#/