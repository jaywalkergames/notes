Bourne-Again SHell. Common in Unix enviornments.

Shell: The program that provides a CLI to the OS.
`sudo du -cha --max-depth=1 /var/log/postgresql/ | grep -E "M|G"`
### General Command Format: command [OPTIONS] arguments

```bash
man # Lists commands
ps # Determing shell
date # Display today's date
pwd # Display present working directory
ls # List the contents of the current directory
echo # prints value of a variable to the terminal
```

### Scripting

.sh extension by naming convention

Start with #!

Find path to bash with “which bash:”

```bash
#!/path/to/bash
echo "Hello $1!"
# $1 is first command line argument. ./hello.sh joey prints Hello Joey!

# Read from a file line by line
while read line
do
	echo $line
done < input.txt

# Write to a file
echo "This is some text." > output.txt

# Append to a file
echo "More text." >> output.txt

# Redirect output
ls > files.txt

# Conditional
if [[ condition ]];
then
	statement
elif [[ condition ]]; then
	statement 
else
	do this by default
fi
i=1

# Switch
case expression in
    pattern1)
        # code to execute if expression matches pattern1
        ;;
    pattern2)
        # code to execute if expression matches pattern2
        ;;
    pattern3)
        # code to execute if expression matches pattern3
        ;;
    *)
        # code to execute if none of the above patterns match expression
        ;;
esac

# While loop
while [[ $i -le 10 ]] ; do
   echo "$i"
  (( i += 1 ))
done

# For loop
for i in {1..5}
do
    echo $i
done

# cron
# min, h, day, month, weekdays
* * * * * sh /path/to/script.sh

# exit codes
$? # 0 indicates success of last command

# grep [OPTION...] PATTERNS [FILE...]
# Finds a pattern in a file

# tail [OPTION]... [FILE]...
# Outputs last 10 lines of file

# sed OPTIONS... [SCRIPT] [INPUTFILE...]
# find and replace on a file

# tr [OPTION] SET1 [SET2]
# replace characters of set 1 with characters of set 2 or none

# awk options 'selection _criteria {action}' input-file > output-file
# Performs action on each satisfying selection_criteria in input_file and saves to output_file
awk '{print NR,$1,$4}' employee.txt # prints first and fourth word to output. NR is the line number
```
### find
```bash
find <path> <conditions> <actions>
```
conditions
```bash
-name "*.c"
-user jonathan
-nouser
-type f            # File
-type d            # Directory
-type l            # Symlink
-depth 2           # At least 3 levels deep
-regex PATTERN
-size 8            # Exactly 8 512-bit blocks 
-size -128c        # Smaller than 128 bytes
-size 1440k        # Exactly 1440KiB
-size +10M         # Larger than 10MiB
-size +2G          # Larger than 2GiB
-newer   file.txt
-newerm  file.txt        # modified newer than file.txt
-newerX  file.txt        # [c]hange, [m]odified, [B]create
-newerXt "1 hour ago"    # [t]imestamp

-atime 0           # Last accessed between now and 24 hours ago
-atime +0          # Accessed more than 24 hours ago
-atime 1           # Accessed between 24 and 48 hours ago
-atime +1          # Accessed more than 48 hours ago
-atime -1          # Accessed less than 24 hours ago (same a 0)
-ctime -6h30m      # File status changed within the last 6 hours and 30 minutes
-mtime +1w         # Last modified more than 1 week ago

\! -name "*.c" # NOT named "*.c"
\( x -or y \)
```
actions
```bash
-exec rm {} \;
-print
-delete
```
### grep
```bash
grep <options> pattern <file...>
```
options
```bash
-e, --regexp=PATTERN
-f, --file=FILE
-i, --ignore-case
-v, --invert-match
-w, --word-regexp
-x, --line-regexp

-F, --fixed-strings   # list of fixed strings
-G, --basic-regexp    # basic regular expression (default)
-E, --extended-regexp # extended regular expression
-P, --perl-regexp     # perl compatible regular expression

-B NUM, --before-context=NUM  # print NUM lines before a match
-A NUM, --after-context=NUM   # print NUM lines after a match
-C NUM, -NUM, --context=NUM   # print NUM lines before and after a match

-c, --count           # print the count of matching lines. suppresses normal output
    --color[=WHEN]    # applies color to the matches. WHEN is never, always, or auto
-m, --max-count=NUM   # stop reading after max count is reached
-o, --only-matching   # only print the matched part of a line
-q, --quiet, --silent
-s, --no-messages     # suppress error messages about nonexistent or unreadable files
```
# AWK
X
# GNU Parallel