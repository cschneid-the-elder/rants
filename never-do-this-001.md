Twenty years ago [I was one of the winners](https://www.ioccc.org/years.html#2000_schneiderwent) of the [International Obfuscated C Code Contest](https://www.ioccc.org/index.html) (IOCCC), whose purpose (quoting from their site) is...

 + To write the most Obscure/Obfuscated C program within the rules.
 + To show the importance of programming style, in an ironic way.
 + To stress C compilers with unusual code.
 + To illustrate some of the subtleties of the C language.
 + To provide a safe forum for poor C code. :-)

With that as preamble, I present __things you should never do with JCL__.

_Abuse of JCL symbols._  JCL symbols are _very_ useful, but as we see here, they hold the potential for abuse.

	//HERC03E JOB CSCHNEID,                                                 00000100
	//            NOTIFY=HERC03,                                            00000200
	//            MSGCLASS=1,                                               00000300
	//            TYPRUN=SCAN,                                              00000400
	//            MSGLEVEL=(1,1)                                            00000500
	//*                                                                     00000600
	//PROC01  PROC                                                          00000700
	//*                                                                     00000800
	//PS01    EXEC PGM=IEFBR14                                              00000900
	//DD01    DD  &D&I&S&P=(&N&E&W,&C&A&T&L&G,&D&E&L&E&T&E),                00001000
	//            &D&S&N=&H&E&R&C.03.&T&E&S&T.0005.&D&D.01,                 00001100
	//            &D&C&B=(&R&E&C&F&M=&F&B,&L&R&E&C&L=80,                    00001200
	//            &B&L&K&S&I&Z&E=27840),                                    00001300
	//            &S&P&A&C&E=(80,(100,100),&R&L&S&E)                        00001400
	//*                                                                     00001500
	//        PEND                                                          00001600
	//*                                                                     00001700
	//JS01    EXEC PROC01,A=A,B=B,C=C,D=D,E=E,F=F,G=G,H=H,I=I,              00001800
	//            K=K,L=L,M=M,N=N,P=P,R=R,S=S,T=T,W=W,Z=Z                   00001900
	//*                                                                     00002000

It turns out that you cannot use a symbol for the leading //, you cannot use a symbol for the JCL statement name, you cannot use a symbol for the JCL operation, but for most JCL statements you can use a symbol anywhere you like after that.  This gives you immense flexibility.  Think _really_ hard about how you want to exercise that power.

_Abuse of the internal reader._  The requirement to serialize jobs is common, and usually solved with a job scheduling package.  Some shops restrict the use of such packages to production jobs only, and/or to select staff trained in their use.  So we see job serialization accomplished via writing a serialized job to the internal reader.  But this is just _awful_.

	//HERC03G JOB CSCHNEID,                                                 00000100
	//            NOTIFY=HERC03,                                            00000200
	//            MSGCLASS=1,                                               00000300
	//            MSGLEVEL=(1,1)                                            00000500
	//*                                                                     00000600
	//JS01     EXEC PGM=IEBGENER                                            00000700
	//SYSUT2   DD  SYSOUT=(A,INTRDR)                                        00000800
	//SYSIN    DD  DUMMY                                                    00000900
	//SYSPRINT DD  SYSOUT=*                                                 00001000
	//SYSUT1   DD  DATA,DLM=##                                              00001100
	//HERC03Y JOB CSCHNEID,                                                 00001200
	//            NOTIFY=HERC03,                                            00001300
	//            MSGCLASS=1,                                               00001400
	//            MSGLEVEL=(1,1)                                            00001600
	//*                                                                     00001700
	//JS01     EXEC PGM=IEBGENER                                            00001800
	//SYSUT2   DD  SYSOUT=(A,INTRDR)                                        00001900
	//SYSIN    DD  DUMMY                                                    00002000
	//SYSPRINT DD  SYSOUT=*                                                 00002100
	//SYSUT1   DD  DATA,DLM=$$                                              00002200
	//HERC03Z JOB CSCHNEID,                                                 00002300
	//            NOTIFY=HERC03,                                            00002400
	//            MSGCLASS=1,                                               00002500
	//            MSGLEVEL=(1,1)                                            00002700
	//*                                                                     00002800
	//JS01     EXEC PGM=IEFBR14                                             00002900
	//*                                                                     00003000
	$$                                                                      00003100
	//*                                                                     00003200
	##                                                                      00003300
	//*                                                                     00003400

I didn't try nesting these any deeper, and maybe there's a limit, but as far as I'm concerned the limit I'm willing to tolerate is _one_.

Abominations like the above may be useful as arguments in favor of access to the shop's job scheduling package and training in how to use it.

I'm sure there are terrible abuses of the INCLUDE statement out there, with parameterized MEMBER= values containing SET statements that redefine those same parameters.  I'm limited to what the Hercules emulator can legally run, but you do your best with what you've got available.
