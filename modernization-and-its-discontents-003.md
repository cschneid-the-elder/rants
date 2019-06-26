Here's a problem with "modernizing" your IT systems: sometimes the business rules are only documented in an unambiguous fashion in the existing code, which, let's be honest, is probably COBOL.

In the early 1990s a colleague charged with reimplementing a working business system related frustration with SMEs (Subject Matter Experts) whose expertise was in how to use the existing system.  The business had been automated since before anyone currently performing those functions had been hired.  The canonical version of the business rules was whatever the code did in the existing system.

Count yourself lucky, the system my colleague was analyzing was written in 360/Assembler.

You can't ignore the existing system.  The users don't know the business rules, they only know how to use the existing system.  The business rules were codified and then forgotten, long, long ago.  

Why forgotten?  Because having the system tell the users what to do, rather than the reverse, means the users become less-skilled labor.  Less training is required.  Costs are perceived to go down.  Staff turnover becomes less of a problem.

Those staff who worked with the analysts and programmers to unambiguously specify how the business works are gone now.  The business knowledge walked out the door with them.  The analysts and programmers likely left too.

> There's a side issue here, and it's that employing organizations have spent the last several decades acting as if the staff were fungible resources.  Those particular farm fowl first returned to their domiciles to roost during the Y2K kerfuffle, when it became evident that deep knowledge of the business and the business applications was important in order to remediate said applications.  The difficulties continue, and you should thank those who still espouse that school of thought for your uncomfortable situation.

There exist companies that purport to extract business rules from your existing applications.  Never having worked with one of these, I nevertheless see a foundational flaw because I am an old man and have become familiar with the scent of snake oil over the course of my career.

Your business rules are very likely _already_ specified in an unambiguous English-like language designed expressly for business.  That's what COBOL _is_.

My point here is that to understand the business rules probably means understanding COBOL, which is what I presume you're going to these great lengths to avoid, for some reason that escapes me.  It's actually kind of funny; programmers, good ones anyway, pick up new programming languages all the time.  In a 30 year career I wrote code in 17 languages, not including multiple dialects.  It's not hard, you just need to find the right people, the ones who actually _like_ coding.

Oh, you'll also need to pay them market rates.  People are funny about that.

All of this presumes that you actually need to rewrite and/or replatform, but [I covered that earlier](https://github.com/cschneid-the-elder/rants/blob/master/modernization-and-its-discontents-002.md).