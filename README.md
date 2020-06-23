# kit-045
*Revised 2019-09-11 by docsalvager*

(EXPERIMENTAL)

A "self-documenting" bash (not POSIX) "framework" of functions that encapsulate a few best practices as well as experimental techniques. The priorities have been ...
  - to maximize functionality
  - to maximize performance
  - to maximize readability and thus...
  - to minimize develpment (and thus debugging) time for enhancements and bug-fixes

Kit uses every "bashism" I can find since anything done in compiled code is many times faster than anything done in script. It would be impractical to try to make kit POSIX-compliant as it depends heavily upon bash introspection facilities like the FUNCNAME\[\] array that do not exist in POSIX shells.

## File Locations
  - Place kit, kit-045 and kit-045.meta (or symlinks to them) in one of the directories in $PATH.
  - Place kit-045.conf in a /home/<user>/.config/kit directory.

## Files
  kit is just a symlink to kit-045.
  
  kit-045 is the executable script.
  
  kit-045.meta is the full, detailed documentation for each function in a format much like manpages and is also executable but doesn't do much. It is made executable because it contains executable code in the form of Command Substitution `$( ... )` within the help text. kit-045 searches kit-045.meta for the function variable and returns the text value. Sometimes this may include text inserted via Command Substitution.
  
## Getting Started
Once the 3 files are in place, kit can be used in a variety of ways such as ...
  - `kit`
  - `kit --help`
    - Displays help in a scrollable window (assuming YAD or dialog are available) for the kit() function which starts off everything.
  - `kit meta fnInit`
    - Displays help in a scrollable window for the fnInit() function which is called at the beginning of every other function to handle --help, --version and a number of other common options.
  - `kit meta fnInit --inspect`
    - Displays help in a scrollable window for the fnInit() function as well as a diagnostic window showing the function stack and other debugging information. This will noticeably slow down execution as all debuggers do so the timings should be considered relative to each other rather than absolute.
  - In the directory with kit-045, create a symlink that runs the meta() function.
    - The name must _*exactly*_ match the function name.
      - `ln -s kit-045 meta`
    - Then use the new command...
      - `meta fnInit`

## GUI and CLI Interface
kit-045 attempts to use the best interface available for user interaction. Currently, YAD, dialog/cdialog and plain text (CLI) are supported. Zenity support is in there but is deprecated and will be removed in future versions. There are a common set of options (--GUI, --CLI, --NODLG) to override the default behavior that can be used with any function.

## Bugs
I'm sure there are numerous bugs and ways things could be done better. Improvements and fixes are welcome and the best ones will be incorporated into future versions.

With the exception of one-time initialization code at the beginning of the script, ***everything*** is done in defined functions with a call at the end to get things started.

## Submitted Changes
Please make a copy of the function to be changed and append '\_1' (without quotes) or similar. Only underscores (\_) are used since there are many variables derived from function names. This suffix will require each other function that calls this function to be likewise changed to use the new name. This will alert us to the other functions that need to be tested against the change. If there are many functions affected, please list the main ones and note that there are others. Please document extensively as to **why** the change is necessary or better and what is being accomplished. Restating in prose what the code clearly shows does not add anything useful.

## Code Styling For Easier Debugging
"Over 90% of development time is (or should be) spent in debugging."

Every programmer settles on the coding style that works for them. Mine is intended to ease debugging. While always willing to listen to new ideas, having done this since 1981, this is the style that works for me. I ask that you try to conform to it as best you can and tell me why your way is better when you can't. You might be right.

That said, the first thing you'll notice is that I put most comments _after_ the code line and indented with 3 hashes and a space. Please never forget the space. The style of comments without a space are very hard to read and adds no measurable speed to code execution.

Comments are _after_ the code because it is the code that is being executed and thus what is important in debugging. Comments can often be misleading until they are changed to reflect the final version of the code line.

In fact you'll find a lot of techniques in kit that violate common practice. Be assured that I have spent days experimenting with different techniques and found that a great many of the "best practices" in common use do not speed up execution appreciably, often slow it down, and very often make debugging harder.

## Future Versions
Currently working on kit-047 which has a number of core changes and so is incompatible with kit-045. For the curious, kit-046 was a rabbithole I went down and abandoned.
