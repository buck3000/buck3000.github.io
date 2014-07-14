---
layout: post
title: "Unix File Permissions: A Starter Guide"
description: "Read the title ya dope."
category: 
tags: [Linux, Unix, File Permissions]
---
{% include JB/setup %}

I've spent most of my time over the past year as a fledgling programmer being terrified of file permissions -- essentially being afraid of breaking something. While conciously I know that breaking things is how you learn, I also consciously didn't want to do anything horrible to my laptop (which is essentially a personal heirloom) so I tended to outsource those issues to programmer friends with more experience. When none of those people were available I would either 1) google errors and sudo like crazy with mixed results or 2) cry in a corner.

Today though I decided to dig into the file permissions monster on my computer and fight back (or at least read a few things on the internet about changing permissions and ownership). The result is this idiot's guide to file permissions: 

To correct / fight the file permissions monster you must first see what you're up against. To list the current file permissions for a given directory (and its contents) use the command 'ls -l'.

Now you're going to get a bunch of output (or just one line if you listed a specific file after ls -l) that looks like this:

-rw-r--r-- 1 root root 2453 Jul 17 16:25 File.txt (pretend this is the name of one specfic file i ls-l-ed.)

If you're a beginner, the odds are you're looking at that and thinking "wtf?!" or "I'm going to go watch the critically acclaimed indie action movie Snowpiercer instead of this." Don't. Or wait, maybe eventually watch Snowpiercer because it rules. But not now. We're going to decode this:

The first character in this output denotes the file type: - means regular file, d means directory.
The next three characters (in this case rw-) tell you what the permissions are for the user who owns the file. r is read, w is write and x is execute. - is the absence of a permission (Bummer, dude). The next three characters are the permissions for the group that owns that file. The last three are the permissions for every user / sucka that uses your computer.

Oh also -- g means group, u means user and o means other (as in any other person can do whatever the permissions for o specify to your file. Not good peeps.)

The first word following all that is the user who owns whatever is going on (often root or your username). The word after that is the group that has permissions regarding the file. Often this is admin or wheel. Wheel generally refers to the super user group (or su, as in sudo) which is why you have to sudo all the time if you have no f-ing idea what you're doing. 

So now you know what all this shit is. What do you do about it? 

While often if you're working on your own machine you want to own your own files. There are two main commands that change permissions though and we'll go over both of them:

chmod - change permissions

chown - change ownership

So depending on your status as a user you may have to use sudo here (try not to though.) If you want to own the file we discussed earlier the syntax is:

chown BUCK (or whatever your username is) PATH-TO_FILE/FILENAME (just put in whatever you imagined eariler...)

If you want to change the owner for a whole directory (and its contents 'recursively') the command has to have a -R so: 

sudo chown -R BUCK /CRAZY-FOLDER

If you already own it and want to change the permissions you can do a few different things and your syntax looks like this:

chmod ugo+rwx file.txt (or whateva) 

That command means any user, group, other can read, write and execute. You can also with a quick google search you can find octal notation and do this numerically. Analagous syntax for the above item would be:

chmod 777 file.text

Generally, when you're editing permissions (at least for me personally) you want to own and be able to read / write and execute -- the octal syntax for that is:

chmod 755 file.txt

That makes it readable and executable by everyone and writable only by the owner (which generally is me.)

That's what I know about file permissions. Hopefully it was helpful. If not please send an email to my secretary at traviswbrimm@gmail.com .

