If you've been paying attention, you know it's not about [semicolons and curly braces](https://github.com/cschneid-the-elder/rants/blob/master/modernization-and-its-discontents-001.md), nor is it about [rewriting as microservices or APIs or whatnot](https://github.com/cschneid-the-elder/rants/blob/master/modernization-and-its-discontents-002.md), nor is it about [extracting your business rules from your existing applications](https://github.com/cschneid-the-elder/rants/blob/master/modernization-and-its-discontents-003.md), nor is it about [cloudifying your applications](https://github.com/cschneid-the-elder/rants/blob/master/modernization-and-its-discontents-004.md).

So, how _do_ you modernize your mainframe application portfolio?

This application portfolio that you so desperately want to "modernize" is probably (COBOL and/or PL/I) and (CICS or IMS/DC) and (DB2 or IMS/DB).  Likely a bunch of batch procedures too.

The first notion you must disabuse yourself of is that mainframes are not modern.  Current IBM mainframes are 64-bit machines with, well, you can read about the [technical specs](https://www.ibm.com/it-infrastructure/z) if that makes you happy.  Mainframes can run Linux.  Thousands and thousands of instances of Linux, simultaneously and _reliably_.

The second notion you must disabuse yourself of is that CICS and IMS/DC are not modern.  Both of these can function as web application containers.  Applications executing therein can be accessed as web services and can invoke web services.  There are hot failover capabilities built in.

The third notion you must disabuse yourself of is that COBOL and PL/I are not modern.  They are neither object oriented<sup>[1](#f01)</sup> nor functional<sup>[2](#f02)</sup>, they are procedural, but that's a description and not a pejorative. 

There is no "hierarchy" of programming languages from procedural to OO to FP<sup>[3](#f03)</sup>.  These are different styles of programming and programming languages.  Different is not better or worse, it's simply _different._  It's possible a different style is helpful in a given situation; that doesn't make it better but might make it better _in context._

 > Here's something I'm pretty sure most OO and FP people haven't internalized: most business rules are procedural.

Also, COBOL and PL/I natively parse JSON and XML and can generate the same from data structures.

The fourth notion you must disabuse yourself of is that mainframe UIs must be dumb terminal "green screen" UIs.  This hasn't been true since the first 3270 emulators appeared in the 1980s.  Today, developers can use an Eclipse-based "explorer" from IBM and can design applications that communicate with back-end CICS or IMS/DC applications via REST or SOAP<sup>[4](#f04)</sup>.  So your systems of engagement can be as fancy as you like.

 > Here's something else I'm pretty sure has been lost over the past few decades: UIs are not business rules.

The fifth notion you must disabuse yourself of is that RDBMSs and HDBMSs are not modern.  Relational and Hierarchical are conceptual models of data.  Relational models seek to ensure data  is not duplicated, solving the problem of the person with two watches<sup>[5](#f05)</sup>.  In some organizations the business data naturally falls into hierarchies, and for those organizations' IT shops IMS/DB makes sense.  

NoSQL databases (on the mainframe we call it VSAM) remove the requirement for data modeling, speeding up the development process and giving rise to an extraordinary amount of code being written to deal with edge cases not discovered until far too late in the process.  Most mainframe applications' databases have been modeled to reflect and enforce business rules in order to make it impossible for the database to end up in an inconsistent state.

The sixth notion you must disabuse yourself of is that mainframe development cannot be agile.  It _can_, it just usually _isn't._  Most mainframe shops are not optimized for speed of application delivery, they are optimized for staff, i.e. the smallest number of staff possible.  So you end up with a tragedy of the commons where the commons is staff who perform tasks on the critical path.  Fixing this is more of a management problem than a technology problem.

There exist technologies to assist in performing some administrative tasks that often bottleneck mainframe development; the CICS Explorer is one that would allow developers to create their own CICS transaction, program, et. al. definitions.  But it's a management decision to train the developers and to allow the use of such a tool, perhaps in non-Production environments and with a workflow involving CICS Systems Programmers having veto power over particular configurations.

The seventh notion you must disabuse yourself of is that batch is not modern.  To perform some long-running task off-hours without user interaction ("in batch") is simply a design decision.  It's common for mainframe applications to be designed to do things in batch that _could_ be done interactively but... why bother anyone with it?  People are busy, and automation is a good thing.

So what is left to modernize?

 + Update your development processes and incorporate tools to empower development staff and remove some of the burden from your Sysprogs.
 + Train your development staff.
 + Get your security staff looking into securing your applications that must be accessed from (e.g.) mobile applications.  RACF does digital certificates which can be mapped to user IDs for the purposes of CICS transaction execution.
 + Refactor your existing applications into loosely coupled tiers for UI, business rules, and data access.
 + Expose your business rules as web services.

You've already done those things?

__Then you're done.__

____________________________
<a name="f01">1</a> COBOL has had object oriented (OO) extensions for, I don't remember, maybe 20 years now?  Almost no one uses them.

<a name="f02">2</a> I suspect Functional Programming (FP) was invented by some CompSci grad students as a joke.  Like many ivory tower notions, it invents a problem and then solves it.

<a name="f03">3</a> Any more than mammals were "better" than dinosaurs.  Dinosaurs ruled the earth until they were wiped out by an extinction event.  Mammals didn't out-compete dinosaurs, they snuck into the ecosystem void left by the vanished dinosaurs.

<a name="f04">4</a> Or raw sockets, if that floats your boat.

<a name="f05">5</a> Segal's law is an adage that states: "A man with a watch knows what time it is. A man with two watches is never sure."  I'm pretty sure the Wikipedia entry for Segal's law is wrong, it's not meant to be ironic, and I _certainly_ don't mean it to be in this case.

