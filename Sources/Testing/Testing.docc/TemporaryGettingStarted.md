# Getting started

<!--
This source file is part of the Swift.org open source project

Copyright (c) 2023 Apple Inc. and the Swift project authors
Licensed under Apache License v2.0 with Runtime Library Exception

See https://swift.org/LICENSE.txt for license information
See https://swift.org/CONTRIBUTORS.txt for Swift project authors
-->

<!-- NOTE: The voice of this document is directed at the second person ("you")
because it provides instructions the reader must follow directly. -->

Start running tests in a new or existing XCTest-based test target.

## Overview

The testing library is not (yet) integrated into Swift Package Manager, but a
temporary mechanism is provided for developers who want to start using it with
their Swift packages.

- Warning: This functionality is provided temporarily to aid in integrating the
  testing library with existing tools such as Swift Package Manager. It will be
  removed in a future release.

To learn how to contribute to the testing library itself, see
[Contributing to `swift-testing`](https://github.com/apple/swift-testing/CONTRIBUTING.md).

### Downloading a development toolchain

A recent **development snapshot** toolchain is required to use the testing
library. Visit [swift.org](https://www.swift.org/download/#trunk-development-main)
to download and install a toolchain from the section titled
**Snapshots — Trunk Development (main)**.

Be aware that development snapshot toolchains are not intended for day-to-day
development and may contain defects that affect the programs built with them.

### Adding the testing library as a dependency

In your package's Package.swift file, add the testing library as a dependency:

```swift
dependencies: [
  .package(url: "https://github.com/apple/swift-testing.git", branch: "main"),
],
```

To ensure that your package's deployment targets meet or exceed those of the
testing library, you may also need to specify minimum deployment targets for
macOS, iOS, watchOS, tvOS, and/or visionOS (depending on which ones your package
can be used with):

```swift
platforms: [
  .macOS("13.0"), .iOS("16.0"), .watchOS("9.0"), .tvOS("16.0"), .visionOS("1.0")
],
```

Then, add the testing library as a dependency of your existing test target:

```swift
.testTarget(
  name: "FoodTruckTests",
  dependencies: [
    "FoodTruck",
    .product(name: "Testing", package: "swift-testing"),
  ]
)
```

### Adding test scaffolding

Add a new Swift source file to your package's test target named
"Scaffolding.swift". Add the following to it:

```swift
import XCTest
import Testing

final class AllTests: XCTestCase {
  func testAll() async {
    await XCTestScaffold.runAllTests(hostedBy: self)
  }
}
```

You can now add additional Swift source files to your package's test target that
contain those tests, written using the testing library, that you want to run
when you invoke `swift test` from the command line or click the
Product&nbsp;&rarr;&nbsp;Test menu item in Xcode.

### Configuring the environment

#### Configuring the command-line

When running macOS, the system will use the Swift toolchain included with Xcode
by default. To instruct the system to use the development toolchain you just
installed, enter the following command to configure the current command-line
session:

```sh
export TOOLCHAINS=swift
```

#### Configuring Xcode

In Xcode, open the **Xcode** menu, then the Toolchains submenu, and select the
development toolchain from the list of toolchains presented to you&mdash;it will
be presented with a name such as "Swift Development Toolchain 2023-01-01 (a)".

### Running tests

Navigate to the directory containing your package, and either run `swift test`
from the command line or click the Product&nbsp;&rarr;&nbsp;Test menu item in
Xcode. You're done!

Tests will run embedded in an `XCTestCase`-based test function named
`testAll()`. If a test fails, `testAll()` will report the failure as its own.

## Topics

- ``XCTestScaffold``
