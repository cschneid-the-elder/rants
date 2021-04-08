## Tuning Mainframe Applications with Language Environment Options

### TL;DR

If you're using LE in a job step, start with an LE-conforming module.  Specify ALL31(ON) and CBLPSHPOP(OFF) when you can.  Specify the CICS AUTODST(ON) SIT option.  Use the LE storage report (RPTSTG(ON)) to get values to use in HEAP and STACK _initSize_ parameters.  Use the defaults for STORAGE if you can, seriously don't specify a value for _dsaAllocValue_ other than NONE.  For PL/I and/or C/C++ applications take a look at HEAPPOOLS.  You may want to implement custom CEEUOPTs for performance critical CICS transactions.

### Prefatory Remarks
 
Much of this is greatly condensed from SHARE presentations by IBM staff, notably Tom Petrolino, John Monti, Mary Astley, and Mark Picard, and from the IBM documentation.  This material is general in nature; there are specific cases that I'm not covering (_cough_ CEEPIPI _cough_) and I cannot stress enough that [_there is no substitute for reading the documentation_](https://github.com/cschneid-the-elder/rants/blob/master/mainframe-documentation-000.md).

If you are looking for hard numbers on exactly how much savings you can expect via LE tuning, _stop reading now_.  This document is not for you, it is for technical staff who want to save CPU and for reasons best known to themselves cannot change application code.

Also, there's nothing here about IMS because my experience is limited to modifying one application in 1987.

### History

In the old days, before the surface of the earth had cooled, every language had its own runtime routines.  This worked fine until you tried to make a frankenmodule out of COBOL and PL/I, when the disparate runtime routines didn't get along so well in a single run unit.

So IBM, with input from some of its customers, set about designing a common runtime library to be used by all high level languages.  With very little effort, LE is usable by Assembler too.

### How it Works

LE does a lot of work for you...

 + Initialization
 + Storage management
 + Condition Handling
 + Message services
 + Date/Time services
 + Math functions
 + Termination

...we're going to mostly concentrate on storage management.

When your application requests memory, e.g. for COBOL Working-Storage, C calls to the malloc(), calloc(), and realloc() functions, PL/I variables with storage classes CONTROLLED or BASED, or calls to the CEEGTST LE Callable Service, that memory comes from the LE _heap_.

COBOL Local-Storage, and C or PL/I automatic variables come from from the LE _stack_.

Allocation of the heap and stack are controlled by LE runtime options.

### HEAP(...)

HEAP(_initSize_,_incrSize_,_loc_,_keepOrFree_,_initSize24_,_incrSize24_)

 + _initSize_ is how big of an initial chunk of storage to obtain
 + _incrSize_ is how big of a subsequent chunk of storage to obtain if the initial chunk proves to be insufficient
 + _loc_ is ANYWHERE, ANY, or BELOW to indicate whether to obtain storage below the 16M line or anywhere storage is available
 + _keepOrFree_ is KEEP or FREE to indicate what to do with a chunk of storage no longer in use
 + _initSize24_ is how big of an initial chunk of storage to obtain for AMODE 24 applications that specify ANYWHERE or ANY for _loc_
 + _incrSize24_ is how big of a subsequent chunk of storage to obtain for AMODE 24 applications that specify ANYWHERE or ANY for _loc_ if the initial chunk proves to be insufficient

 - Default as of z/OS 2.4 for non-CICS is HEAP(32K,32K,ANYWHERE,KEEP,8K,4K).
 - Default as of z/OS 2.4 for CICS is HEAP(4K,4080,ANYWHERE,KEEP,4K,4080).

Your shop may have altered these defaults.  You can see what the defaults are for batch by specifying the RPTOPTS(ON) LE runtime option.  There are a number of different ways to specify LE runtime options, we'll get to that later.

### STACK(...)

STACK(_initSize_,_incrSize_,_loc_,_keepOrFree_,_dsInitSize_,_dsIncrSize_)

 + _initSize_ is how big of an initial chunk of storage to obtain
 + _incrSize_ is how big of a subsequent chunk of storage to obtain if the initial chunk proves to be insufficient
 + _loc_ is ANYWHERE, ANY, or BELOW to indicate whether to obtain storage below the 16M line or anywhere storage is available
 + _keepOrFree_ is KEEP or FREE to indicate what to do with a chunk of storage no longer in use
 + _dsInitSize_ is how big of an initial chunk of storage to obtain in a XPLINK environment
 + _dsIncrSize_ is how big of a subsequent chunk of storage to obtain if the initial chunk proves to be insufficient in an XPLINK environment
 
XPLINK is a specialized topic and you can refer to the IBM documentation if you're interested.  It doesn't come into play for purposes of this discussion.

 - Default as of z/OS 2.4 for non-CICS is STACK(128K,128K,ANYWHERE,KEEP,512K,128K).
 - Default as of z/OS 2.4 for CICS is STACK(4K,4080,ANYWHERE,KEEP,4K,4080).

Your shop may have altered these defaults.  You can see what the defaults are for batch by specifying the RPTOPTS(ON) LE runtime option.  There are a number of different ways to specify LE runtime options, we'll get to that later.

### STORAGE(...)

STORAGE(_heapAllocValue_,_heapFreeValue_,_dsaAllocValue_,_reserveSize_)

 + _heapAllocValue_ is the value to set HEAP storage to after it is allocated, or NONE to leave it uninitialized
 + _heapFreeValue_ is the value to set HEAP storage to before it is freed, or NONE to leave it as the application left it
 + _dsaAllocValue_ is the value to set STACK storage to after it is allocated, or CLEAR to set to binary zeroes, or NONE to leave it uninitialized
 + _reserveSize_ is amount of storage for LE to reserve in the event of an out-of-storage condition

 - Default as of z/OS 2.4 for non-CICS is STORAGE(NONE,NONE,NONE,0K).
 - Default as of z/OS 2.4 for CICS is STORAGE(NONE,NONE,NONE,0K).

Your shop may have altered these defaults.  You can see what the defaults are for batch by specifying the RPTOPTS(ON) LE runtime option.  There are a number of different ways to specify LE runtime options, we'll get to that later.

Setting _dsaAllocValue_ to any value other than CLEAR or NONE incurs __extremely high overhead__.

### ALL31(...)

ALL31(_onOrOff_)

 + _onOrOff_ ON indicates if this all code is AMODE(31) while OFF indicates some AMODE(24) code will be executed
 
Seriously, if you have 24-bit code still running, _why?_

### CBLPSHPOP(...)

CBLPSHPOP(_onOrOff_)

 + _onOrOff_ ON indicates an implicit EXEC CICS PUSH HANDLE will be issued prior to calling any COBOL subroutine in CICS and an implicit EXEC CICS POP HANDLE will be issued on return from calling any COBOL subroutine, OFF indicates no such PUSH or POP HANDLE will be issued

 - This option is ignored outside of CICS.
 - Default value for CICS is CBLPSHPOP(ON).

The purpose of CBLPSHPOP is to avoid compatibility problems when calling COBOL subroutines that contain CICS CONDITION, AID, or ABEND condition handling commands.  Setting CBLPSHPOP(OFF) incurs less overhead, particularly in applications with many repeated calls to COBOL subroutines.

### HEAPPOOLS(...)

HEAPPOOLS(_onOrOffOrAlign_,_cellSize|(cellSize,poolCount)_,_percentage_)

 + _onOrOffOrAlign_ ON indicates the heap pools algorithm is to be used, OFF indicates the heap pools algorithm is not to be used, ALIGN indicates the heap pools algorithm is to be used and that the storage for cells less than 248 bytes in size do not cross a cache line
 + _cellSize_ is the size of a single cell in a heap pool
 + _poolCount_ is the number of pools of this cell size to create
 + _percentage_ is the percent size of the LE _heap_ allocated to the cell pool

HEAPPOOLS uses a storage management algorithm which improves the performance of PL/I and C/C++ multithreaded applications which frequently obtain heap storage.

I'm only mentioning this so it's not forgotten, unfortunately my experience is inadequate for a detailed discussion.  Please refer to the documentation, or to Mary Astley's excellent session 8210 from SHARE February 2008.  You might be able to get a copy from IBM if you can't get one from SHARE.

### What Are Your LE Runtime Options?

For batch, run a batch program that uses LE.  Any COBOL program will do, preferably one that doesn't do anything much.

Specify `PARM='/RPTOPTS(ON)'` on the EXEC statement, or add a DD with the DDNAME CEEOPTS.

    //CEEOPTS  DD  *
    RPTOPTS(ON)

For CICS, I found the easiest way is to look at an abend.  When LE writes a core dump it includes the runtime options.  You can use the CLER transaction if you're authorized, but you probably aren't.  If you happen to be authorized for CLER, _be sure to change nothing_ because changing LE runtime options in a CICS region without the approval of the Systems Programmer can be career limiting.

Different CICS regions can have different LE runtime options.

### Specifying LE Runtime Options

You've already seen two ways to specify LE runtime options, via the `PARM=` parameter on the EXEC statement in JCL (though there's a bit of a trick to it).  The LE options are not options to be passed to your program, they're to be passed to the runtime.  The notation to indicate this is, _for COBOL_, follow any parameters being passed to your program with a slash and add the LE runtime options after that.  For PL/I the runtime options come first, followed by a slash, followed by any parameters being passed to the program.  Obviously this method limits the number of LE runtime options because PARM data cannot exceed 100 bytes.

You can use the CEEOPTS DD method, which does not suffer from the PARM data limitation.

You can use a CEEUOPT CSECT, assembled from the CEEXOPT macro and statically bound into your program object.  This is very useful if your application requires specific LE runtime options.

The C/C++ compiler provides `#pragma runopts()` construct.  The PL/I compiler provides the `PLIXOPT` construct.

IBM documents other mechanisms via which Systems Programmers specify region and LPAR LE runtime option defaults, but these aren't available to application programmers.

### LE Storage Report

Run your application, specifying the LE runtime option RPTSTG(ON).  You will get a report showing you how much _heap_ and _stack_ storage your application used.  There will be recommendations as to what to specify for _initSize_ for heap and stack, and what to specify for HEAPPOOLS _cellSize_.

### Tuning LE Managed Storage

Reduce the "Number of segments allocated" for "HEAP statistics" and "STACK statistics" to 1 by increasing the _initSize_ parameter.

Where the storage report, under "STACK statistics", reads "Maximum used by all concurrent threads" you'll see a number.  If that number is greater than the "Initial size" number, you'll want to increase your STACK _initSize_ parameter to match (LE will round up to the next multiple of 8).

Where the storage report, under "HEAP statistics", reads "Total heap storage used (sugg. initial size)" you'll see a number.  If that number is greater than the "Initial size" number, you'll want to increase your STACK _initSize_ parameter to match (LE will round up to the next multiple of 8).

Really, that's about all there is to it.  For batch.  For CICS, specify the AUTODST(ON) SIT parameter and CICS will tune storage for you - there is a caveat and a mitigation for the caveat in the documentation.

### Tuning Other Things

If you've a mix of COBOL applications in a CICS region, some of which use EXEC CICS HANDLE calls and some that don't, you might have to specify CBLPSHPOP(ON) for compatibility reasons.  But you could bind a custom CEEUOPT specifying CBLPSHPOP(OFF) into applications that are CALL heavy in order to improve performance.

If you use dynamic COBOL CALLs (CALL _identifier_) in CICS, you can avoid some LE overhead that comes with EXEC CICS LINK.  EXEC CICS LINK creates a new LE "enclave" which means a new STACK and HEAP are allocated.  Dynamic calls run in the same LE enclave and thus use the same STACK and HEAP.

Use ALL31(ON) when you can.  Don't turn your world upside down to use it, but use it when you can.

The most efficient way to initialize variables is with what your compiler provides, that's `VALUE` clauses for COBOL.  Head in the direction of not using what STORAGE provides for HEAP initialization, and don't ever set a value for _dsaAllocValue_.

If you don't need to clear storage after programs are done with it, leave the STORAGE _heapFreeValue_ option at NONE.

If your batch job step's initial program is non-LE conforming Assembler, you probably want to either convert that to LE conforming Assembler or write a COBOL stub to call the Assembler program.  It saves on LE setup and teardown.

IBM, per a SHARE requirement, makes available a document covering COBOL tuning.  The most current as of this writing is [here](https://www.ibm.com/support/pages/enterprise-cobol-version-6-release-1-performance-tuning).  For future reference, the naming convention has been COBPFvr.PDF where _v_ is the version number and _r_ is the release number, so COBOL 6.1 would be COBPF61.PDF.

### References

 + SHARE Session 1533 Tuning LE for Performance by Mark Picard, August 2009
 + SHARE Session 8210 Understanding the Language Environment Storage Report by Mary Astley, February 2008
 + SHARE Session 13669 Look What I Found Under The Bar! by John Monti, August 2013
 + SHARE Session 1502 z/OS Language Environment Setup & Customization by Tom Petrolino, August 2009
 + SHARE Session 1551 Making CICS and LE Play Nice Together by Mark Picard, August 2009
 + [IBM Documentation](https://www.ibm.com/docs/en)
