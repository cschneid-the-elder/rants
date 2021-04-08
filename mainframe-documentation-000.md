To my delight, I'm starting to see more and more mention in articles about programming and programmers that the most valuable skill is being able to figure things out for oneself.

Building on [something I wrote earlier](https://github.com/cschneid-the-elder/rants/blob/master/apps-staff-tuning.md), I'd like to point out that [IBM documentation](https://www.ibm.com/docs/en), particularly what is now known as IBM Z (commonly referred to as "mainframe") documentation, is free, detailed, and voluminous.

Learning how to find what you're looking for, and how to understand the particular dialect in which this documentation is written, is essential to managing stress for mainframe staff.  The reference to dialect is to indicate that IBM tends to write documentation enumerating _what_ is possible mostly without providing pragmatic examples of _how_ make use of the features cited.  I value IBM's Knowledge Centers, but their volume could easily be expanded by a third by adding more examples.

Possibly for this reason, people have become accustomed to using Internet search engines to find content.  The problem with doing that is telling a support person that some random page on the Internet said you could do it this way is unlikely to garner sympathy for your position.  

Of course there are exceptions, [Mark Zelden](http://www.mzelden.com/mvsutil.html) and [Lionel Dyck](https://lbdsoftware.com) have web sites which are wonderful sources of information, and certainly the late John Ehrman's book on [z/Architecture Assembler language programming](http://idcp.marist.edu/enterprisesystemseducation/assemblerlanguageresources-1.html) is fantastic.

Before I abandoned the codeface for a seat by the fire, I used to send out links to my shop's development staff in hopes they would bookmark the IBM documentation for the products we used.

I urge you to follow the link above to the IBM documentation, find that which is appropriate to your shop, bookmark it, and become familiar with how it is organized.  Also, keep up on your shop's upgrades; new releases and especially new versions of a product often have new features, and sometimes features are deprecated.

z/OS itself is enormous.  Some helpful tips:

 + JCL is documented under _z/OS MVS_
 + IEBGENER, et. al. are documented under _z/OS DFSMS -> z/OS DFSMSDfp Utilities_
 + Language Environment (LE) is the shared runtime routines and additional utilities for all High Level Languages (HLLs) and includes very handy "callable services"
 + C/C++ is documented in the z/OS Knowledge Center; HLASM, COBOL, and PL/I each have their own Knowledge Center, as do CICS, MQ, DB2, IMS, et. al.

None of these products is small.  Taking the time to learn where and how things are documented will serve you well.
