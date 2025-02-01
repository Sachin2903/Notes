#                     Linux Operating System


## Basic understanding

> data is transfer through cables

IP ADDRESS --> ISP (Internet Service Provider ) --> Optical Fiber --> Data Center

> Server ( Server / Dilever information )
* email server
* file server
* DB server
* App server

> Client ( Request / consume  infomation )

> DNS ( WHo map / linked IP Address to Domain )

> Application vs Web Server
Application :- Dyanmic Data
Web Server :- Static Data

user <--> (Apache / nginx ) <--> web server <--> Application server

> Type of Application
* Standalone Apps
Applications that run locally on a single device without needing internet connectivity.

* Web Application
Applications accessed via a web browser that typically require an internet connection. They may have both static and dynamic content.

## Linux
* Open source OS
* unix (paid eg:- MacOS) vs linux (free) 

> use linux through
* WSL
* VM
* AWS
etc

* shell ( Cmd ) >> linux kernel 
* bootloader ( GRUB ) :- run files and setup envonment to run OS  

![alt text](./assests/architecture-of-linux.png)

## Linux Commands

> top
--> runnning process
PS 1 is the file that run first
Procss state :- Sleeping . running , terminated , zombie

> df -h
--> disk space

> free -h
--> see ram

> cd
--> change directory

> cd ../
--> move back

> cd /
--> go to root folder

> ls

> cd /var/logs
--> all logs

> cd Users
--> show users

> date
--> show todat date

> mkdir
--> create directory

> pwd
--> Show present directory path

> touch eg:- touch file.txt
--> create a file

> rm , rmdir
--> delete file and folder 
-r: The -r (or --recursive) flag tells rm to delete the directory and all its subdirectories and files, recursively.

> cat file name
--> show data inside file

> echo "hello dosto" > demofile.txt
--> print data in a file , id file is not exist it create  a file and add that text

> zcat file name
--> see inside zip file

> head myfile.txt
--> print top 5 file

> tail myfile.txt
--> print last 5 line

> tail -f nmyfile.txt
--> show update data live

> less and more file.txt
--> show large file data

> cp source_filename destination_file_name
--> copy one file data to another file

> cp -r source_folder destination_folder
--> copy data from directory to destination folder

> mv souce_file  detination file
--> move a file and rename a directory and file

> wc ( word count ) filename
--> show line words size_of_file_in_bytes myfile.txt
can work with 1 or more file

> soft and hard links
--> ln -s file_name destination (soft link)
--> ln file_name destination (hard link)

> cut -b 1-4 filename.txt
--> show words from index

> echo "hello" | tee
> echo "hello" | tee hello.txt
--> use to put on screen or in file 

> sort filename.txt
--> sort text

> diff file_name file_2
--> difference between file

can not differe more than 2 file

> vi (editor)
vi file.txt > i > esc > :wq > enter


## connect one linux to another

ssh
secure shell generate a private key



> ssh -i privatekeypath ubuntu@ce2address
--> connnect ec2 server on out plateform

































