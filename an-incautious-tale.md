### An Incautious Tale

In the mid-noughties I was approached by a colleague who had been presented with an assignment to produce 100+ COBOL programs, identical save for the FDs and SELECT clauses.  These were to be used in a project being developed with an I-CASE tool that required flat file I/O to be done in external modules.

My colleague, well versed in Assembler in an OLTP context, asked if there wasn't a way to do this with one Assembler program instead of one COBOL program per flat file.

And so we found a way to introduce modern Assembler techniques to the organization.  Reentrant, LE-conforming, 31-bit (much to everyone's surprise you can do 31-bit QSAM I/O), named USINGs, making use of the IBM Structured Programming Macros, and using Name-Token Services to preserve data between calls.

We learned that LE-conforming Assembler comes with [its own set of rules](https://www.ibm.com/docs/en/zos/2.4.0?topic=considerations-system-services-available-assembler-routines).  We learned about LE Callable Services.  We _learned_.  You'd be surprised what you don't know about the runtime for those applications that run your business.

How did we learn this stuff?  Easy, we _read_.  We read the documentation.  Everyone complains about documentation, but IBM Z's is quite good, and where it isn't you can (and I have) submit requests for clarifications and modifications.  We read [SHARE](https://www.share.org) presentations by John Monti and Tom Petrolino and the late John Ehrman.  I was lucky enough to attend some of those SHARE presentations.  It's worth the trip.  It's worth more than one trip.

So there's just the one program to maintain.  It's got a test harness in case anyone needs to make changes.  Fifteen+ years on, no one has.

Other COBOL applications, unthought-of at the time of this module's creation, found a use for the ability to read files whose record length was unknown until runtime.  Reuse isn't just a benefit of OO languages.

If I had it to do over again, I'd also investigate a single COBOL program calling C runtime functions fopen, fread, fwrite, and fclose, Language Environment making this pretty easy, as pointed out by Steve Comstock of (late, lamented) Trainer's Friend fame.

The point of this tale is that sometimes the best interests of your organization are served by _not_ just doing as you're told.  Take the time to think about the assignment rather than just its deadline.  Managers take note, don't mistake the bit of grit in the oyster for sand in the gears.