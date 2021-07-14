# Homework 0
### Hey there! 
My name's Ricky Deng, and I look forward to teaching you guys **Unix Tools 101**.
I'll make "homeworks" but these won't be real homeworks, just worksheets basically.

This one may be too easy for some and too hard for others, but its mostly for me to get to know you and hopefully vice versa.

I'd like to teach for Attack-Defense CTFs rather than jeopardy, since I enjoy real world applications and Jeopardy CTFs is in large part self-study knowledge anyway.

#### For starters, how about name, grade, and experience so I can get a handle on things.
```
Ricky Deng; College Sophomore; CS enjoyer
```
### Let's try some quick practical knowledge.
**FEEL FREE TO USE ALL RESOURCES AT YOUR DISPOSAL!**
**You can also reach out to me if you feel like my questions are ambiguous.**

**More importantly, if you feel *TOO BEHIND* or *TOO AHEAD*, let me know.**

I've just hired you for a job at my networking and cybersec company, Ricky Corporation. Because of the coronavirus situation, all company employees will need to connect remotely to a secure remote desktop via ssh. All company employees should have access to a full featured terminal for company assignments.

Your company email will be *yourname@rickycorp.org*. 
The company's remote server is *remotedesktops@rickycorp.org* .
Let's say your login username is your company email and password is *rickyCorpPassword12345abcde*.

<br>
Your home PC is running Windows. Describe how you would connect to your remote desktop. 
<details> 
	<summary>Hint</summary>
	Windows built-in RDP is a textbook, but half credit answer.
	Try a third party terminal for Windows. (Mobaxterm, PuTTy)
</details>

<details> 
	<summary><em><b>Learning Objective</b></em></summary>
	Do we know the basics of ssh remote connection?
</details>

```
We could use built-in Windows features, but we know we're in a big company that runs on linux.
In a real world situation, we would want a professional-grade solution: an enhanced terminal / ssh client.
```

Uh oh, your PC broke and you've decided to pick up a company laptop, running Ubuntu 20.04.2.0. It is an untouched and fresh installation, with no third party programs. You connect with the command ```ssh remotedesktops@rickycorp.org ``` , and you want to open and edit a file called welcomeFriend.md. What is the full command to do this?
<details> 
	<summary><em><b>Learning Objective</b></em></summary>
	Do we know how to use basic Linux tools?
</details>

```
gvim welcomeFriend.md

If you're keen, you'll notice a few things. 
Do I even have permissions to open this file? 
Here, we assume yes, but consider what we can do if I didn't.
Notice also that the command I used was simply 'ssh remotedesktops@rickycorp.org' on the standard ubuntu terminal.
This means X11 forwarding is not enabled so I will not able to use a GUI for gvim; we address this in the next question.
```

Did you use vim or gvim in the previous command? If you used gvim, you may have realized that you got a "could not display" error. How can you fix this, and why did it happen?
<details> 
	<summary>Hint</summary>
	X11 forwarding for ssh.
</details>
<details> 
	<summary><em><b>Learning Objective</b></em></summary>
	<br>
	Can we solve simple real world issues?
	<br><br>
	This situation happened to me the first time I connected to a remote desktop. I was trying to access the gui of a debug program on a remote desktop, however I had not enabled X11 forwarding.
</details>

```
gvim is a GUI and thus we need X11 forwarding for ssh.
ssh -X remotedesktops@rickycorp.org to enable X11 forwarding.
ssh -Y is also an acceptable answer for trusted X11 forwarding.
```

### Advanced Text Manipulation
<details> 
	<summary><em><b>Learning Objective</b></em></summary>
	<br>
	This is the most you should ever reasonably need in terms of text manipulation.  
	<br>
	<br>
	However, we should also know or reference common vim commands when necessary.
	Helpful ones include setnu to show line numbers and :wq to save and quit.
	<br><br>
	(For people who have not used vim before, if you simply exit out without saving, this can break your files, creating duplicate "ghost" files of previous versions that you may want to clean up.)
	<br><br>
	The vim command being tested here is find and replace with wildcards.
	This can be helpful when writing codes or scripts and you need to replace variable names or other mistakes.
	<br><br>
	A similar command would be the popular grep command, typically used with piping and cat. Grep sees much more use in CTFs, simply because it allows you to search file systems with relative ease. It can be great for scripting.
	<br>
	<br>
</details>

Upon opening **welcomeFriend.md**, you realize that it's actually a textfile of the usernames and passwords of all 100,000 employees of our company! All stored in plaintext! What a great welcome present from your boss! Each line contains 2 username and password duos like so:

```
username1password1username2password2
```

Looking over your boss's instructions, it seems like the file was to help you get to know everyone's usernames and should have been a collection of all employee's usernames and the letter X after each username, but instead of the letter X, your boss pasted all the passwords.

We want this ouput per line:

```
username1Xusername2X
```

Luckily, you notice that every password starts with rickyCorpPassword and ends in a string of alphanumeric characters. 
Company policy also dictates that employees should have username starting with rickyCorpUsername.

Let's fix your boss's mistake!

<details> 
	<summary>Hint 1</summary>
	Let's try using vim to open the file. (or you can use the grep approach)
	What vim commands could we use to search and replace?
</details>

<details> 
	<summary>Hint 2</summary>
	We want to find and replace all passwords with 'X'. 
	<br>
	The passwords start with a string they all have in common: 'rickyCorpPassword' and end with a random unique string. This means we want to use a wildcard in our search.
</details>

```
Let's open the file with vim. Then we'll use 2 vim commands:
:%s/rickyCorpPassword.*rickyCorpUsername/XrickyCorpUsername/g
:%s/rickyCorpPassword.*/X/g

%s means substitute in all lines
/ is our delimiter
first string is the value we're searching for and the second string is what we replace it with
.* is regex for wildcard (. means any character (not linebreak) and * means repeated any # of times)
the g flag at the end means "global," this checks for multiple occurences per line
(not to be confused with % we used to check all lines)
```
