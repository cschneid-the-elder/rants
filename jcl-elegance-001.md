# The Elegant Simplicity of JCL

Despite the estimable [Fred Brooks' comments](https://www.computerhistory.org/revolution/mainframe-computers/7/162/2270), I would like to praise the elegant simplicity of JCL.

JCL is ridiculously simple.  The syntax is each line begins with an identifier field consisting of two slashes, optionally followed by a one to eight character name followed optionally by a dot and another one to eight character name followed by a space followed by an operation, followed by a space, followed by a comma separated list of operation parameters or operands.

If the identifier field is two slashes followed by an asterisk, the line is considered a comment and ignored.

If the identifier field is a single slash followed by an asterisk, the statement is a JES control statement.  Such statements control the execution environment for the job.

The name field can consist of alphabetic, numeric, or national (@#$) characters, except it cannot begin with a numeric character.

Any text preceded by a space following an operation parameter or operand is considered to be a comment and is ignored.  Such comments can be continued by coding a non-blank character in column 72, in which case the next line is considered a comment.

If all the operands don't fit on a single line, you end the line with an operation parameter or operand and its comma and continue on the next line.  Which must begin with two slashes but must not have a name field but must have at least one and no more than eleven spaces before the next operand.

A line is eighty bytes long, but your JCL must not go past column 71 unless you intend to continue an operation parameter or operand which is enclosed in quotes in which case you leave column 72 non-blank and continue the operation parameter or operand on the next line after the identifier field and at least one but not more than eleven spaces.

Columns 73 - 80 are for line numbers or comments and are ignored unless the statement is a JES2 `SIGNON` control statement in which case these columns hold a password.

There are only 17 operations, some of which are trivial, though the DD (Data Definition) operation has over a hundred operands or operation parameters and subparameters, many of which are for use with hardware and media that have long since vanished from the face of the earth and so can be safely ignored.  None of those operations is a looping construct.

If the operation is DD and its first operation parameter or operand is an asterisk, then the following lines are considered to be data to be read when the program being executed indicates it wants to read data from the named file.  The end of the data is indicated by the identifier field being two slashes, a single slash followed by an asterisk, two slashes followed by an asterisk, or whatever value is coded for the `DLM` operation parameter or operand on the DD statement.

This elegance is due in no small part to the purpose of JCL, which is not to _do_ anything, but to execute programs which to the actual work.  JCL only specifies which programs are to be executed and the files on which they should operate.

[Nothing could be simpler](https://www.youtube.com/watch?v=yKg7IinlUfI).  Please note that, given a blank slate from which to begin, the Java Community Process came up with [JSL](https://javaee.github.io/tutorial/batch-processing003.html) as part of [JSR 352](https://jcp.org/aboutJava/communityprocess/mrel/jsr352/index.html).

