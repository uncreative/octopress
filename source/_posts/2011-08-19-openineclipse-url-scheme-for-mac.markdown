---
layout: post
title: "OpenInEclipse Url Scheme for Mac"
date: 2011-08-19 00:18
comments: true
categories: 
---

## What this does:
Enables you to externally open a specific file in eclipse, and go to some line

That is clicking on the following link:
[openineclipse://open?url=file:///etc/hosts&line=3](openineclipse://open?url=file:///etc/hosts&line=3)
Will open /etc/hosts file and go to line 3

## How to create this:

* open AppleScript Editor and paste

{% gist 1156457 openineclipse.applescript %}

* If your eclipse isn't located at "/Applications/eclipse/Eclipse.app", modify  

``` applescript
    set path_to_eclipse to "the/correct/absolute/path/of/Eclipse.app"  
```


* Save as Application OpenInEclipse.app under /Applications
* edit /Applications/OpenInEclipse.app/Contents/Info.plist and replace the last
        </dict>
        </plist>
with: 
{% gist 1156457 Info.plist %}

* Verify a link works:
[openineclipse://open?url=file:///etc/hosts&line=3](openineclipse://open?url=file:///etc/hosts&line=3)

{% gist 1156457 test_open_in_eclipse.html %}

## Integrate with xdebug 

* add the following to php.ini in the xdebug section:


``` ini
    xdebug.file_link_format="openineclipse://open?url=file://%f&line=%l"
```

* and restart apache:


``` bash
    $ sudo apachectl restart
```


## Troubleshooting

In the AppleScript Editor uncomment:

``` applescript
 	display alert "DEBUG: file " & filename & "   line " & line_number
```
 	
Click on link again:

* In the alert, are the filename and line_number parsed correctly? verify the href tag is correct or and that the code correctly parses the parameters

* The alert displays the filename correctly but it doesn't open:

    - Make sure path_to_eclipse is set to the correct location "/Applications/eclipse/Eclipse.app"

``` applescript
    set path_to_eclipse to "the/correct/absolute/path/of/Eclipse.app"  
```

* .
    - Make sure eclipse is able to open a file from terminal, maybe your eclipse version is too old?

``` bash
    $ open -a /path/to/your/eclipse.app /etc/hosts
```

 
* the file opens but it doesn't go to the line number: 

    ** for system events to work with key code, you must "Enable access for assistive devices" in "System Preferences" under "Universal Access"

    ** If you change the keyboard shortcut for go to line in eclipse, you'll have to change the following line to send the correct key

``` applescript
	 tell application "System Events" to key code 37 using command down #send command L 
``` 

finally, you can try to increase the sleep time before eclipse tries 'go to line' by modifying the following:


``` applescript
    set sleep_before_going_to_line to "0.5" # in seconds
``` 


* An alert does not display
** Check for the currently 


{% gist 1156457 force_registration_of_url_scheme.py %}

