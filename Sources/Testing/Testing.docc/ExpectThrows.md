# Validating errors and issues in tests

<!--
This source file is part of the Swift.org open source project

Copyright (c) 2023 Apple Inc. and the Swift project authors
Licensed under Apache License v2.0 with Runtime Library Exception

See https://swift.org/LICENSE.txt for license information
See https://swift.org/CONTRIBUTORS.txt for Swift project authors
-->

Validate when and how tested code throws errors.

## Overview

It is often necessary as part of a test to validate that an error is thrown (or
that an error is _not_ thrown.) The testing library provides several overloads
of the `#expect()` and `#require()` macros that can be used to perform these
actions.

The testing library also provides a function, `withKnownIssue()`, that can be
used to mark issues as known. In other words, if a test is known to record an
issue, may record an issue intermittently (a "flaky" test), or tests incomplete
application code, this function can be used to inform the testing library at
runtime not to mark the test as failing when those issues occur.

## Topics

### Validating that errors are thrown

- ``expect(throws:_:performing:)-2j0od``
- ``expect(throws:_:performing:)-1s3lx``
- ``expect(_:performing:throws:)``
- ``require(throws:_:performing:)-8762f``
- ``require(throws:_:performing:)-84jir``
- ``require(_:performing:throws:)``

### Validating that errors are not thrown

- ``expect(throws:_:performing:)-jtjw``
- ``require(throws:_:performing:)-4a80i``

### Recording known issues in tests

- ``withKnownIssue(_:isIntermittent:fileID:filePath:line:column:_:)-4txq1``
- ``withKnownIssue(_:isIntermittent:fileID:filePath:line:column:_:)-8ibg4``
- ``withKnownIssue(_:isIntermittent:fileID:filePath:line:column:_:when:matching:)-3n2cc``
- ``withKnownIssue(_:isIntermittent:fileID:filePath:line:column:_:when:matching:)-5bsda``
- ``Issue``
- ``KnownIssueMatcher``
