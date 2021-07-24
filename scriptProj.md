# A Brief Scripting Project
## Script 47
It must be a pain to always be killing the same processes over and over again. Let's build a very simple script that can kill processes given a file of shady processes we need to kill.
##### (do not include sudo inside your script, allow the user to sudo the script themselves
### Some Guidlines:
#### Input Text File
In practice, we would probably use smth like pgrep to get fresh pids/names specific to our situation then dump them into a file. We could also make a simple script for that, for example to pgrep all processes related to ssh and write them to a file.

The given file contains a different process to be killed per line. We will accept both PID and name, so brute force both. There may be undesirable leading or trailing whitespace per line. Thus, DO NOT use IFS in your script.
Example: 
```
      shadyMcShades
apache2                      
 firefox
              3105
  n3rdh4x0r  
```
#### Pseudocode
This script is pretty generic, and you can do it however you like. Remember, theres many ways of reading file input, but they're all pretty similar. Go with what works for you. This is a pseduocode outline.

```
#!/bin/bash

read filePath

# can we use quotes or brackets here? do we need to?
fileName=$filePath

# how can we read the file line by line?
# google is your friend here, fill in the ???

while ???; do
# an invalid pid or process name will produce an error but not stop our script
# thus we do not need to check for validity, simply shotgun through
# if you'd like you can add extra flavor in this body, like hit confirm, etc
  killByName
  killByPID
done ???

# you can simply exit on completion, or if you'd like, make the script ask if the user wants to try another file

```
