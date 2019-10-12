Something positive for a change.  If you've been [following along](https://github.com/cschneid-the-elder/rants), you've been wading through quite a bit of negative space -- me ranting about what _not_ to do.

Well, here's a bit of what _to_ do.

__Read__

Read the IBM documentation for products you use.  The Knowledge Centers are right there, waiting for you, veritably stuffed with information.  I don't mean to start at the beginning and just read straight through, I mean look at the table of contents and see what you didn't know was there.  Language Environment or JCL references are good places to start.

Read [SHARE presentations](https://www.share.org/p/cm/ld/fid=59) (sometimes called proceedings).  Lots of good stuff there, several orders of magnitude better if you can attend, but if you can't you can still learn from the PDFs available on the web.

Read the documentation for ISV products you use.  There's some danger in tying your processes to products that your IT shop may decide to replace, so ask the Sysprogs about the viability of using obscure features.

There are other sources of mainframe information.  Before I left the codeface for a seat by the fire I spent my lunch reading mainframe RSS feeds and the ibm-main, cics, and mq listservs.  There are also many informative YouTube videos, if you're into that sort of thing.

__Experiment__

_Try_ things.

Years ago, presented with an argument regarding which of various ways to copy a file was "best," I used IEBDG to generate test data files in varying sizes and demonstrated that, for files greater than a particular size, our SORT utility was an order of magnitude faster than its nearest competitor in the shop.  Which led to CPU savings.

So, e.g., see what effect adding BUFNO= various values has on CPU time.  It may not have any effect at all for a SORT, but could help for your COBOL programs.

Does it matter if you add AMP='RMODE31=ALL' to the DD for a VSAM file?  How about MSG=SMBBIAS?  Do you learn anything about whether you should maybe code ACCBIAS?

What are your default LE options?  Would something you're working on benefit from a specific change?  Use CEEOPTS to determine what, if any, changes would be a good idea.

What kind of a mainframe are you running on?  What kind of a mainframe is at your DR site?  How do these compare with the default ARCH level specified in your compile options?

Be certain to capture your results.  Record dates, times, job numbers, job names, CPU usage, and so forth in order to back up your recommendations.

__Talk__

Sysprogs tend to be busy, and to not suffer fools gladly, but in my experience they welcome intelligent questions.  If approached with, "I made these JCL changes and tested them, nothing bad seems to have happened and the CPU time went down by 10% - am I missing something or should I propose the JCL changes come along with what I was actually supposed to be doing?" you may very well get a positive reaction.

Now, your production support staff who are responsible for the care and feeding of production batch jobstreams may justifiably be reticent about making changes to what is known to work well.  But if you can demonstrate CPU savings (thus having a positive impact on the 4HRA) they too may have a positive reaction.

By all means, _talk_ to people.  _Listen_ to their concerns and _understand_ why those concerns are important to them.  

__Write__

Once you've read up on what can be done, tried it out in an experimental mode, talked to the appropriate staff in your organization and received approval to implement your changes, _write_ about the experience.  What did you learn from your reading, how did you put it to use, who did you talk to about the observed benefits, and what were the actual benefits once implemented.

Make sure management knows what you did, and the good things that resulted.  My management was always delighted by cost savings, and also by discovering someone who could write coherent prose.

An understanding of _how it works_ is much more valuable than the knowledge of how to fix a subset of the infinite number of specific issues.

Of such things are technical advancement made.
