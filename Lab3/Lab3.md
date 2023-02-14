# Lab Report 3
Welcome to CSE 15L Lab Report 3. This week we're studying bash commands. Or should I say, the many commands of the one command I've picked: `grep`

## Definition
In our previous labs, we used `grep ".txt"` to find all the files in a directory that ended with the `.txt` extension. However, here's how `grep` defines itself and all its options, unapologetically copied and pasted from the command `grep --help`:
 ```
Usage: grep [OPTION]... PATTERN [FILE]...
Search for PATTERN in each FILE or standard input.
PATTERN is, by default, a basic regular expression (BRE).
Example: grep -i 'hello world' menu.h main.c

Regexp selection and interpretation:
  -E, --extended-regexp     PATTERN is an extended regular expression (ERE)
  -F, --fixed-strings       PATTERN is a set of newline-separated strings
  -G, --basic-regexp        PATTERN is a basic regular expression (BRE)
  -P, --perl-regexp         PATTERN is a Perl regular expression
  -e, --regexp=PATTERN      use PATTERN for matching
  -f, --file=FILE           obtain PATTERN from FILE
  -i, --ignore-case         ignore case distinctions
  -w, --word-regexp         force PATTERN to match only whole words
  -x, --line-regexp         force PATTERN to match only whole lines
  -z, --null-data           a data line ends in 0 byte, not newline

Miscellaneous:
  -s, --no-messages         suppress error messages
  -v, --invert-match        select non-matching lines
  -V, --version             display version information and exit
      --help                display this help text and exit

Output control:
  -m, --max-count=NUM       stop after NUM matches
  -b, --byte-offset         print the byte offset with output lines
  -n, --line-number         print line number with output lines
      --line-buffered       flush output on every line
  -H, --with-filename       print the file name for each match
  -h, --no-filename         suppress the file name prefix on output
      --label=LABEL         use LABEL as the standard input file name prefix
  -o, --only-matching       show only the part of a line matching PATTERN
  -q, --quiet, --silent     suppress all normal output
      --binary-files=TYPE   assume that binary files are TYPE;
                            TYPE is 'binary', 'text', or 'without-match'
  -a, --text                equivalent to --binary-files=text
  -I                        equivalent to --binary-files=without-match
  -d, --directories=ACTION  how to handle directories;
                            ACTION is 'read', 'recurse', or 'skip'
  -D, --devices=ACTION      how to handle devices, FIFOs and sockets;
                            ACTION is 'read' or 'skip'
  -r, --recursive           like --directories=recurse
  -R, --dereference-recursive  likewise, but follow all symlinks
      --include=FILE_PATTERN  search only files that match FILE_PATTERN
      --exclude=FILE_PATTERN  skip files and directories matching FILE_PATTERN
      --exclude-from=FILE   skip files matching any file pattern from FILE
      --exclude-dir=PATTERN  directories that match PATTERN will be skipped.
  -L, --files-without-match  print only names of FILEs containing no match
  -l, --files-with-matches  print only names of FILEs containing matches
  -c, --count               print only a count of matching lines per FILE
  -T, --initial-tab         make tabs line up (if needed)
  -Z, --null                print 0 byte after FILE name

Context control:
  -B, --before-context=NUM  print NUM lines of leading context
  -A, --after-context=NUM   print NUM lines of trailing context
  -C, --context=NUM         print NUM lines of output context
  -NUM                      same as --context=NUM
      --color[=WHEN],
      --colour[=WHEN]       use markers to highlight the matching strings;
                            WHEN is 'always', 'never', or 'auto'
  -U, --binary              do not strip CR characters at EOL (MSDOS/Windows)
  -u, --unix-byte-offsets   report offsets as if CRs were not there
                            (MSDOS/Windows)

'egrep' means 'grep -E'.  'fgrep' means 'grep -F'.
Direct invocation as either 'egrep' or 'fgrep' is deprecated.
When FILE is -, read standard input.  With no FILE, read . if a command-line
-r is given, - otherwise.  If fewer than two FILEs are given, assume -h.
Exit status is 0 if any line is selected, 1 otherwise;
if any error occurs and -q is not given, the exit status is 2.

Report bugs to: bug-grep@gnu.org
GNU grep home page: <https://www.gnu.org/software/grep/>
General help using GNU software: <http://www.gnu.org/gethelp/>
 ```
There are a lot of command options here, but I'd like to hone in on a just few of them. 

## `-r` command option
I first learned about the `-r` option when preparing for the skill demonstration and very quickly learned about how useful it could be. I was initially struggling to find out how to use `grep` to search all the directories within a directory, but it would only search the non-directory files within the directory, echoing out `[DIRECTORY NAME]: Is a directory` without actually searching them. `-r` (standing for `--recursive`) solved this by recursively traversing all directories and searching inside each of them as well. 

Source: [LinuxHint](https://linuxhint.com/use-grep-recursively/)

### Example 1
```
$ grep -r "Forte da Ponte da Bandeira" written_2
written_2/travel_guides/berlitz2/Algarve-WhereToGo.txt:Your first view of Lagos will probably be from the long, riverside Avenida dos Descobrimentos, which divides the old walled city from the port. At the other end of the avenue, the well-restored fortress, Forte da Ponte da Bandeira, once guarded the entrance to the harbor in the 17th century. Cross the river to see busy fishermen, handsome boats anchored in the marina, and the fine view of the city above the walls. Many of the streets rising towards the top of town are narrow, cobbled, and more accustomed to donkeys than rental cars. Though Lagos town still retains a good part of its original walls — most of them from the 16th century, but part-Roman in places — they have been rebuilt and expanded over the centuries. Climb the ramparts for fine views over the port and out to sea.
written_2/travel_guides/berlitz2/Portugal-WhereToGo.txt:The well-restored fortress, Forte da Ponte da Bandeira, once guarded the entrance to the harbor in the 17th century. Many of the streets rising towards the top of town are narrow, cobbled, and more accustomed to donkeys than rental cars. Though Lagos town still retains a good part of its original walls — most of them from the 16th century, but part-Roman in places — they have been rebuilt and expanded over the centuries.
```
### Example 2
```
$ grep -r "if ("
.git/hooks/fsmonitor-watchman.sample:if ($version ne 2) {
.git/hooks/fsmonitor-watchman.sample:   if (is_work_tree_watched($o)) {
.git/hooks/fsmonitor-watchman.sample:   if (substr($last_update_token, 0, 1) eq "c") {
.git/hooks/fsmonitor-watchman.sample:   if ($retry > 0 and $error and $error =~ m/unable to resolve root .* directory (.*) is not watched/) {
.git/hooks/fsmonitor-watchman.sample:   if ($^O =~ 'msys' || $^O =~ 'cygwin') {
.git/hooks/pre-rebase.sample:                   if (!exists $not_in_next{$elem->[0]}) {
.git/hooks/pre-rebase.sample:                           if ($msg) {
DocSearchServer.java:       if (url.getPath().equals("/")) {
DocSearchServer.java:       } else if (url.getPath().equals("/search")) {
DocSearchServer.java:           if (parameters[0].equals("q")) {
```
## `-l` command option
This is another option I used during the skill demonstration, as I noticed that even after finding the file in a directory it would print the the line that the pattern (string) was on along with the file name, resulting in an extremely long and cluttered output result. It would also print a file more than once if the pattern appears more than once, which would be redundant when used for file searching. The `-l` (standing for `--files-with-matches`) option solved this by printing only the file with the matching pattern, once. 

### Example 3
```
$ grep -r -l "Forte da Ponte da Bandeira" written_2
written_2/travel_guides/berlitz2/Algarve-WhereToGo.txt
written_2/travel_guides/berlitz2/Portugal-WhereToGo.txt
```
### Example 4
```
$ grep -r -l "if ("
.git/hooks/fsmonitor-watchman.sample
.git/hooks/pre-rebase.sample
DocSearchServer.java
```
## `-n` command option
The `-n` option (standing for `line-number`) is one I didn't use during the skill demonstration, but after researching it I was able to think of a couple of ways it could be useful. Simply put, it prints out the line number of the matching patterns along with the line itself. This can be useful, especially in debugging, if you were to look for all instances of a certain command in a file (if statements, for/while loops, conditions) or perhaps to search for all instances of a variable (in order to replace it). By knowing the line number, it is easier to go into the file to search and edit it yourself.  

Source: [SoftwareTestingHelp](https://www.softwaretestinghelp.com/grep-command-in-unix/)

### Example 5
```
$ grep -r -n "if ("
.git/hooks/fsmonitor-watchman.sample:25:if ($version ne 2) {
.git/hooks/fsmonitor-watchman.sample:48:        if (is_work_tree_watched($o)) {
.git/hooks/fsmonitor-watchman.sample:90:        if (substr($last_update_token, 0, 1) eq "c") {
.git/hooks/fsmonitor-watchman.sample:126:       if ($retry > 0 and $error and $error =~ m/unable to resolve root .* directory (.*) is not watched/) {
.git/hooks/fsmonitor-watchman.sample:165:       if ($^O =~ 'msys' || $^O =~ 'cygwin') {
.git/hooks/pre-rebase.sample:79:                        if (!exists $not_in_next{$elem->[0]}) {
.git/hooks/pre-rebase.sample:80:                                if ($msg) {
DocSearchServer.java:39:       if (url.getPath().equals("/")) {
DocSearchServer.java:41:       } else if (url.getPath().equals("/search")) {
DocSearchServer.java:43:           if (parameters[0].equals("q")) {
```
### Example 6
```
$ grep -n "return" DocSearchServer.java
25:        return result;
28:        return new String(Files.readAllBytes(f.toPath()));
40:           return String.format("There are %d total files to search.", paths.size());
53:               return String.format("Found %d paths:\n%s", foundPaths.size(), result);
56:               return "Couldn't find query parameter q";
60:           return "Don't know how to handle that path!";
69:            return;
```
## `-v` command option
The `-v` option (standing for `--invert-matches`) is another interesting command option I found while researching. It basically prints out the opposite output of what a normal `-grep` command would, meaning that instead of printing all lines or files with matches, it prints out all lines or files WITHOUT matches instead. Not only will you receive this inverted data, but you could also use it to essentially REMOVE all lines with a certain pattern. 

Source: [AskUbuntu](https://askubuntu.com/questions/1153513/what-does-grep-v-grep-mean-and-do)
### Example 7: All files with "California" that are not in `non-fiction'.
```
$ grep -r -v "non-fiction" grep-results.txt
written_2/travel_guides/berlitz1/HandRLosAngeles.txt
written_2/travel_guides/berlitz1/HistoryLasVegas.txt
written_2/travel_guides/berlitz1/WhatToLasVegas.txt
written_2/travel_guides/berlitz1/WhatToLosAngeles.txt
written_2/travel_guides/berlitz1/WhereToIndia.txt
written_2/travel_guides/berlitz1/WhereToLosAngeles.txt
written_2/travel_guides/berlitz1/WhereToMallorca.txt
written_2/travel_guides/berlitz2/California-History.txt
written_2/travel_guides/berlitz2/California-WhatToDo.txt
written_2/travel_guides/berlitz2/California-WhereToGo.txt
written_2/travel_guides/berlitz2/Canada-WhereToGo.txt
```
### Example 8: All files with "California" that arenot in `travel-guides`.
```
$ grep -r -v "travel_guides" grep-results.txt
written_2/non-fiction/OUP/Abernathy/ch15.txt
written_2/non-fiction/OUP/Abernathy/ch2.txt
written_2/non-fiction/OUP/Berk/ch1.txt
written_2/non-fiction/OUP/Castro/chA.txt
written_2/non-fiction/OUP/Castro/chB.txt
written_2/non-fiction/OUP/Castro/chC.txt
written_2/non-fiction/OUP/Castro/chL.txt
written_2/non-fiction/OUP/Castro/chM.txt
written_2/non-fiction/OUP/Castro/chP.txt
written_2/non-fiction/OUP/Castro/chQ.txt
written_2/non-fiction/OUP/Castro/chR.txt
written_2/non-fiction/OUP/Castro/chV.txt
written_2/non-fiction/OUP/Castro/chW.txt
written_2/non-fiction/OUP/Fletcher/ch9.txt
written_2/non-fiction/OUP/Kauffman/ch1.txt
written_2/non-fiction/OUP/Kauffman/ch9.txt
written_2/non-fiction/OUP/Rybczynski/ch1.txt
written_2/non-fiction/OUP/Rybczynski/ch2.txt

```
