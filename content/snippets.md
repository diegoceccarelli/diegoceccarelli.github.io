+++
title = "Snippets"
+++

## Code Snippets

This page contains a small collection of (mainly) bash commands that I discovered during the Ph.D. Bash is evil but during the Ph.D. was often useful to get stuff done quickly (and it is still useful today). 

### [bash] print a beer icon in a script

```bash
    echo $'\360\237\215\272'
```

or

```bash
    echo $'\360\237\215\270'
    echo $'\360\237\215\271'
    echo $'\360\237\215\273'
    echo $'\360\237\215\274'
```

From [http://codepoints.net/miscellaneous_symbols_and_pictographs](http://codepoints.net/miscellaneous_symbols_and_pictographs)

### [bash] copy the output of a command to the clipboard (on macosx) 

```bash
    echo "pippo" | pbcopy
```
	
Now `cmd+v` will paste `pippo`. 


### [bash] zcat does not work on MACOS (.Z bug) 

```bash
	sudo mv /usr/bin/zcat /usr/bin/broken-zcat
	sudo ln -s /usr/bin/gzcat /usr/bin/zcat
```

### [bash] awk insert blank line every n lines

```bash
    awk '{ if ((NR % 5) == 0) printf("\n"); print; }'
```

For `n == 5`, of course. Substitute whatever your idea of `n` is.
	

### [bash] convert windows source file to unix 

```bash
	dos2unix *.py
```

### [bash] remove first column from a file 

```bash
	cut -f2- filename
```

### [bash] replace delete with backspace in screen 

You can define an alias in your `~/.bashrc` file like:

```bash
  alias screen='TERM=screen screen'
```
 

### [bash] sort using tab as separator 

```bash
  sort -t$'\t' -k 2 file
```

### [java] change java heap size 

```bash
  java -Xmx<size> set maximum Java heap size
```

e.g., `java -Xmx4196m Pippo`

### [bash] resolve redirected url 

```bash
  URL=...
  REDIRECT_URL=$(curl -w %{redirect_url} URL) 
```
 

### [bash] get a txt file edited from pirate pad 

```bash
curl http://piratepad.net/ep/pad/export/$id/latest?format=txt
```



###  [bash] dump a website 

```bash
wget -r -H -l1 -k -P $targetdir --exclude-domains ${comma-seperated domain name} --user=xxx --password=xxx $url
```

### [bash] get a webpage with autentication 

```bash
url= ""
outpage = ""
user=""
pass=""
curl -u $user:$pass $url >  $outpage
```


### [linux] 10 nice hints

[http://web.archive.org/web/20111229021312/http://www.ibm.com/developerworks/linux/library/l-10sysadtips/](http://web.archive.org/web/20111229021312/http://www.ibm.com/developerworks/linux/library/l-10sysadtips/) 

### [bash] how to get the sum of all the lines in the file  

```bash
awk '{a+=$0}END{print a}' abc
```

### [python] remove the garbage collector in python 

When you are working with a big data structure in python the garbage
collector can slow down the execution, sometime can make sense to disable it.  

```bash
import gc
gc.disable()
```

### [bash] how to query solr from the shell 

[https://cwiki.apache.org/confluence/display/solr/Solrj#](https://cwiki.apache.org/confluence/display/solr/Solrj#)

... Or just use python and the package [pysolr](https://pypi.org/project/pysolr/).

### [bash] sum rows with the some field 

dictionary in awk:
```bash
$ cat nayan.out
saman 1
gihan 2
saman 4
ravi 1
ravi 2

$ awk '{arr[$1]+=$2} END {for (i in arr) {print i,arr[i]}}' nayan.out > nayan.out.tmp

$ cat nayan.out.tmp
ravi 3
saman 5
gihan 2
```

### [maven] resources in a jar 

[http://stackoverflow.com/questions/1266615/maven-configuration-of-dependency-jar](http://stackoverflow.com/questions/1266615/maven-configuration-of-dependency-jar)

### [bash] get all pdf in a page 

```bash
  wget -m --accept=pdf -nd  $url
```

### [bash] iterate over the lines of a jar 

```bash
while read line
do
echo $line
done < file_to_read
```

### [bash] remove blank lines in a file 
```bash
grep -v '^[[:space:]]*$'  file
```

### [bash] change tmp folder where sort put temporary files 
```bash
sort -T dir ...
```

### [bash] print number of a specific char for each line of a file  

```bash
awk -F'#' '{ print NF-1}' 
```

It will print how many chars '#' per line

### [bash] replace a substring 

```bash 
i=pippo.txt
echo ${i/txt/tex}
```

It will print `pippo.tex`

### [bash] sort on more than one field 
```bash
sort -k 1,1 -k 3,3nr file.tsv > tmp
```

It sorts on the first field and if two elements are equal on the first, on the third field in reverse integer order

### [bash] remove all files of size 0 

```bash
find . -type f -size 0k -exec rm {} \; | awk '{ print $8 }'
```

### [bash] remove all chars in a particular position from a file 

```bash
cut -c42- file
```
It removes the first 42 characters from all the lines of a file.

### [bash] view what is appended on file 

```bash
tail -f file -n 
```

### [bash] get words distribution from a file  

```bash
cat file | tr '[A-Z]' '[a-z]' | tr -sc '[a-z]' '\n' | grep -v '^[^a-z]*$' | grep -v '^[\]'  |    sort | grep -vxf topwords-ita.txt | uniq -c   | sort -nrk1
```

### [bash] tr complement 

```bash
tr -sc '[a-zA-Z]' '\n' < file
```
It replaces all chars that are **not** alphabetic in new lines

### [bash] remove first or last lines  

```bash 
 sed '1d' filename 
```
To remove the first line

```bash 
 sed '$d' filename 
```
To remove the last line 

### [bash] Generate all the couples of terms 

```bash
tr -sc '[a-zA-Z0-9\n]' '\t'  < inputFile | awk '{for (i = 1; i < NF; i++) print $i"\t"$(i+1); }'
```

### [bash] Find a process listening on a particular port  

```bash
sudo netstat -lpn | grep :8080
```

### [bash] Check for proper number of command line args  

```bash
EXPECTED_ARGS=1
E_BADARGS=65

if [ $# -ne $EXPECTED_ARGS ]
then
  echo "Usage: `basename $0` {arg}"
  exit $E_BADARGS
fi
```

###  [bash] Sort in numeric order with scientific notation allowed	

```bash
sort -g
```

### [bash] create ssh pub key 

```bash
<ssh-keygen -t rsa -C "your_email@example.com"
# Creates a new ssh key, using the provided email as a label
# Generating public/private rsa key pair.
# Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```

Now you need to enter a passphrase.

```bash
Enter passphrase (empty for no passphrase): [Type a passphrase]
# Enter same passphrase again: [Type passphrase again]
```

Copy `id_rsa.pub` in `.ssh/authorized_key` to login on a remote machine without password.  

### [bash] gzip a folder 

```bash
  tar -czf folder_name.tar.gz folder_name/
```
### [git] change the commit message

```bash
  git commit --amend -m "New commit message"
```

### [git] undo latest commit (e.g., if you commit -a -m instead of commit -m) 

```bash
  git reset --soft HEAD^
```