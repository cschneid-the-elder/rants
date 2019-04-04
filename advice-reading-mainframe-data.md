Some generic advice for non-mainframe people desirous of transferring data from a mainframe in order to process it on their preferred platform.

Please understand there is a big difference between...

 + what is technically possible
 + what is allowed in your shop
 + what is likely to provide a robust and maintainable solution given your requirements

These are three very different things.  Some of us have life experiences that make us reticent about answering questions regarding what is technically possible absent any mention of what is allowed in your shop or what the actual business requirement is that is being solved.

Mainframes have been around for over half a century, and many shops have standard solutions to technical problems.  Sometimes the solution is "don't do that, and here's what *we* do instead."  Working against the recommendations of your technical staff, or your shop standards, is career limiting.

Considerations and questions you must be able to answer in order to accomplish your goal or have a mainframe person assist you (e.g. on [Stack Overflow](https://stackoverflow.com)).

####What operating system?  

**z/OS** is in common use on mainframes, but there do exist shops that still run one of its ancestors like MVS/XA.  The mainframe operating system traces its roots back to OS/360 first available in 1965.  

**z/VSE**

**z/TPF**  

**z/Linux** usually runs on top of the **z/VM** hypervisor.  

####In what sort of file does the data reside?  

**QSAM** or Queued Sequential Access Method, also commonly called flat files.  

**VSAM** or Virtual Sequential Access Method.  There are several different kinds of VSAM files including *KSDS* (Keyed Sequential Data Set) *ESDS* (Entry Sequenced Data Set), *RRDS* (Relative Record Data Set), and *Linear* (conceptually similar to a memory mapped file).  

**a DBMS** like *DB2* or *IMS*.  A DBMS typically has extract facilities to allow writing a flat file from its own internal format.  DB2, for example, stores data in Linear VSAM datasets.  

**Unix System Services** files reside in a different file system than QSAM or VSAM.  This will be more familiar to Unix, Linux, and Windows people as it has a directory structure where the classic z/OS file system has none.  

####What does the data look like?  

You must know the record layout of the data you wish to retrieve.

Text fields _must_ be converted from EBCDIC to ASCII. Binary and packed decimal (sometimes known as Binary Coded Decimal or BCD) fields _must not_ be converted. If you convert binary fields then you will alter their values, it's possible (likely? certain?) you will destroy their values.

Binary fields coming from a mainframe will be big-endian, you may need to convert these to little endian. +10 in a halfword on a mainframe is x'000A' while on a little endian machine it is x'0A00'.

Packed decimal fields may have implied decimal positions. If your file contains x'12345C' that may represent +123.45 or +12,345. The format of the field tells you how to interpret the data.

You cannot do the conversion without knowing the record layout including field formats.

In my experience, the best way to avoid these difficulties is to preprocess the file on the mainframe, converting all binary and packed decimal fields to text with embedded explicit signs and decimal points. Then the file can safely go through code page (EBCDIC to ASCII in this case) conversion.

Such preprocessing can easily be done with the mainframe SORT utility, which typically excels at data transformations.

It is common for mainframe data to include both text and binary data in a single record, for example a name, a currency amount, and a quantity:  

`Hopper    Grace     ar% .`  

...which would be...  

`x'C8969797859940404040C799818385404040404081996C004B'`  

...in hex.  This is code page 37, commonly referred to as EBCDIC.  

Without knowing that the family name is confined to the first 10 bytes, the given name confined the the subsequent 10 bytes, the currency amount is in packed decimal (also known as binary coded decimal) in the next 3 bytes, and the quantity in the next two bytes, you cannot accurately transfer the data because code page conversion will destroy the currency amount.  Converting to code page 1250, commonly in use on Microsoft Windows, you would end up with...  

`x'486F707065722020202047726163652020202020617225002E'`  

...where the text data is translated but the packed data is destroyed.  The packed data no longer has a valid sign in the last nibble (the lower half of the last byte), the currency amount itself has been changed as has the quantity (from decimal 75 to decimal 11,776 due to both code page conversion and mangling of a big endian number as a little endian number).  

Keep in mind that data in DB2 will likely be normalized and thus you must join the contents of related tables in order to make sense of the data.

####Security  

Is the data you wish to access covered by privacy legislation?  You may have to provide some evidence that whatever protections are in place to guarantee that only authorized personnel have access to this data on the mainframe are also in place once you have transferred it off of the mainframe.  Such guarantees may have to satisfy an auditor.   

####What you need  

You need to know what operating system holds your data, you need to know what type of file holds your data (a DBMS isn't a type of file but let's let that go for now), and you need to know your record layout(s).  

Typically, the easy way to retrieve data is to extract it from its existing data store (QSAM, VSAM, DBMS) into a flat file where all the data is in a text format.  *There are mainframe utilities to accomplish this.*  In extreme cases, a program can be written to accomplish this goal.  Once it has been accomplished, you can transfer your data without fear of destroying packed or binary data.  

You may be able to read data directly from a DBMS if that's where your data resides, but this may depend on shop standards, including security.  

Transferring the data can be done via a number of methods, depending on your shop's standards.  Mainframes can use FTP, FTPS, or SFTP.  NFS and SMB are also supported.  All of these must be set up by your shop's technical staff.  One or more may already be in place.

Once you have the data transferred you may be able to use [JRecord](https://stackoverflow.com/questions/46313332/how-do-you-generate-javajrecord-code-for-a-cobol-copybook) (if you're using Java) or [cb2xml](https://stackoverflow.com/questions/48519682/cobol-copybook-parser) if you want to generate XML.  I'm sure there are other tools.