Do you have batch jobs running in place?

Sometime in the early noughties, a coworker was researching what used particular flags in one of our databases.  What she uncovered became the stuff of stories told 'round the light of a monitor well into the evening.

There was a batch job that scanned the database for records with a particular flag turned on.  It stored the keys to such records in a flat file, which was passed to a series of subsequent steps which performed various business processes, and ultimately turned off the flag on the records in the database.

The production support staff kept the spool output from the last _n_ of our batch job runs in GDGs (this was a function of our job scheduler, and it was handy in a number of instances, you could probably roll your own with Rexx and the SDSF API).  This made it easy to review control totals.  Which were zero.  In the last _n_ runs, this batch job had selected zero records for processing.

Which seemed odd.  Maybe it was normal, but no one seemed to know.

Further investigation led to the discovery that there was no extant program that turned that particular flag on.  Even further investigation turned up the fact that the last program that turned that particular flag on had been retired more than a decade prior.

Prior to Y2K.

For whatever reason, this particular batch stream had not been identified as part of the retirement effort and was left running.  Because it was selecting zero records, it was using negligible CPU, and no one complained.  No complaint, no problem, nothing to see here, let's move on.

Yes, the programs in the batch stream in question had been remediated for Y2K.  There were utilities for turning flags on and off in the database, and no doubt that was how the stream was tested without uncovering the fact that there was no application to turn on that particular flag.  Which is to say no one held the Y2K remediation staff to blame, nor should they have, this was beyond their project scope. 

 > Do you have a mechanism in place for retiring applications?  For determining if a particular piece of data in your database is obsolete?  How comprehensive is this mechanism?

We went on a mission at this point, looking for anything else that might have been running in place (as we termed it).  Most of what we found were batch programs for which there was no execution JCL, and subroutines called from nowhere.

I spent spare time locating clists that used file tailoring to construct JCL that executed vendor products we no longer licensed, or wrote to ISPF tables in datasets no longer extant.  Code written in the 1980s and left to gather dust as the world moved on.

We made use of SMF data, CICS shutdown statistics, and a vendor product that logged which modules were loaded into memory (eventAction, I have no affiliation with the vendor).

None of this was automated, the fact that something isn't executed in `${LIMIT}` years doesn't mean it's obsolete.  Maybe it's an exception routine, the sort of thing you _hope_ never to call.  Determining obsolescence requires brainwork; tools just provide leading indicators.

Obsolete stuff costs a negligible amount in DASD, little or no CPU, so what's the problem?

The problem is impact analysis.  Obsolete stuff increases the number of things that must be evaluated when you upgrade.  

 > You do impact analysis on your application portfolio when you upgrade, don't you?  Upgrade what?  The OS, the DBMS, the OLTP environment, compilers.

The problem is maintenance.  If you've no way of determining something is obsolete, you may spend time and money remediating it.  Even if your staff "just know" it's obsolete, it's still something they bark their shins on during their analysis.  And staff turnover means eventually no one will "just know" any more.

At one point I kicked over a rock and found the last module whose source was written in FORTRAN still executing in our shop.  Eliminating it meant we could eliminate a compiler and its associated costs (it was being run by just one person who agreed a spreadsheet fit their needs better).  Sometimes you can save actual `${CURRENCY_TYPE}`.

And what did we do with obsolete code?  We copied it to shadow datasets, with one of the higher level qualifiers set to OBSOLETE.  Just in case.  But these weren't included in impact analysis or maintenance.

Someday someone should figure out whose job it is to do all this.  The Systems side of the shop typically regards applications as the responsibility of the Applications side of the shop.  The Applications side of the shop typically gets scolded if they venture beyond automating business processes.
