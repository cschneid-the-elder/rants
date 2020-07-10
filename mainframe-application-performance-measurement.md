In 2012, after a particularly unpleasant CPU capacity shortfall, I was tasked with putting together statistics to help prevent/predict/notice the graph of our application CPU experiencing a sudden upward inflection. This would be indicative of a nasty surprise come the end of month billing cycle.

SMF and MXG and SAS to the rescue. Amongst other things, I put in place an alert for applications experiencing atypical behavior. The alert was an email to me and the other two members of our team, our response was to begin digging through the change management system to see if maintenance had been applied to the application recently.

On more than one occasion we discovered maintenance had resulted in performance degradation. As the shop implemented CPU chargeback, it was appreciated that we brought the behavioral changes to the notice of the application staff.

In at least one instance we discovered that it was not maintenance to the application, but very specific data fed into it that caused more than usual CPU usage. This was part of a business cycle - every 3 months a particular CICS transaction's CPU usage would spike for a day or two.

The alert was made possible by keeping a profile of applications, implemented as a flat file with fields for CICS CPU, CICS storage high water mark, DB2 CPU, number of DB2 requests, elapsed time, TCB switches, etc. From this, one can compute historical rolling measures of central tendency and then determine if current measurements are far enough away from historical measurements to warrant investigation.

I went so far as to route reports (top 10 CPU users, top 10 TCB switchers, et. al.) to GDGs and to write ISPF dialogs to view them. Publishing to an internal web page or dashboard would have been a good idea.

And no, I don't have the code, it belongs to a previous employer. If you're a SAS person, this isn't that hard to do, most of the heavy lifting has been done for you by Barry Merrill's [MXG package](https://www.mxg.com/product_info/) which is common on IBM Z. Talk to your Capacity and Performance people about what's available in your shop for processing SMF data.

There's a tendency now to buy instead of building your own. That's not always the best solution.