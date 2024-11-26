#  interacting with the internet

##  content

`base64`  encode / decode base64 strings

`rev`  reverse the order of a text string

`touch`  create a file

`wget`  download files from the internet or a server

`curl`  download files from the internet or a sever, upload file via `FTP`

`jq`  parse java script object notation `JSON` data

`apt install {curl, venv, jq}`

`Python3 -m venv [virtual environment]`

`pip3 install pyftpdlib`

`python3 -m http.server`

`python3 -m pyftpdlib -w`

##  `base64`

`base64`  base64 encode / decode data and print to standard output

`$ base64 [OPTION] FILE`

Base64 encode or decode `FILE`, or standard input, to standard output.  with no `FILE` or when `FILE` is `-`, read standard input.

pertinent option 

`-d`  decode data

##  `rev`

`rev`  reverse lines characterwise

`$  rev [OPTION] FILE`

the `rev` utility copies the specified files to standard output, reversing the order of characters in every line.  if no files are specified, standard input is read.

##  `touch`

`touch`  change file timestamps

`$ touch [OPTION] FILE`

update the access and modification times fo each `FILE` to the current time.  if `FILE` argument that does not exist is created empty, unless `-c` or `-h` is supplied.

##  `wget` 

`wget`  the non interactive network downloader

`$  wget` [OPTION] URL`

`GNU Wget is a free utility for non interactive download of files from the web.  it supports `HTTP`, `HTTPS`, and `FTP` protocols, as well as retrieval through `HTTP` proxies.

pertinent options include

`-q`  turn off wget's output

`-i`  read urls from a local or external file

`-O`  the documents will not be written to the appropriate files, but all will be concatenated together and written to file.  if `-` is used as file, documents will be printed to standard output, disabling link conversions.

`-U`  identify as agent string to the http server

`-m`  turn on options suitable for mirroring

`-S` print the headers sent by `HTTP` servers and responses sent by `FTP` servers

`--user=user`  specify the username for both `FTP` and `HTTP` file retrieval

`--password=password`  specify the password for both `FTP` and `HTTP` file retrieval

`--ask-password`  prompt for a password for each connection established

```bash
❯ wget www.example.com
Prepended http:// to 'www.example.com'
--2024-11-26 14:09:26--  http://www.example.com/
Resolving www.example.com (www.example.com)... 2606:2800:21f:cb07:6820:80da:af6b:8b2c, 93.184.215.14
Connecting to www.example.com (www.example.com)|2606:2800:21f:cb07:6820:80da:af6b:8b2c|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1256 (1.2K) [text/html]
Saving to: ‘index.html’

index.html                 100%[=====================================>]   1.23K  --.-KB/s    in 0s

2024-11-26 14:09:26 (92.1 MB/s) - ‘index.html’ saved [1256/1256]
```

```bash
❯ head index.html
<!doctype html>
<html>
<head>
    <title>Example Domain</title>

    <meta charset="utf-8" />
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <style type="text/css">
    body {
```

##  `curl`

`curl`  transfer a `URL`

`$  curl [OPTIONS] URL`

`curl` is a tool for transferring data from or to a server.  it supports these protocols `DICT`, `FILE`, `FTP`, `FTPS`, `GOPHER`, `HTTP`, `HTTPS`, `IMAP`, `IMAPS`, `LDAP`, `LDAPS`, `POP3`, `POP3S`, `RTMP`, `RTSP`, `SCP`, `SFTP`, `SMTP`, `SMTPS`, `TELNET`, and `TFTP`.  the command is designed to work without user interaction.

pertinent options include

`-s`  silent or quiet mode.  do not show progress meter or error messages.  essentially makes `curl` mute

`-o`  write output to `<FILE>` instead of stdout

`-O`  write output to a local file named like the remote file we get

`-A`  http specify the user agent string to send to the http server

`-u <username:password>`  specify the username and password to use for server authentication

`-u <username>`  if you simply specify the username, curl will prompt for a password

`-T: <file>:`  this transfers the specified local file to the remote `URL`

`$  curl https://www.iana.org/help/example-domains | head`

##  `jq`

`jq`  command line `JSON` processor

`$  jq [OPTIONS] filter [files]`

jq can transform `JSON` in various ways, by selecting, iterating, reducing, and otherwise mangling `JSON` documents

pertinent options include

`-r`  don't parse the input as JSON.  instead each line of text is passed to the filter as a string

`-j`  like `-r`, but `jq` won't print a new line after each output

pertinent filter examples include



```
JQ(1)                                                                                             JQ(1)

NAME
       jq - Command-line JSON processor

SYNOPSIS
       jq [options...] filter [files...]

       jq can transform JSON in various ways, by selecting, iterating, reducing and otherwise mangling
       JSON documents. For instance, running the command jq ´map(.price) | add´ will take an array of
       JSON objects as input and return the sum of their "price" fields.

       jq can accept text input as well, but by default, jq reads a stream of JSON entities (including
       numbers and other literals) from stdin. Whitespace is only needed to separate entities such as 1
       and 2, and true and false. One or more files may be specified, in which case jq will read input
       from those instead.

       The options are described in the [INVOKING JQ] section; they mostly concern input and output
       formatting. The filter is written in the jq language and specifies how to transform the input
       file or document.

```




##  assessment

login into the `CS497QClient VM("Student")` and use it to interact with the `CS497QServer VM`.  the ip addressed assigned to the `CS497QServer VM` is `192.168.100.6`.   the answers to question 1 to 5 can be accessed via HTTP port 8080 on the `CS497QServer VM`.  the username for the `FTP` server is `student` and the password is `cs497q`.

