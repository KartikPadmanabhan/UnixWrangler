# The head Command

The head command reads the first few lines of any text given to it as an input and writes them to standard output (which, by default, is the display screen).

head's basic syntax is:

```
   head [options] [file(s)]
```

The square brackets indicate that the enclosed items are optional. By default, head returns the first ten lines of each file name that is provided to it.

For example, the following will display the first ten lines of the file named aardvark in the current directory (i.e., the directory in which the user is currently working):

```
   head aardvark
```

If more than one input file is provided, head will return the first ten lines from each file, precede each set of lines by the name of the file and separate each set of lines by one vertical space. The following is an example of using head with two input files:

```
   head aardvark armadillo
```

If it is desired to obtain some number of lines other than the default ten, the -n option can be used followed by an integer indicating the number of lines desired. For example, the above example could be modified to display the first 15 lines from each file:

```
   head -n15 aardvark armadillo
```
-n is a very tolerant option. For example, it is not necessary for the integer to directly follow it without a space in between. Thus, the following command would produce the same result:

```
   head -n   15 aardvark armadillo
```

In fact, the letter n does not even need to be used at all. Just the hyphen and the integer (with no intervening space) are sufficient to tell head how many lines to return. Thus, the following would produce the same result as the above commands:

```
   head -15 aardvark armadillo
```

head can also return any desired number of bytes (i.e., a sequence of eight bits and usually long enough to represent a single character) from the start of each file rather than a desired number of lines. This is accomplished using the -c option followed by the number of bytes desired. For example, the following would display the first five bytes of each of the two files provided:

```
   head -c 5 aardvark anteater
```

When head counts by bytes, it also includes the newline character, which is a non-printing (i.e, invisible) character that is designated by a backslash and the letter n (i.e., \n). Thus, for example, if there are three new, blank lines at the start of a file, they will be counted as three characters, along with the printing characters (i.e., characters that are visible on the monitor screen or on paper).

The number of bytes or lines can be followed by a multiplier suffix. That is, adding the letter b directly after the number of bytes multiplies it by 512, k multiplies it by 1024 and m multiplies it by 1048576. Thus, the following command would display the first five kilobytes of the file aardvark:

```
  head -c5k aardvark
```
The -c option is less tolerant than the -n option. That is, there is no default number of bytes, and thus some integer must be supplied. Also, the letter c cannot be omitted as can the letter n, because in such case head would interpret the hyphen and integer combination as the -n option. Thus, for example, the following would produce an error message something like head: aardvark: invalid number of bytes:

```
   head -c aardvark
```
If head is used without any options or arguments (i.e., file names), it will await input from the keyboard and will successively repeat (i.e., each line will appear twice) on the monitor screen each of the first ten lines typed on the keyboard. If it were desired to repeat some number of lines other than the default ten, then the -n option would be used followed by the integer representing that number of lines (although, again, it is not necessary to include the letter n), e.g.,
```
   head -n3
```

As is the case with other command line (i.e., all-text mode) programs in Linux and other Unix-like operating systems, the output from head can redirected from the display monitor to a file or printer using the output redirection operator (which is represented by a rightward-pointing angular bracket). For example, the following would copy the first 12 lines of the file Yuriko to the file December:

```
   head -n 12 Yuriko > December
```

If the file named December did not yet exist, the redirection operator would create it; if it already existed, the redirection operator would overwrite it. To avoid erasing data on an existing file, the append operator (which is represented by two consecutive rightward pointing angle brackets) could be used to add the output from head to the end of a file with that name if it already existed (or otherwise create a new file with that name), i.e.,

```
   head -n 12 Yuriko >> December
```

The output from other commands can be sent via a pipe (represented by the vertical bar character) to head to use as its input. For example, the following sends the output from the ls command (which by default lists the names of the files and directories in the current directory) to head, which, in turn, displays the first ten lines of the output that it receives from ls:

```
   ls | head
```

This output could easily be redirected, for example to the end of a file named file1 as follows:
```
   ls | head >> file1
```

It could also be piped to one or more filters for additional processing. For example, the sort filter could be used with its -r option to sort the output in reverse alphabetic order prior to appending file1:

```
   ls | head | sort -r >> file1
```

The -q (i.e., quiet) option causes head to not show the file name before each set of lines in its output and to eliminate the vertical space between each set of lines when there are multiple input sources. Its opposite, the -v (i.e., verbose) option, causes head to provide the file name even if there is just a single input file.

The tail command is similar to the head command except that it reads the final lines in files rather than the first lines.

As is the case with other commands on Unix-like operating systems, additional information can be obtained about head and tail by using the man and info commands to reference the built-in documentation, for example

```
   man head
```

or

```
info tail
```

Reference:
----------
http://www.linfo.org/head.html
