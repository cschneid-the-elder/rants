"Modernization," or digital transformation by some definitions, as an exercise in decoupling your applications from your infrastructure, or indeed any specific infrastructure, is a good idea.

Not that you'll do that, but it is a _really_ good idea.

C is a portable language.  Moving an application from one OS and hardware platform to another can be a matter of of recompiling and relinking the code.  Just don't do anything platform-specific in your code.  Like define a variable as a DWORD which is what those wizards in your Windows IDE will do for you.

COBOL is a portable language.  Moving an application from one OS and hardware platform to another can be a matter of recompiling and relinking the code.  Just don't do anything platform-specific in your code.  Like access a database, in which case you'll have to re-precompile your code and re-evaluate your performance profile.  You can mitigate this by designing your application in layers, but you've [read all about that](https://github.com/cschneid-the-elder/rants/blob/master/modernization-and-its-discontents-002.md).

SQL was designed to be RDBMS-agnostic.  The SQL in your applications is likely using features specific to your RDBMS for performance or convenience reasons.  You're not alone, this is common, and intentional on the part of the RDBMS vendor.  Vendor lock-in is a feature from their point of view.

Java, and languages based on the Java VM specification, are portable at a byte-code (.class file) level.  Just don't do anything platform-specific in your code.  Like refer to a drive letter.  Or create a window -- not all OSs support a GUI, e.g. z/OS.  Also, not all OSs are equally tolerant of a Java VM -- e.g. macOS.  Also, Java isn't completely free of charge any more, depending on your definition of free and what sort of support you want and what version you're using and probably various other caveats; it's become complicated.

[OpenStack](https://en.wikipedia.org/wiki/OpenStack) is... oh, you know where this is going.

Cloud vendors have learned from history, and will require, or at least seek to entice you to use, their own version of containers and orchestration and database software.  Vendor lock-in is still a feature from their point of view.  If you're hosting your data on their cloud, and _of course you are_ because otherwise you're still doing your own hosting and the point of cloudification is to _not_ do your own hosting, are you using a vendor-specific database?  Whether you are or not, how much data are we talking about?  How would you go about moving that data to another vendor's cloud?  It's easy to get in, but getting out is another story.  And at what cost?

You _can_ be portable, you _can_ be OS-agnostic and DBMS-agnostic, and cloud vendor-agnostic.  But that's _hard_ and requires _thought_, and _planning_, and it _costs money_, which cuts into the savings from doing it, or the profits of the company you hire to do it for you.  So you'll probably find yourself locked into some vendor's product(s) because this is all about short term savings in order to make the quarterly numbers of someone above you in the food chain look good instead of long term direction for the organization in order to insulate you from technological change.

I mean really, you're going to go with Amazon, right?  That's the safe bet, and [nobody ever got fired](http://wiki.c2.com/?NobodyEverGotFiredForBuyingMicrosoft) for recommending AWS and EC2.  And Amazon DynamoDB.  And Amazon EKS.

Getting out of the future vendor lock-in is someone else's problem.  It always is; getting _into_ the cloud is just _you_ getting out of the _last person's_ vendor lock-in.
