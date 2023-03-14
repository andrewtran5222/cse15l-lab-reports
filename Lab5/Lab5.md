# Lab Report 5
Welcome to CSE 15L Lab Report 5. This week we're looking more into the bash command I passed on in Lab Report 3: `less`

## Definition
In previous labs, `less <<file name>>` was a command we used to quickly explore files from the command line. That by itself is useful, but there are many options of the command that can make them even more useful. The command has a long summary of its usage when inputted with `--help`, and here is the raw description from its "OPTIONS" section. 
 ```
                          OPTIONS

        Most options may be changed either on the command line,
        or from within less by using the - or -- command.
        Options may be given in one of two forms: either a single
        character preceded by a -, or a name preceded by --.

  -?  ........  --help
                  Display help (from command line).
  -a  ........  --search-skip-screen
                  Search skips current screen.
  -A  ........  --SEARCH-SKIP-SCREEN
                  Search starts just after target line.
  -b [N]  ....  --buffers=[N]
                  Number of buffers.
  -B  ........  --auto-buffers
                  Don't automatically allocate buffers for pipes.
  -c  ........  --clear-screen
                  Repaint by clearing rather than scrolling.
  -d  ........  --dumb
                  Dumb terminal.
  -D [xn.n]  .  --color=xn.n
                  Set screen colors. (MS-DOS only)
  -e  -E  ....  --quit-at-eof  --QUIT-AT-EOF
                  Quit at end of file.
  -f  ........  --force
                  Force open non-regular files.
  -F  ........  --quit-if-one-screen
                  Quit if entire file fits on first screen.
  -g  ........  --hilite-search
                  Highlight only last match for searches.
  -G  ........  --HILITE-SEARCH
                  Don't highlight any matches for searches.
  -h [N]  ....  --max-back-scroll=[N]
                  Backward scroll limit.
  -i  ........  --ignore-case
                  Ignore case in searches that do not contain uppercase.
  -I  ........  --IGNORE-CASE
                  Ignore case in all searches.
  -j [N]  ....  --jump-target=[N]
                  Screen position of target lines.
  -J  ........  --status-column
                  Display a status column at left edge of screen.
  -k [file]  .  --lesskey-file=[file]
                  Use a lesskey file.
  -K  ........  --quit-on-intr
                  Exit less in response to ctrl-C.
  -L  ........  --no-lessopen
                  Ignore the LESSOPEN environment variable.
  -m  -M  ....  --long-prompt  --LONG-PROMPT
                  Set prompt style.
  -n  -N  ....  --line-numbers  --LINE-NUMBERS
                  Don't use line numbers.
  -o [file]  .  --log-file=[file]
                  Copy to log file (standard input only).
  -O [file]  .  --LOG-FILE=[file]
                  Copy to log file (unconditionally overwrite).
  -p [pattern]  --pattern=[pattern]
                  Start at pattern (from command line).
  -P [prompt]   --prompt=[prompt]
                  Define new prompt.
  -q  -Q  ....  --quiet  --QUIET  --silent --SILENT
                  Quiet the terminal bell.
  -r  -R  ....  --raw-control-chars  --RAW-CONTROL-CHARS
                  Output "raw" control characters.
  -s  ........  --squeeze-blank-lines
                  Squeeze multiple blank lines.
  -S  ........  --chop-long-lines
                  Chop (truncate) long lines rather than wrapping.
  -t [tag]  ..  --tag=[tag]
                  Find a tag.
  -T [tagsfile] --tag-file=[tagsfile]
                  Use an alternate tags file.
  -u  -U  ....  --underline-special  --UNDERLINE-SPECIAL
                  Change handling of backspaces.
  -V  ........  --version
                  Display the version number of "less".
  -w  ........  --hilite-unread
                  Highlight first new line after forward-screen.
  -W  ........  --HILITE-UNREAD
                  Highlight first new line after any forward movement.
  -x [N[,...]]  --tabs=[N[,...]]
                  Set tab stops.
  -X  ........  --no-init
                  Don't use termcap init/deinit strings.
  -y [N]  ....  --max-forw-scroll=[N]
                  Forward scroll limit.
  -z [N]  ....  --window=[N]
                  Set size of window.
  -" [c[c]]  .  --quotes=[c[c]]
                  Set shell quote characters.
  -~  ........  --tilde
                  Don't display tildes after end of file.
  -# [N]  ....  --shift=[N]
                  Horizontal scroll amount (0 = one half screen width)
                --follow-name
                  The F command changes files if the input file is renamed.
                --mouse
                  Enable mouse input.
                --no-keypad
                  Don't send termcap keypad init/deinit strings.
                --no-histdups
                  Remove duplicates from command history.
                --rscroll=C
                  Set the character used to mark truncated lines.
                --save-marks
                  Retain marks across invocations of less.
                --use-backslash
                  Subsequent options use backslash as escape char.
                --wheel-lines=N
                  Each click of the mouse wheel moves N lines.
 ```
There are a lot of command options here, but I'd like to go more into just a few of them. 

## `-N` command option
The `-N` option (standing for `line-numbers`) prints out the line number of the file being printed. It's interesting that the built-in summary describes it as "Don't use line numbers", when this is the command that you need to make them show. This can be useful in debugging, because you scroll through the file, when you see a line with an error or mistake in it, you have the line number to refer to when debugging or when referring it to another collaborator. 


### Example
```
$ less -N history.txt
      1
      2
      3
      4
      5 A Brief History
      6 Little is known of the earliest Stone Age inhabitants of Europe’s southwestern extremity. The ancient Greeks      6  called them the Cynetes (or Cunetes). Whatever their origins, their culture evolved under the pressure and       6 influence of foreign forces. Among the many invading armies that settled here and contributed to nascent Por      6 tuguese culture were Phoenicians, who settled in the area around 1,000 b.c., followed by the Celts, Iberians      6 , Greeks, and Carthaginians.
      7 But it was the Romans, who arrived late in the third century b.c., who most greatly influenced all of Iberia      7 . They built towns, industries, roads, and bridges, developed agriculture, and bequeathed the Latin language      7 , of which Portuguese is a direct descendant. The Romans named the southwestern province of the peninsula Lu      7 sitania, oddly enough for one of the Celtiberian tribes they defeated, and by the third century a.d. had int      7 roduced Christianity. By the beginning of the fourth century the Algarve had a bishop in place, based in Far      7 o. But Rome had already fallen into decay, and soon hordes of northern tribesmen took over the empire. The A      7 lgarve fell to the Visigoths in the mid-fifth century.

```
## `-S` command option
This `-S` command option (standing for `chop-long-lines`) is a command that truncates the end of a long line instead of wrapping the text around to a new line. If you might've noticed from the last example, the output is quite ugly when it automatically wraps the text onto the next line by default. It was hard to view the line numbers individually, as they didn't correlate visually, but with the `-S` option, `less` behaves more like a standard GUI and truncates at the edge of the terminal, but the data is still viewable by using the right arrow key or scrolling to the right. 

### Example
```
$ less -S history.txt




A Brief History
Little is known of the earliest Stone Age inhabitants of Europe’s southwestern extremity. The ancient Greeks called>
But it was the Romans, who arrived late in the third century b.c., who most greatly influenced all of Iberia. They >
Under Moorish Rule
In a.d. 711, the Moors brought powerful armies from North Africa and launched a devastating attack on the Iberian p>
The Moors governed their Iberian kingdoms from across the border in Seville, but the Algarve had its own regional c>
The long struggle by Christians to expel the Moors (a campaign known as the Reconquista, or Reconquest) began towar>
The Reconquest of Silves, not achieved for another 50 years, was a grisly affair. A mixed bag of Crusaders from nor>
```

## `-s` command option
The `-s` option (standing for `squeeze-blank-lines`) prints out the file while without showing the blank lines in the file. In the example I've been using that `history.txt`, you might've noticed that the first few lines had some obsolete spaces at the beginning of the file. The `-s` command fixes that, but it does more than just remedy some graphical annoyances. I've done some cybersecurity exercises where there are a lot of empty lines in a file (`.txt`, `.log`, even `.jpg` files), and while some lines can be seemingly empty from a human perspective, they might not actually be. Some malware could be hidden after a million empty spaces, or there could be lines made entirely of no-break spaces that disrupt the code, but would be invisiable to the human eye. The `-s` option can help weed out some of these bugs.   

### Example
```
$ less -s history.txt

A Brief History
Little is known of the earliest Stone Age inhabitants of Europe’s southwestern extremity. The ancient Greeks called them the Cynetes (or Cunetes). Whatever their origins, their culture evolved under the pressure and influence of foreign forces. Among the many invading armies that settled here and contributed to nascent Portuguese culture were Phoenicians, who settled in the area around 1,000 b.c., followed by the Celts, Iberians, Greeks, and Carthaginians.
But it was the Romans, who arrived late in the third century b.c., who most greatly influenced all of Iberia. They built towns, industries, roads, and bridges, developed agriculture, and bequeathed the Latin language, of which Portuguese is a direct descendant. The Romans named the southwestern province of the peninsula Lusitania, oddly enough for one of the Celtiberian tribes they defeated, and by the third century a.d. had introduced Christianity. By the beginning of the fourth century the Algarve had a bishop in place, based in Faro. But Rome had already fallen into decay, and soon hordes of northern tribesmen took over the empire. The Algarve fell to the Visigoths in the mid-fifth century.
Under Moorish Rule

```
## In-command Moving and Searching
Besides the command-line accessible options available to the `less` command, there are also tools inside the program (besides the obvious up, down, left, and right arrows) we can use to navigate through it dexterously. 

### Jumps
* `g`: Goes to the first line in the file. Useful for when you're trying to get to data at or near the start of the file. 
* `G`: Goes to the last line in the file.U seful for when you're trying to get to data at or near the end of the file. 
* `{`, `(`, `[`, `}`, `(`, `]`: Jumps to the nearest open or closed bracket. This is very useful for debugging because a lot of languages use these brackets as the start or end of a condition or command, and this would help navigate to them quickly. 

### Moving
* `z`: Moves forward one window. Works faster than repeatedly spamming the down arrow. 
* `w`: Moves backward one window. Works faster than repeadly spamming the down arrow. 
* `e`: Moves forward one line, or N number of lines. Useful for debugging when you already know which line number the code that needs to be edited is on, then jump to it precisely. 
* `y`: Moves backward one line, or N number of lines. Similar to `e`, but backwards. 

###
* `/pattern`: Searches forward to (N-th) matching line. The pattern represents any input that you are searching for. Anyone who's ever used `Ctrl-F` in other documents knows the usefulness of being able to search through a document for a specific pattern. You comb through data faster than a human eye ever could. 
* `?pattern`: Searches backward to (N-th) matching line. Similar to `/pattern`, but backwards. 
* `&pattern`: Displays only lines that match the pattern. Useful for debugging, for example you can find all the `if` statements or `for` loops and view them all at once. 
