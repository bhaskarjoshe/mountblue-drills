# CLI

## Practice Drill 1

###  1. Create the following directory structure. (Create empty files where necessary)

```
mkdir hello
cd hello
mkdir five six
cd five
mkdir six
cd six
touch c.txt && mkdir seven
touch seven/error.log
cd \~/hello/one
touch a.txt b.txt && mkdir three
cd three
touch d.txt && mkdir three
cd three
touch e.txt && mkdir four
touch four/access.log
cd \~
tree hello
```
### Explanation -
> cd : to navigate in the directories
> cd \~ : home directory
mkdir : to create a directory
touch : to create a file
tree : give branched structure


**2) Delete all the files having the ******.log****** extension**

Command - find . -name \"\*.log\" -exec rm {} +

Explanation -

{

find . -- means that it will search in the current directory and all
subdirectories

-name "\*.log" - -name flag is used to match a pattern which in this
case is all files ending with .log

-exec rm {} + -- execute flag is used here to perform a specific
function which is remove. Also for the execute a batch is made under {}
and which has been l ocked by + at the end so that after all the log
files are found in the batch then only rm performs it's action (so that
rm doesn't have to run again and again)

}


**3) Add the following content to ******a.txt****

'Unix is a family of multitasking, multiuser computer operating systems
that derive from the original AT&T Unix, development starting in the
1970s at the Bell Labs research center by Ken Thompson, Dennis Ritchie,
and others'

Steps :

1\. cd hello/one\
2. cat \> a.txt\
* Unix is a family of multitasking, multiuser computer operating systems
that derive from the original AT&T Unix, development starting in the
1970s at the Bell Labs research center by Ken Thompson, Dennis Ritchie,
and others\
3. *cat a.txt

Explanation -

cat : to view a file

cat \> : to add text into the file

** 4) Delete the directory named ******five****

Steps -

1\. cd ..

2\. rm -r five

**5) ******Rename the ******one****** directory to ******uno****

**mv one uno**

**

****6)******Move ******a.txt****** to the ******two****** directory****

** Step1 - cd uno**

** Step 2 -mv a.txt two/a.txt**


# ****Practice Drill 2****

### Pipes

1.  **Download the contents of \"Harry Potter and the Goblet of fire\"
    using the command line
    from *(https://raw.githubusercontent.com/bobdeng/owlreader/master/ERead/assets/books/Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt)

    -   Steps-

        1\. mkdir harryPotter

        2\. curl -o book.txt
        <https://raw.githubusercontent.com/bobdeng/owlreader/master/ERead/assets/books/Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt>

Explanation :

curl -o : curl or Client URL is used to transfer data and -o the
transferred data into book.txt.

1.  -   

2.  Print the first three lines in the book

head -n 7 book.txt \| tail -n 3

(head gives lines from starting and tail gives line for the end)

1.   Print the last 10 lines in the book

    -   tail -n 10 book.txt

2.  How many times do the following words occur in the book?

         -   Harry - grep -o \'Harry\' book.txt \| wc -l

         -   Ron - grep -o \'Ron\' book.txt \| wc -l

         -   Hermione - grep -o \'Hermione\' book.txt \| wc -l

         -   Dumbledore - grep -o \'Dumbeldore\' book.txt \| wc -l

Single Command - grep -o -E \"Harry\|Ron\|Hermione\|Dumbledore\"
book.txt \| s ort \| uniq -c

> (Explanation -- grep: matches required text

> -o: give match of only inputed text

> -E: to match multiple values at one

> sort : sort everything in alphabetic order

> uniq-c: gives count of unique elements)

1.  Print lines from 100 through 200 in the book

    -   head -n 200 book.txt \| tail -n 101

        or

        awk 'NR\>99 && NR\<201' book.txt

        (awk is used here to select row numbers from 100 to 200)

2.  How many unique words are present in the book?

    -   tr -c \'\[:alnum:\]\' \'\\n\' \< book.txt \| sort \| uniq -c \|
        wc -l

        (Explanation-

        tr -c '\[:alnum\]' '\\n') \<book.txt : tr or translate here is
        used to manipulate the text. So, first of all book.txt is
        inputed in tr and -c (complementary) flag takes two argments(i
        this case \[:alnum:\] and \\n ), so -c leaves all the first
        arguments and except them converts all the other things into a
        new line so that every word is seperated into a new line

        sort \| uniq -c \| wc -l : now words in every line are sorted so
        same words come together, then there count is done and at last a
        sum of all is output by wc.

### Processes, ports

1.  List your browser\'s process ids (pid) and parent process ids(ppid)

    ps -eo pid,ppid,comm \| grep brave

    1.  Explanation-

        1.  ps: process status

            -e: every processe

            -o : output format which is pid(process id),ppid(parent
            process id),comm(command)

    2.  Stop the browser application from the command line

        kill 9039 (pid taken from earlier step)

        1.  or

        pkill -9 brave

2.  List the top 3 processes by CPU usage.

    1.  top -o %CPU \| head -n 10

3.  List the top 3 processes by memory usage.

    1.  top -o %MEM \| head -n 10

4.  Start a Python HTTP server on port 8000

    1.  python3 -m http.server 8000

5.  Open another tab. Stop the process you started in the previous step

    1.  Step 1 - ps aux \| grep http.server

        Step 2 -- kill 26462

6.  Start a Python HTTP server on port 90

    1.  sudo python3 -m http.server 8000

7.  Display all active connections and the corresponding TCP / UDP
    ports.

    1.  netstat -tuln (t -- tcp, u -- udp, l -listening ports,
        n-numerical address)

8.  Find the pid of the process that is listening on port 5432

    1.  netstat -tuln \| grep 5432

### Managing software

** Use ******apt****** (Ubuntu) or ******homebrew****** (Mac) to:**

1.  1.  **Install ******htop******, ******vim****** and ******nginx****

**** ****sudo apt install htop**

** sudo apt install v**im**

** sudo apt install ngi**nx** **

** **

1.  1.  **Uninstall ******nginx****

        1.  1.  **sudo apt uninstall nginx**

                **

Explanation- sudo : grants admin permission ,apt : advanced package
tool; to install new packages

########## Misc

1.  What\'s your local IP address?

    1.  ifconfig \| grep inet \| head -n 1 \| awk \'{print \$2}\'

        (ifconfig -- interface configuration to look for all networks )

2.  **Find the IP address of ******google.com****

**** ****nslookup google.com **

** **(nslookup -- to look for dns and ip)**

** **or**

** host google.com**

1.  How to check if Internet is working using CLI?

    1.  ping -c 4 8.8.8.8

        (if it fails then network connection is not there)

2.  **Where is the ******node****** command located? What
    about ******code******?**

whereis node && whereis code

**
