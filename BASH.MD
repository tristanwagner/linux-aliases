# - `$?` - exit status of the last executed command
 
  ## echo
  a=hi
  echo $a \\(planet\\) # hi (planet)
  echo '$a (planet)' # $a (planet)
  echo "$a (planet)" # hi (planet)
  echo # empty line
 
  ## variables
  a=Hello
  b="Hello World"
  c=16
  echo $a
  echo $b
 
  ## command substitution
  # - use `$()` to take output of some command
  d=$(pwd)
  echo $d
 
  ## math
   - `(( expression ))` -- as variable `val=$(( expresion ))`
  a=2
  b=$((a+2))
  echo $b
 
  ## comparison
 : '
   - `[[ expresion ]]` **0 = True** , **1 = False**
   - comparing strings `==` `!=` `>` `<` `<=` `>=`
   - comparing intigers `-eq` `-ne` `-gt` `-lt` `-le` `-ge`
   - logic operations `&&` `||` `!`
   - **is null?** = `[[ -z $a ]]` , **is not null?** = `[[ -n $a ]]`
   '
 
  [[ "cat" == "cat" ]]
  echo $?
 
  [[ "cat" = "car" ]]
  echo $?
 
  [[ 20 -gt 100 ]]
  echo $?
 
  a=""
  b="cat"
  [[ -z $a && -n $b ]]
  echo $?
 
  ## working with strings
 : '  
   - concatenation `$a$b`
   - length of string `echo ${#a}`
   - substring `echo ${c:3}`
   - substring from end of the word `echo ${c: -4}`
   - substring four characters after third one `echo ${c:3:4}`
   - substring first three letters from last four `echo ${c: -4:3}`
   '
 
  a="hello"
  b="world"
  c=$a$b
  echo $c         # helloworld
  echo ${#c}      # 10
  echo ${c:3}     # loworld
  echo ${c: -4}   # orld
  echo ${c:3:4}   # lowo
  echo ${c: -4:3} # orl
 
  ## replace string with another one
 
  fruit="apple banana banana orange"
  echo ${fruit/banana/kiwi}        # apple kiwi banana orange
  echo ${fruit//banana/kiwi}       # apple kiwi kiwi orange
  echo ${fruit/#apple/kiwi}        # it replace only if it is begining of the string
  echo ${fruit/%orange/kiwi}       # it replace only if it is end of the string
  echo ${fruit/o*/kiwi}            # pattern matching # apple banana banana kiwi
 
  ## colors
 : '
   - `-e` = allow escape characters `echo -e ...`
   - (foreground, background) -> black = (30,40); red = (31,41); green = (32,42) => yellow, blue, magenta, cyan, white = (37,47)
   - **0** - no style; **1** - bold; **3** - italic; **4** - underline; **7** - reverse
   '
 
  flashred="\\033[5;31;40m"
  red="\\033[31;40m"
  none="\\033[0m"
  echo -e $flashred"Error: "$none$red"Something went wrong"$none
 
  ## date
 : '
   - `date` -> `Mon Jan 28 10:32:11 CET 2019`
   - `date +"%d-%m-%y` -> `28-01-19`
   - `date +"%H:%M:%S` -> `10:32:11`
   - `man date` - for more options
   '
  ## printf
 : '
   - `printf "Name:\\t%s\\nID:\\t%04d\\n" "bendo" "13"`
   - `printf -v d` - use `-v` to store result to variable **d**
   - `echo "$d"` - double quotes to respect new lines
   '
 
  today=$(date +"%d-%m-%Y")
  time=$(date +"%H:%M:%S")
  printf -v d "Current User:\\t%s\\nTime:\\t\\t%s @ %s\\n" $USER $today $time
  echo "$d"
 
  ## arrays
  a=() # empty array
  b=("apple" "banana" "orange") # three elements in array
  echo ${b[2]} # orange
  b[5]="kiwi"
  b+=("mango") # add element to the end of array
  echo ${b[@]} # echo whole array
  echo ${b[@]: -1} # echo last element of array
  # like map
  declare -A myarray
  myarray[blue]=color
  myarray["two words"]="another words"
  echo ${myarray[blue]} and ${myaaray["two words"]}
 
  ## files
  echo "Some text" > file.txt # write to file.txt - creates file if doesn't exist
  > file.txt # zero out file.txt - make it empty
  echo "Some more text" >> file.txt # writes to end of file.txt
 
  # to read file.txt
  i=1
  while read f; do
      echo "Line $i: $f"
      ((i++))
  done < file.txt
 
  cat < file.txt # use cat to read the file
 
  ## here documents
 
  # to print some long text or instructions
  cat <<- EOF
  Some really long
  text, like help,
  or like documents.
  EOF
 
  # to run some commands
  ftp -n <<- DownloadDocument
      open mirrors.xmission.com
      user anonymous nopass
      ascii
      cd gutenberg
      get GUTINDEX.00
      bye
  DownloadDocument
 
  ## if statement
  if expression; then
      echo "True"
  elif expression2; then
      echo "ex False, ex2 True"
  else
      echo "False"
  fi
 
  ## loops
  i=0
  while [ $i -le 10 ]; do
      echo i: $i
      ((i+=1))
  done
  j=0
  until [ $j -ge 10 ]; do
      echo j: $j
      ((j+=1))
  done
 
  for i in {1..100}
  do
      echo $i
  done
 
  # another variant
  for (( i=1; i<=10; i++ ))
  do
      echo $i
  done
 
  # array
  arr=("apple" "banana" "cherry" "kiwi" "mango")
  for i in ${arr[@]}
  do
      echo $i
  done
 
  # command subtitution
  for i in $(ls)
  do
      echo $i
  done
 
  ## case
  a="dog"
  case $a in
      cat) echo "miow miow";;
      dog|puppy) echo "huf huf";;
      *) echo "No match";;
  esac
 
  ## functions
  greet() {
      echo "Hi $1. What a nice $2"
  }
  echo "And now greetings."
  greet Ben Morning
  greet Everybody Evening
 
  numberthings() {
      i=1
      for f in $@; do
          echo $i: $f
          ((i+=1))
      done    
  }
 
  numberthings $(ls)
  numberthings haskell elm python
 
  ## arguments
 : '
   - `$@` - array of arguments
   - `$#` - number of arguments
   '
 
  echo $1 $2 # first and second argument
 
  for i in $@
      do
          echo $i
      done
     
  echo "There were $# arguments."
 
  ## flags
  while getopts :u:p:ab option; do  # : means I do wait some value for u: p:
      case $option in               # for ab I just want to know if it was used
          u) user=$OPTARG;;         # if : is used before then I want check flags which are not specified
          p) pass=$OPTARG;;
          a) echo "got the flag a";;
          b) echo "got the flag b";;
          ?) echo "I don't know what $OPTARG is";;
      esac
  done
  echo "User: $user / Pass: $pass"
 
  ## read
  echo "What is your name?"
  read name
  echo "What is your password?"
  read -s pass # silent you will not see characters while typing
 
  read -p "What is your favorite language? " lang
  echo name: $name, pass: $pass, lang: $lang
 
  ## select
  select animal in "cat" "dog" "spider" "fly"
  do
      echo "You selected: $animal"
      break
  done
 
  select option in "cat" "dog" "quit"
  do
      case $option in
          cat) echo "Cats like cuddle";;
          dog) echo "Dogs like to run";;
          quit) break;;
          *) echo "I am not sure what that is";;
      esac
  done
 
  ## ensure response
  # checks number of arguments, if not enough it will write message
  if [[ $# -lt 3 ]]; then
      cat <<- EOF
          This command requires three arguments:
          username, userid and favorit number.
      EOF
  else
      echo "Username: $1"
      echo "Userid: $2"
      echo "Favorite number: $3"
  fi
 
  # till option is satisfied
  read -p "Favorite animal? " a
  while [[ -z "$a" ]]; do
      read -p "I need an answer! " a
  done
  echo "$a was selected."
 
  # predefined option
  read -p "Favorite animal? [cat] " a
  while [[ -z "$a" ]]; do
      a="cat"
  done
  echo "$a was selected."
 
  # checking input with regexp
  read -p "Which year? [nnnn]" year
  while [[ ! $year =~ [0-9]{4} ]]; do
      read -p "A year please! [nnnn]" year
  done
  echo "Selected year: $year"
