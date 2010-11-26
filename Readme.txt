Kiwi
----

Kiwi is open source software. You may freely distribute it under the terms of
the license agreement found in License.txt.

Simple BDD for the iPhone and iPad
----------------------------------
Kiwi is a Behavior Driven Development library for iPhone and iPad development.
The goal is to provide a BDD library that is exquisitely simple to setup and use.

Quick Setup
-----------

For non-library usage:
1. Add a Cocoa Touch 'Unit Test Bundle' target to your Xcode project. This is your spec target.
2. Optional: Set the compiler for the spec target to LLVM compiler 1.x if available.
3. Add the Kiwi/Kiwi folder to the spec target.
4. Add a spec file to the spec target (example below).
5. Build the spec target on the Simulator to run the spec.

To use as a Cocoa framework (OS X development):
1. Compile the KiwiCocoa target.
2. Move the KiwiCocoa.framework to an appropriate location; typically ~/Library/Frameworks.
3. Add a Cocoa 'Unit Test Bundle' 
3. Add the KiwiCocoa.framework framework to the spec target.
4. Add a spec file to the spec target (example below).
5. Build the spec target to run the spec.
//----------------------8<------------------------------

#import "Kiwi.h"

SPEC_BEGIN(TestSpec)

describe(@"A simple test", ^{
    it(@"works", ^{
        // Try changing the should's to shouldNot's, and vice-versa to see
        // failures in action.

        id anArray = [NSArray arrayWithObject:@"Foo"];
        [[anArray should] contain:@"Foo"];
        [[anArray shouldNot] contain:@"Bar"];

        [[theValue(42) should] beGreaterThan:theValue(10.0f)];
        [[theValue(42) shouldNot] beLessThan:theValue(20)];

        id scannerMock = [NSScanner mock];
        [[scannerMock should] receive:@selector(setScanLocation:)];
        [scannerMock setScanLocation:10];

        [scannerMock stub:@selector(string) andReturn:@"Unicorns"];
        [[[scannerMock string] should] equal:@"Unicorns"];

        [[theBlock(^{
            [NSException raise:NSInternalInconsistencyException format:@"oh-oh"];
        }) should] raise];
    });
});

SPEC_END

//----------------------8<------------------------------

Learn more at http://www.kiwi-lib.info
