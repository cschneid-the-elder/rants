# IBM COBOL CALLs: Static, Dynamic, and Tradeoffs

The COBOL CALL statement is typically how control is transferred from one compile unit to another.  The program that executes the CALL statement is referred to as the _calling program_ and the program that is invoked by the CALL statement is referred to as the _called program_.  The called program need not be written in COBOL, it may be Assembler, C, FORTRAN, or PL/I.

## Static CALLs

Static CALLs are characterized by the calling program and the called program both being physically contained in the executing program object.  Static calls are typically coded as...

       ID Division.
       Program-ID. AGBELL.
       Environment Division.
       Data Division.
       Procedure Division.
           CALL 'WATSON'  *> a static call
           GOBACK.

...with the `NODYNAM` option in effect at compile time.  This generates code that will cause the binder (in ancient times known as the linkage editor) to `INCLUDE WATSON` in the program object AGBELL.

## Dynamic CALLs

Dynamic CALLs can be coded two different ways.  The first looks identical to a static call...

       ID Division.
       Program-ID. AGBELL.
       Environment Division.
       Data Division.
       Procedure Division.
           CALL 'WATSON'  *> a dynamic call if DYNAM is in effect
           GOBACK.

...but with the `DYNAM` option in effect at compile time.  The second looks a bit different, and can take a number of forms...

       ID Division.
       Program-ID. AGBELL.
       Environment Division.
       Data Division.
       Working-Storage Section.
       01  CONSTANTS.
           05  MYNAME        PIC X(008) VALUE 'AGBELL'.
           05  PGM-WATSON    PIC X(008) VALUE 'WATSON'.
       Procedure Division.
           CALL PGM-WATSON  *> a dynamic call
           GOBACK.

...regardless of whether the `DYNAM` or the `NODYNAM` option is in effect at compile time.

One can get quite creative with the dynamic CALL constructs...

       ID Division.
       Program-ID. MOYA.
       Environment Division.
       Data Division.
       Working-Storage Section.
       01  CONSTANTS.
           05  MYNAME        PIC X(008) VALUE 'MOYA'.
           
       01  CALLED-PROGRAMS.
           05  PGM-AERYN     PIC X(008) VALUE 'AERYN'.
           05  PGM-CRICHTON  PIC X(008) VALUE 'CRICHTON'.
           
       01  WORK-AREAS.
           05  PGM-TO-CALL   PIC X(008) VALUE SPACES.
           
       Procedure Division.
           MOVE PGM-AERYN TO PGM-TO-CALL
           PERFORM 0100-CALL
           MOVE PGM-CRICHTON TO PGM-TO-CALL
           PERFORM 0100-CALL
           GOBACK.
           
       0100-CALL.
           CALL PGM-TO-CALL
           .
  
...or...

       ID Division.
       Program-ID. MOYA.
       Environment Division.
       Data Division.
       Working-Storage Section.
       01  CONSTANTS.
           05  MYNAME        PIC X(008) VALUE 'MOYA'.
           
       01  CALLED-PROGRAMS.
           05  PGM-TO-CALL   PIC X(008) VALUE SPACES.
             88  PGM-AERYN              VALUE 'AERYN'.
             88  PGM-CRICHTON           VALUE 'CRICHTON'.
           
       01  WORK-AREAS.
           
       Procedure Division.
           SET PGM-AERYN TO TRUE
           PERFORM 0100-CALL
           SET PGM-CRICHTON TO TRUE
           PERFORM 0100-CALL
           GOBACK.
           
       0100-CALL.
           CALL PGM-TO-CALL
           .
  
...or even...

       ID Division.
       Program-ID. CHIANA.
       Environment Division.
       Data Division.
       Working-Storage Section.
       01  CONSTANTS.
           05  MYNAME        PIC X(008) VALUE 'CHIANA'.
           05  ABEND-DUMP    PIC 9(008) COMP-5 VALUE 1.
           
       01  WORK-AREAS.
           05  ABEND-CODE    PIC 9(008) COMP-5 VALUE 0.
           05  KEY-VALUE     PIC X(008) VALUE SPACES.
           05  PGM-TO-CALL   PIC X(008) VALUE SPACES.

       EXEC SQL INCLUDE SQLCA END-EXEC.

       Linkage Section.
       01  PARM.
           05  PARM-LENGTH   PIC S9(004) COMP.
           05  PARM-VALUE    PIC X(100).

       Procedure Division Using PARM.
           IF PARM-LENGTH > LENGTH OF KEY-VALUE
           OR PARM-LENGTH = 0
               DISPLAY 'PARM length must be <= ' LENGTH OF KEY-VALUE
                   ' and > 0'
               MOVE 1 TO ABEND-CODE
               CALL 'CEE3ABD' USING 
                   ABEND-CODE
                   ABEND-DUMP
               END-CALL
           END-IF
           
           MOVE PARM-VALUE(1:PARM-LENGTH) TO KEY-VALUE
           
           EXEC SQL
               SELECT PGM
               INTO   :PGM-TO-CALL
               FROM   PGMTABLE
               WHERE  KEY = :KEY-VALUE
           END-EXEC
           
           IF SQLCODE NOT = 0
               DISPLAY 'Unexpected SQLCODE = ' SQLCODE
               MOVE 2 TO ABEND-CODE
               CALL 'CEE3ABD' USING 
                   ABEND-CODE
                   ABEND-DUMP
               END-CALL
           END-IF
           
           PERFORM 0100-CALL
           GOBACK.
           
       0100-CALL.
           CALL PGM-TO-CALL
           .

...where the name of the called program is not contained within the calling program at compile time.  Though not shown here, one might imagine a framework of programs, all with the same calling parameters, called for different business purposes.

## Tradeoffs

### Performance

IBM documents performance considerations for dynamic CALLs.  When a statically bound executable is brought into memory, all called programs are contained therein.  As these subprograms are CALLed, there is no additional overhead involved in bringing them into memory, they're already there.  Additionally, the bootstrap routines are only loaded once for a statically bound executable; individually bound dynamically called subprograms each contain a copy of the bootstrap routines, thus using slightly more memory.

This may not be as important as it sounds.  Yes, there is extra overhead in loading dynamically called programs into memory when they are CALLed, but this is only going to happen on the first CALL (unless CANCEL is coded, in which case you have an initialization problem which has been solved by killing it with fire instead of using Local-Storage as should have been done).  If you have many subprograms each CALLed once in a run unit, then there is likely a difference in performance but whether that difference is measurable is debatable.

IBM also documents that the _CALL literal_ syntax (with the `DYNAM` compile option) performs better than the _CALL identifier_ syntax.

Note that CICS does not allow the _CALL literal_ syntax with the `DYNAM` compile option.  The CICS runtime routine CALLs that are substituted (by either the precompiler or the integrated translator) for EXEC CICS _do something_ END-EXEC commands are required to be static CALLs.  It is unclear as of this writing (late 2020) if a developer can prefix EXEC CICS _do something_ END-EXEC with CALLINTERFACE STATIC and suffix it with CALLINTERFACE DYNAMIC to work around this restriction.

### Portfolio Management

IBM documents that dynamic CALLs are a better way to manage complex applications.  My personal experience is that this is true.

In an application portfolio making use of static CALLs, changes to called programs require rebinding all executables calling the changed called programs.  Absent a tool to manage this process, some executables are invariably missed.  Even with the use of such a tool, deadlines and internal conflicts can cause the same effect.

These were lessons learned well during Y2K remediation.  Shops discovered old versions of called programs, statically bound into executables, the source code for which no longer existed, and where the called program had evolved to the point where updating the previously left behind callers involved more work than anyone imagined.

Dynamic CALLs also solve the problem of determining which version of a called program is being CALLed.   There is only one.

### Application Portfolio Analysis

#### Static Code Analysis

Static code analysis looks at the source code. The process has no knowledge of what happens as the code executes. For purposes of application portfolio analysis, this results in some representation of what could happen, not what does happen. Consider...

           IF A = B
               CALL 'ZHAAN'
           END-IF
            
...static analysis has no way of knowing if A is never equal to B due to some business rule and thus subprogram ZHAAN is never called.

Dynamic CALLs can make static code analysis difficult or impossible.  Consider the CHIANA example above.  The called program name appears nowhere in the source code.

#### Runtime Behavior Analysis

Runtime behavior analysis looks at what actually happens as code executes, often through some form of instrumentation. For purposes of application portfolio analysis, this results in some representation of what _does_ happen, not what _could_ happen, in that run. Consider...

           IF A = B
               CALL 'ZHAAN'
           END-IF
            
...runtime behavior analysis only knows that A was never equal to B _in any of the runs analyzed_ and thus subprogram ZHAAN was never called. No assertion can be made that subprogram ZHAAN will never be called.

#### Both Have Their Uses

A combination of both static code analysis and runtime behavior analysis is necessary in order to understand an application portfolio. Simply noting that a given program is never executed is not prima facie evidence that it is obsolete. Maybe that program is only executed when an error condition occurs; exception processing should, after all, be exceptional.

## So, Now What?

Dynamic CALLs tend to lead to less staff time spent on maintenance, troubleshooting, and impact analysis.

Your shop may have standardized on static CALLs long ago and continues to use them due to organizational momentum.  If you want to try, and keep in mind this may be tilting at windmills, you might be able to persuade those in authority by pointing them at the IBM documentation indicating dynamic CALLs are preferable...

 >> With dynamic CALLs (call literal with DYNAM or call identifier), each subprogram is link-edited separately from the others. They are brought into storage only if they are needed. This is the better way of managing complicated applications.
 
...which is currently [here](https://www.ibm.com/docs/en/cobol-zos/6.3?topic=performance-using-calls) and can be navigated to from the IBM Documentation for COBOL table of contents via Home > Enterprise COBOL for z/OS 6.3.0 > Performance Tuning Guide > COBOL and LE features that affect runtime performance > Using CALLs.

My personal opinion is that performance benefits are more likely gained via [tuning Language Environment options](https://github.com/cschneid-the-elder/rants/blob/master/apps-tuning-with-le.md).

Any analysis of your application portfolio, whether it be via runtime monitoring, static code analysis, or both, must take into account edge cases where neither technique gives the whole picture.  Software tools can help architects, analysts, and developers to understand an unfamiliar code base, but ultimately that understanding is the result of your own brainwork.
