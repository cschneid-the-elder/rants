Presented as an object lesson in how JCL can be constructed in a non-onerous fashion.

In the waning years of the previous century, we were divesting ourselves of a homegrown source/executable management system in favor of a commercial product.  This served as a triggering event for a number of other endeavors.

Our practice, since the inception of the shop in the late 1960s, was to have production code in the linklist and to STEPLIB to non-production code.  With the advent of DB2 in the late 1980s our practice changed so job steps accessing DB2 would always STEPLIB, explicitly looking for either production or non-production.  This was in preparation for the DB2 upgrade process where the DB2 system code would not be the same in non-production as it was in production.

The ensuing decade brought a number of other changes, ultimately resulting in the construction of STEPLIB concatenations becoming an arcane art.  Thankfully, a solution presented itself in the JCL INCLUDE statement.

In relatively short order all STEPLIBs were encapsulated in JCL INCLUDE members whose names were parameterized to indicate production or one of our non-production environments.  We did something similar with SYSOUT, SYSPRINT, etc.

The end result was our JCL became uncluttered, containing only business-related DD statements.

Except for control statements, e.g. SORT statements.  There we made the mistake of having our non-production environments contain only the members which had changed, and picking up production via concatenation.  Absent this, we could have tested by simply specifying a parameter indicating the environment in which we chose to execute.

So it's possible to set up your execution environments such that the development staff are testing their code changes instead of their ability to construct JCL that hopefully tests their changes, and it's possible for your development staff to submit JCL changes that actually resemble what the production workflow staff will be scheduling.

No additional products required.

Some samples follow.

This does presume a JCLLIB statement following the JOB statement, listing the libraries from which INCLUDE statements retrieve specified members.

First, let's admit that we all just copy those SYSOUT DDs from one job to the next.  How about, instead of copying them, we INCLUDE them?

Create a member called SYSOUT in a shared JCL INCLUDE library...

    //SYSOUT   DD  SYSOUT=&OUTCLASS
    //SYSPRINT DD  SYSOUT=&OUTCLASS
    //CEEDUMP  DD  SYSOUT=&DMPCLASS
    //SYSUDUMP DD  SYSOUT=&DMPCLASS

...and we'll get to that a bit later.

Let us posit the existence of a set of environments...

 + D - Development.  The application developers' playground, abends are expected here.  An alternative name might be Unit Test.
 + S - System Test.  This is where application developers determine if their code plays well with others.  An alternative name might be Integration Test.  Abends should be less frequent here.
 + A - Acceptance.   The end users' and/or QA testers' playground.  Abends here need investigation.
 + P - Production.   The real world.

Let us further posit a set of execution libraries...

 + DEVT.LOADLIB
 + SYST.LOADLIB
 + ACPT.LOADLIB
 + PROD.LOADLIB

...where DEVT.LOADLIB contains only those executables currently being worked upon, SYST.LOADLIB contains only those executables determined to have passed unit testing and to be ready to be integrated, ACPT.LOADLIB contains only those executables having passed integration testing and ready for QA or end user acceptance testing, and PROD.LOADLIB contains all executables except those that are brand new and have yet to pass all tests.

Why?  Why not simply have each library include all executables?  Because you probably get billed for DASD usage.

So a STEPLIB for Development testing should look like this...

    //STEPLIB  DD  DISP=SHR,DSN=DEVT.LOADLIB
    //         DD  DISP=SHR,DSN=SYST.LOADLIB
    //         DD  DISP=SHR,DSN=ACPT.LOADLIB
    //         DD  DISP=SHR,DSN=PROD.LOADLIB

...because, if an executable is using dynamic CALLs, the STEPLIB needs to contain every executable being called, and every executable those executables call.  Put another way, let's say I'm testing executable CRICHTON in Development and it calls executable AERYN which is currently in Acceptance and DARGO which is in System Test.  All three of those executables call executable MOYA which is in Production.

A STEPLIB for System Testing should look like this...

    //STEPLIB  DD  DISP=SHR,DSN=SYST.LOADLIB
    //         DD  DISP=SHR,DSN=ACPT.LOADLIB
    //         DD  DISP=SHR,DSN=PROD.LOADLIB

...because if you're testing DARGO you don't want that flaky code I'm not done with that's in Development.

Likewise, an Acceptance STEPLIB should look like this...

    //STEPLIB  DD  DISP=SHR,DSN=ACPT.LOADLIB
    //         DD  DISP=SHR,DSN=PROD.LOADLIB

...because, let's face it, that DARGO module isn't ready for Acceptance testing yet but AERYN is.

A Production STEPLIB should of course look like this...

    //STEPLIB  DD  DISP=SHR,DSN=PROD.LOADLIB

Each of these STEPLIBs is a separate member in our JCL INCLUDE library...

 + SLOADD
 + SLOADS
 + SLOADA
 + SLOADP

...so we can write JCL that looks like this...

    //FARSCAPE EXEC PGM=CRICHTON
    //             INCLUDE MEMBER=SLOAD&AENV
    //             INCLUDE MEMBER=SYSOUT
    //INPUT01  DD  DISP=OLD,DSN=&AENV..CRICHTON.INPUT01
    //OUTPUT01 DD  DISP=(NEW,CATLG,DELETE),
    //             DSN=&AENV..CRICHTON.OUTPUT01(+1),
    //             AVGREC=K,
    //             LRECL=80,
    //             RECFM=FB,
    //             SPACE=(80,(10,10),RLSE)

...and write it once.  Execution is accompanied by appropriate SET statements or setting of JCL symbols on the EXEC PROC statement.

    // SET AENV=D     Application Environment
    // SET OUTCLASS=* Output class
    // SET DMPCLASS=K Core Dumps

This technique is extensible.  You can have a DB2ENV parameter for when you use the call attach facility executables accessing DB2...

    //TALYN    EXEC PGM=IKJEFT1B
    //             INCLUDE MEMBER=SLOAD&AENV
    //             INCLUDE MEMBER=DB2SYS&DB2ENV
    //         DD  DISP=SHR,DSN=&AENV..CTLCARDS(CRAIS)
    //             INCLUDE MEMBER=SYSOUT
    //OUTPUT01 DD  DISP=(NEW,CATLG,DELETE),
    //             DSN=&AENV..CRAIS.OUTPUT01(+1),
    //             AVGREC=K,
    //             LRECL=80,
    //             RECFM=FB,
    //             SPACE=(80,(10,10),RLSE)

...where our JCL INCLUDE library has a set of members...

 + DB2SYSD
 + DB2SYSS
 + DB2SYSA
 + DB2SYSP

...containing a SYSTSIN DD...

    //SYSTSIN  DD  DISP=SHR,DSN=P.CTLCARDS(DB2SYSD) Development

...where P.CTLCARDS(DB2SYSD) looks like...

     DSN SYSTEM(D01D)
 
...or whatever the name of your Development DB2 subsystem is, and the CRAIS member looks like...

     RUN PROGRAM(CRAIS) PLAN(CRAIS)
 
...or however you have your plans and programs and packages organized for execution.

And of course you have a DB2SYS member for each of your DB2 subsystems And your SLOAD&AENV members include the DB2 load libraries.

Now, when the name(s) of your DB2 subsystems change (and ours did), you aren't chasing down hundreds or thousands of places to make that change.

While it's possible to have differing numbers of DB2 subsystems and application environments, it's easiest if there are the same number.

Our practice, after a few attempts at trying to game the system, was to have a matched one-for-one set of environments for applications, CICS, DB2, and MQ.

