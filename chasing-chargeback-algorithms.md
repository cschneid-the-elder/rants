All systems are built around the current billing algorithm.  That's one of the things Tom Peltin taught me when he hired me in the late 1980s.  Thirty+ years on, I would amend that as follows...

 > Consciously or not, all applications are built around the current chargeback algorithm.  Cost optimizations look less and less clever as the algorithm changes.  A feature of the algorithm may be that you are unaware of its existence.
 
I have witnessed organizations chasing their chargeback algorithm, attempting to cut costs by dancing around the edges of the rules.  This works until those in charge of the algorithm notice your dance moves and put a stop to them.  They can do that, it's their algorithm.

Neon Enterprise Software [discovered this](https://www.theregister.com/2011/06/01/ibm_prevails_over_neon_zprime/), with their zPrime offering.

One of my employers had batch jobs that required a VSAM file.  They would run IDCAMS to define the VSAM file at the beginning of the job, REPRO the contents from tape, run the steps that used the VSAM file, REPRO the data back to tape, then delete the VSAM file.  This was data arbitrage, taking advantage of the fact that the tape mounts and REPROs cost less than leaving the VSAM file on DASD.

One of my employers had a daily batch job that created a GDG on tape.  End of month processing loaded all extant generations and concatenated them into a monthly GDG.  On tape.  Because keeping these files on DASD cost more than the tape mounts.

This was all true until, with a wave of a pen, it wasn't.  And then someone noticed their bill had gone up and people were scrambling to change `UNIT=TAPE` to `UNIT=DISK`.

One of my employers took advantage of the cost differential between unmigrated DASD datasets and HSM ML2 datasets.  Which reduced their costs right up until someone noticed how much time was being spent migrating and recalling those datasets.

You are not in control of the chargeback algorithm.  Actions you take to reduce your bill will be met with counter-actions to restore the status quo.

While I realize these are all mainframe examples, the same thing will happen to you in the cloud.  You don't think Amazon, Google, and Microsoft are in business to benefit _you_, do you?  They're in business to squeeze as much money out of you as they can, whilst keeping the cost of changing cloud providers just high enough to make it worth your while to stick with whichever you're using currently.

Those costs aren't just in ${CURRENCY_TYPE}.  Each has, or will have, proprietary features that you'll use because it's easier to do so than not.  Remember, vendor lock-in is a feature from their point of view.

My point is this: if you're going to reduce costs by chasing the chargeback algorithm, you must commit to _chasing_ the chargeback algorithm.  Whatever dance you do around the edges of the rules, you must be prepared to alter your steps as the rules are altered.  And you are in control of neither the nature nor the rate of change.

There are [other ways](https://github.com/cschneid-the-elder/rants/blob/master/apps-management-tuning.md) to save money.
