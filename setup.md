---
title: Setup
---

> ## Prerequisites
> * Go to <a href="https://uor.topdesk.net/tas/public/ssp/content/serviceflow?unid=ca8f1436fbd246bbb75f19fb448debe3">the UoR Topdesk portal</a> to request access to the VPN and, importantly, quote the ref: I-1909-5956 in the field "Additional information". Alternatively, you can also email a request to access the VPN to it@reading.ac.uk, quoting the same ref. Following the link to read more information <a href="https://www.reading.ac.uk/internal/its/help/its-help-networks/pcsecurity-setupvpn.aspx">about installing Pulse Secure</a>, the software enabling VPN connection.
> * Have an account on the CINN Nutanix platform. Please ask me if you run into trouble.
> 
{: .prereq}

### Ready, steady, ... Go!

Assuming you have completed the tutorial on bash shell, and have successfully launched a CINN Virtual Machine, you can find the folder we will use for PYM0FM using the command “cd” and list the files, and folders within that folder using the command “ls” (that’s a lower-case L and a lower-case s).

Note also that in the box below, the “$” represents the prompt for the bash, i.e. where you will type the command; you should not type the “$”, just type what comes afterwards, as it is shown. You can also copy-paste it into the shell, if that's easier.

~~~
$ cd /storage/silver/pym0fm
$ ls
~~~
{: .language-bash}

At this point, bash should show you a list of folders, including one that has named after your IT login.

~~~
au820779  course_material  ip820428  ly804792  nx824248  ro830628  ub834672  xo833295
bin	  dp001965	   jk015241  ml830974  oo825180  tv828654  we837461
bu807041  ib907932	   lo831025  nm818719  pn809625  tz901918  xi831850
~~~
{: .output}

### Find the data

In the command terminal, if you haven’t done it already, go to your folder on the PYM0FM folder, by typing the below, and replacing your ITS login accordingly;

~~~~
$ cd /storage/silver/pym0fm/<YOUR ITS LOGIN>
~~~~
{: .language-bash}

Then use the “ls” (that’s an “l” as in lullaby) command to see a list of files in the directory, simply type:

~~~~
$ ls
~~~~
{: .language-bash}

~~~
~~~
{: .output}

You will see.... nothing. :) This is your folder, where you will store your data and analyses. At the moment, there is nothing to show. Let’s start by adding some data, type:

~~~~
$ cp ../course_material/fsl_course_data.tar.gz .
$ ls
~~~~
{: .language-bash}

You will now see that, inside your folder, there is one file. The “cp” command copied a file from a different folder, using a path relative to where you are currently standing: Assuming you are in your folder “..” indicates to bash that it should go one folder up, and then go to ../course_material. The final “.” at the end of the command tells “cp” that it should copy the file where you are currently standing.

~~~
$ ls -al
~~~
{: .language-bash}

This adds parameters to the “ls” command, to show details about the files (using “-l”) and also to show any hidden files (using “-a”): you can, but you don’t have to, combine the two parameters “-l” and “-a” into a single set of parameter, into “-la”. This gives you more information about the file we have just copied inside your folder. It should show something like the following:

~~~
-rw-r--r--  1 tz901918 stor-silver-pym0fm 5348460464 Oct 22 13:16 fsl_course_data.tar.gz
~~~
{: .output}

The output above is about the file named “fsl_course_data.tar.gz”, which is contained in the original folder /storage/silver/pym0fm/course_material/. I created it, and my IT login is tz901918.

When you type “ls -al” inside your own folder, provided that you typed the “cp” command above as instructed, you should see a copy of the file fsl_course_data.tar.gz that has appeared inside your folder.

The “ls -al” command will give you quite a lot more information than just the name. You can see that the file is about 5GB large, 5,348,460,464 bytes to be precise. You can see that you have created it (as part of the group stor-silve-pym0fm), and are thus the owner of the file, and you can see that it has the following permissions: -rw-r-\-r-\- which should read in groups of 3 letters:

* The first dash "–" says it is not a directory, and it’s a file, otherwise it would read “d” (for directory)
* The second group of 3 letters corresponds to the permissions you personally have over this file: "rw-" means you can read and write, but cannot execute the file.
* The second group of 3 letters corresponds to the permissions any users belonging to your group (stor-silver-pym0fm) have over my file: “r-\-” means they (anybody else in the calss) have read permission, but they can’t write or execute the file.
* The third group of 3 letters corresponds to the permissions anybody else (who is not me, and not in the same group as you, i.e. anybody else in CINN) have over your file: “r-\-” which means they have read permissions, but cannot write or execute the file.

This file is compressed. That means it is an entire folder compressed into a single file that will take much less space than if it was not compressed. Yes, the file is currently 5GB, and the uncompressed folder will be larger. In your folder, type:

~~~
$ tar xvzf fsl_course_data.tar.gz
~~~
{: .language-bash}

After a little while, the command will have uncompressed the file, and created a folder called “fsl_course_data”, which contains a selection of data for you to play with. You can always repeat this procedure if you want to start anew.

Visit the folder, and try to figure out what this is.

> ## Exercise
>
> Visit the folder, and look at the subfolders to identify what they are.
>
> > ## Solution
> >
> > By now, you probably figured out that you can use the commands "cd" and "ls" to move within the folder. Each subfolder contains a different kind of data file. Carry on with the tutorial to see what they are!
> >
> > ~~~
> > $ ls
> > ~~~
> > {: .language-bash}
> > ~~~
> > fsl_course_data.tar.gz      fsl_course_data_UNMODIFIED
> > ~~~
> > {: .output}
> > ~~~
> > $ cd fsl_course_data_UNMODIFIED
> > $ ls
> > ~~~
> > {: .language-bash}
> > ~~~
> > fdt  fmri  intro  melodic  reg   scripting  seg_struc  tbss
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

{% include links.md %}
