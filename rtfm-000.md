I blame IBM.  The mainframe has such amazing backward compatibility that no one needs to read IBM's own documentation regarding what's changed because all the old stuff still works.

If IBM would just break things, people would be forced to read their documentation and learn what's new and different and _better_ and the mainframe world would be a better place.

You can do 31-bit I/O.  It's an option on the Assembler macros.  This is huge for eliminating below the line constraints.

You never looked because the old ways just kept working.

z/OS _is_ Unix.  You've got all those wonderful Unix text processing utilities available to you, along with free third-party stuff like Perl.  Wonderful stuff for digging into your libraries of control cards and source code, looking for old-school stuff that no longer needs to be so constrained, like 24-bit code from the 1970s _that just keeps working_.

You've been avoiding Unix System Services because it's weird and you don't need it because you've got ISRSUPC and if ISRSUPC can't do the job then the job doesn't need to be done.

Have you _looked_ at the JCL Reference?  I mean, if you're still coding COND parameters there's no hope for you, but if you haven't given the manual a skim-through since IF statements came about in the last decade of the previous century then IBM has some surprises for you...  In-stream data in cataloged PROCs, the NOTIFY statement, the SCHEDULE statement.  Good, useful stuff.

You don't bother because 1970s style JCL was good enough for your father and his father before him and so it's good enough for you.

COBOL has conditional compilation now.  Which means if you have dual-purpose CICS and batch modules that need _slightly_ different behavior at run time you can do this in a single source code member.  And you can have a formatted map of your storage, including your variable names and their values, in case of an abend _without_ the overhead of loading those symbols at run time.  Also, you can generate and parse JSON.

You're still coding as if it were 1975 and OS/VS COBOL was still shiny and new.

CICS now has an API for multithreading your transactions.  If you've got a transaction that, e.g., accesses more than one independent web service then you can run them in parallel and save on response time.

You haven't looked.  No one does.

_For Hollerith's sake, IBM publishes a Summary of Changes for each z/OS element, how can you not look at that when there's an upgrade?_

Have you looked beyond the IBM documentation at what's available?  No, you're blissfully unaware that there's a Swift compiler and Python and NPM and git and...

Why do I bother.  Mainframes are being replaced by significantly less reliable, significantly less performant, significantly less secure platforms.  In part, because you're not paying attention.

Because IBM doesn't break things.  Apple does.  Microsoft does.  Google does.  But not IBM.  And so here we are.

This is why you can't have nice things:  __You don't want them.__  You prefer stuff that breaks at every major version change, stuff that's barely secure, stuff that grinds to a halt because of a badly performing regex.

Now get off my lawn, I'm fatigued from shaking my cane at the lot of you.
