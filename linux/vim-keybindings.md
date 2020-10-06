## Switching Modes
Key | Description
--- | ---
Esc | switch to command mode
i | switch to insert mode
: | switch to line mode

## Line Mode
Key | Description
--- | ---
:r \<file> | read in file and insert at current position
:w | write to file
:w \<file> | write out to specified file
:w! \<file> | overwrite specified file
:x or :wq | write out to file and exit vim 
:q | quit vim
:q! | quit vim even though modifications have not been saved
--- | ---
:0 | move to beginning of file
:n | move to line n
:$ | move to the last line of file
--- | ---
:sh | opens an external command shell. After you exit the shell, you will resume the vim editing session
:!   | execute a command within vim. `%` represents the file currently being edited

## Command Mode
Key | Description
--- | ---
j | Move one line down
k | Move one line up
h | Move one character left
l | Move one character right
--- | ---
0 | Move to beginning of line
$ | Move to end of line
H | Move to the first line on screen
L | Move to the last line on screen
w | Move to beginning of next word
b | Move to beginning of previous word
e | Move to end of next word
--- | ---
Ctrl + F or Page Down | Move forward one page
Ctrl + B or Page Up | Move backward one page
^l | To refresh and center screen
**Search for text** |
/pattern | Search forward for pattern
?pattern | Search backward for pattern
n | Move to next occurence of search
N | Move to previous occurrence of search
**Working with text** |
a | Append text after cursor
A | Append text at end of current line
i | Insert text before cursor
I | Insert text at beginning of current line
--- | ---
o | Start a new line below current line, insert text there
O | Start new line above current line, insert text there
--- | ---
r | Replace character at current position
R | Replace text starting with current position
cw | Changes the word at the current position
--- | ---
x | Delete character at current position
Nx | Delete N characters, starting at current position
dw | Delete the word at the current position
D | Delete the rest of the current line
dd | Delete the current line
Ndd | Delete N lines
--- | ---
u | Undo the previous operation
yy | Yank (copy) the current line and put it in buffer
Nyy | Yank (copy) N lines and put it in buffer
"cY | Yank a line to the c (named buffer)
p | Paste at the current position the yanked line or lines from the buffer
"cp | Paste after the current line the contents of the c named buffer
"1P | Paste the first line of the file over the current line