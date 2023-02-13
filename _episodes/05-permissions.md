---
title: "File Permissions"
teaching: 30
exercises: 25

questions:
- "How does Linux know who can access files?"
- "How can I see what permissions a file has?"
- "How can I set or change the permissions on a file?"
objectives:
- "View file permissions"
- "Understand the structure of the permissions string"
- "Change owners and permissions of files"
- "Use binary references to change permissions of files"
keypoints:
- "We can list permissions for a file or folder using the `-l` flag with `ls`"
- "The order of permissions groups is **owner**, **group** and **others**"
- "The types of permissions are **read**, **write** and **others**"
- "Use the `chown` command to change both owner and group associated with a file/folder"
- "Use `chmod` to change permissions."
- "Binary reference is made up of r=4, w=2 and x=1"
---

Every file or folder in Linux has a set of permissions associated with it. These define who can access the file or folder and see or interact with them. Each file or folder has three types of entities that can have permissions assigned to them. These are, User, Group and all others. They have the following definitions:

- **owner** - The Owner permissions apply only the owner of the file or directory, they will not impact the actions of other users. 

- **group** - The Group permissions apply only to the group that has been assigned to the file or directory, they will not effect the actions of other users. 

- **all users** - The All Users permissions apply to all other users on the system, this is the permission group that you want to watch the most. 


Let's start by going back to the `molecules/` directory and quickly viewing the permissions of the `methane.pbd` file.

~~~
$ cd molecules
$ ls -l methane.pdb
~~~
{: .language-bash}

~~~
-rw-r--r--  1 user  staff   422B  8 Aug  2019 methane.pdb
~~~
{: .output}

The command `ls -l` lists the files in the current folder and displays them in the long listing format. While this may initially look complex, we can break this down in the following left to right order:

1.  A set of ten permission flags
2.  Link count (which is irrelevant to this course)
3.  The owner of the file
4.  The associated group
5.  The size of the file
6.  The data that the file was last modified
7.  The name of the file

The permission flags are the important thing we want to look at here. We can further break these down into the following three basic permission types:

- **Read** - Which refers to a user's capability to read the contents of the file. 
- **Write** - Which refer to a user's capability to write or modify a file or directory. 
- **Execute** - Which affects a user's capability to execute a file or view the contents of a directory.

Each of these permission types is listed in the `_rwxrwxrwx` section of the output. The first character marked by an underscore is the special permission flag that can vary. It shows things like whether the item is a directory.

- The following set of three characters (rwx) is for the owner permissions. 
- The second set of three characters (rwx) is for the Group permissions. 
- The third set of three characters (rwx) is for the All Users permissions. 


> ## On users and groups
> When listing the contents of a directory you may come across files that 
> have the same text for both the user and group.
> An example of this is in the output `-rw-r--r--  1 c.whcrm9  c.whcrm9   422B  1 Sep  2019 test.txt`
> In Linux, users will usually have a group associated with them that shares the same name that the user does. 
> While this can seem strange, make sure that you understand the difference in the output so you 
> know who has access to your files.
{: .callout}

> ## Can you spot the difference here? What does it mean?
> Let's take a look at some files in a different folder.
> ~~~
> $ cd Desktop/data-shell/north-pacific-gyre/2012-07-03
> $ ls -l
> ~~~
> {: .language-bash}
> ~~~
> -rw-r--r-- 1 user  staff  4406  8 Aug  2019 NENE01729A.txt
> -rw-r--r-- 1 user  staff  4400  8 Aug  2019 NENE01729B.txt
> -rw-r--r-- 1 user  staff  4371  8 Aug  2019 NENE01736A.txt
> -rw-r--r-- 1 user  staff  4411  8 Aug  2019 NENE01751A.txt
> -rw-r--r-- 1 user  staff  4409  8 Aug  2019 NENE01751B.txt
> -rw-r--r-- 1 user  staff  4401  8 Aug  2019 NENE01812A.txt
> -rw-r--r-- 1 user  staff  4395  8 Aug  2019 NENE01843A.txt
> -rw-r--r-- 1 user  staff  4375  8 Aug  2019 NENE01843B.txt
> -rw-r--r-- 1 user  staff  4372  8 Aug  2019 NENE01971Z.txt
> -rw-r--r-- 1 user  staff  4381  8 Aug  2019 NENE01978A.txt
> -rw-r--r-- 1 user  staff  4389  8 Aug  2019 NENE01978B.txt
> -rw-r--r-- 1 user  staff  3517  8 Aug  2019 NENE02018B.txt
> -rw-r--r-- 1 user  staff  4391  8 Aug  2019 NENE02040A.txt
> -rw-r--r-- 1 user  staff  4367  8 Aug  2019 NENE02040B.txt
> -rw-r--r-- 1 user  staff  4381  8 Aug  2019 NENE02040Z.txt
> -rw-r--r-- 1 user  staff  4386  8 Aug  2019 NENE02043A.txt
> -rw-r--r-- 1 user  staff  4393  8 Aug  2019 NENE02043B.txt
> -rwxr-xr-x 1 user  staff   345  8 Aug  2019 goodiff
> -rwxr-xr-x 1 user  staff   218  8 Aug  2019 goostats
> ~~~
> {: .output}
> The data files in this folder, e.g `NENE01978A.txt` have a different permission set to `goodiff`.
> Can you tell why this is and explain what this might mean for the `goodiff` file?
> > ## Solution
> > The `goodiff` file has the execution flags set for user, group and all.
> > Which will allow anyone to execute the file. It's therefore likely that `goodiff` is a script that
> > preforms some actions. In theory you could run this script using `./goodiff`
> {: .solution}
> Lets take a further look at things by looking at in the folder above this.
> ~~~
> $ cd ..
> $ ls -l
> ~~~
> {: .language-bash}
> ~~~
> drwxr-xr-x 21 user  staff  672  8 Aug  2019 2012-07-03
> ~~~
> {: .output}
> Can you guess what the `d` at the beginning of the output line means?
> > ## Solution
> > The `d` indicates whether the file has any special type associated with it. In this
> > case it's indicating that this is a directory.
> {: .solution} 
{: .challenge}


## Modifying permissions
Let's say we want to modify who can access some of the files in the `molecules/` directory. We'll assume here that we're members of the `scw1148` on our system. On the Hawk supercomputer run by ARCCA, all users must be members of project groups to run jobs on the system. Each project has a group associated with it, so we can use this method to share files with other members of the same project.

We'll start by changing the ownership of the methane.pdb file so everyone who is a member of the `scw1148` group is able to read this file.

> ## Groups
> You'll find that if you try to assign a group to a file and the group 
> does not exisit you'll get something similar to the following output.
> ~~~
> chown: scw1148: illegal group name
> ~~~
> {: .output}
> If you're trying to do this locally, you can list the groups you're currently a member of using the `groups`
> command like so:
> ~~~
> $ groups
> ~~~
> {: .language-bash}
> Just pick one of these groups to demonstrate the method shown below.
{: .callout}

~~~
$ cd Desktop/data-shell/molecules
$ chown c.whcrm9:scw1148 methane.pdb
~~~
{: .language-bash}

We can break the `chown` command down into the following parts. The command itself, `chown`. The user we want to set `c.whcrm9`. The group we want to set, `scw1148` and the filename `methane.pdb`. When we list the contents of the directory again, we would see the change reflected like so:
~~~
total 48
-rw-r--r-- 1 user  staff  1158  8 Aug  2019 cubane.pdb
-rw-r--r-- 1 user  staff   622  8 Aug  2019 ethane.pdb
-rw-r--r-- 1 c.whcrm9  scw1148   422  8 Aug  2019 methane.pdb
-rw-r--r-- 1 user  staff  1828  8 Aug  2019 octane.pdb
-rw-r--r-- 1 user  staff  1226  8 Aug  2019 pentane.pdb
-rw-r--r-- 1 user  staff   825  8 Aug  2019 propane.pdb
~~~
{: .output}

Now lets say we want to allow members of the group to be able to make changes to this `methane.pdb` file but don't want anyone else to see or edit this file. To do this, we'll need to change the permissions of the file. To explicitly define permissions you will need to reference the Permission Group and Permission Types. 

The Permission Groups used are: 
- **u**	- Owner 
- **g** - Group 
- **o** - Other / All Users

The Permission Types that are used are: 
- **r** - Read 
- **w** - Write 
- **x** - Execute 

The potential Assignment Operators are **+** (plus) and **-** (minus); these are used to tell the system whether to add or remove the specific permissions. 

First, let's remove the ability for other users to read the `methane.pdb` file. We can do this by specifying the **o** permission group, the **r** permission type and the **-** (minus) operator. The command that we use to modify permissions is `chmod`.

~~~
$ chmod o-r methane.pdb
~~~
{: .language-bash}

Checking this has gone through using `ls -l`:

~~~
total 48
-rw-r--r-- 1 user  staff  1158  8 Aug  2019 cubane.pdb
-rw-r--r-- 1 user  staff   622  8 Aug  2019 ethane.pdb
-rw-r----- 1 c.whcrm9  scw1148   422  8 Aug  2019 methane.pdb
-rw-r--r-- 1 user  staff  1828  8 Aug  2019 octane.pdb
-rw-r--r-- 1 user  staff  1226  8 Aug  2019 pentane.pdb
-rw-r--r-- 1 user  staff   825  8 Aug  2019 propane.pdb
~~~
{: .output}

Good, we can see that the **r** flag has been removed from the other users section of the ten permission sets.

Now lets continue by allowing all members of the `scw1148` group to write or edit the file.

~~~
$ chmod g+w methane.pdb
~~~
{: .language-bash}

And again, checking this has gone through using `ls -l`:

~~~
total 48
-rw-r--r-- 1 user  staff  1158  8 Aug  2019 cubane.pdb
-rw-r--r-- 1 user  staff   622  8 Aug  2019 ethane.pdb
-rw-rw---- 1 c.whcrm9  scw1148   422  8 Aug  2019 methane.pdb
-rw-r--r-- 1 user  staff  1828  8 Aug  2019 octane.pdb
-rw-r--r-- 1 user  staff  1226  8 Aug  2019 pentane.pdb
-rw-r--r-- 1 user  staff   825  8 Aug  2019 propane.pdb
~~~
{: .output}

Excellent, now all members of the group can both read and write to the `methane.pdb` file. You can apply this same method to any files that you have write permissions over.

> ## Changing permissions for all files in a directory?
> Say we want to change the permissions for all the files in the `molecules/` directory, how we would do this?
> Let's try and give apply what we've just learnt to give all other users write permissions over the files.
> > ## Solution
> > There's actually a few ways we can go about this and it really depends on how we target the files to change.
> > First, we could use the wildcards we learnt about previously to target files based on a specific pattern.
> > In this case a simple * would suffice to pick out every file in the current folder, e.g:
> > ~~~
> > $ chmod o+w *
> > ~~~
> > {: .language-bash}
> > We could also use the recursive flag avaliable to the `chmod` command to run through every file 
> > in a directory **(including sub-directories)** and apply a set of permissions to every file. E.g:
> > ~~~
> > $ cd ..
> > $ chmod -R o+w molecules/
> > ~~~
> > {: .language-bash}
> > Either method works in this case, however be wary that as the `-R` flag works through the folder 
> > and all sub-folders, you may end up changing the permission on something you didn't intend.
> {: .solution}
{: .challenge}


## Using Binary References to Set permissions 
Now that you understand the permissions groups and types this one should feel natural. However, there is another way to set the permission using binary references. This replaces the explicitly defined permissions with binary references to these. While more complex than the previous method, we can use this to define multiple different permissions to all three permissions groups with a single command.

A sample permission string would be `chmod 640 methane.pdb`, which means that the owner has read and write permissions, the group has read permissions, and all other user have no rights to the file. 

The first number represents the Owner permission; the second represents the Group permissions; and the last number represents the permissions for all other users. The numbers are a binary representation of the **rwx** string where; 
- r = 4	
- w = 2	
- x = 1 

You add the numbers to get the integer/number representing the permissions you wish to set. You will need to include the binary permissions for each of the three permission groups. 

For example, issuing the follow command changes the permissions assigned to `methane.pdb` to allow the owner both read and write to the file, group members read the file and everyone else read the file. Or, the original permissions this file had.

~~~
chmod 644 methane.pdb
ls -l methane.pdb
~~~
{: .language-bash}

~~~
-rw-r--r--  1 c.whcrm9  scw1148   422B  8 Aug  2019 methane.pdb
~~~

> ## Using binary references, how can you make a file executable?
> Now we've seen how to use binary references to change permissions on a file. Can you change the `methane.pdb`
> file to make it executable? In this case, you can't actually execute the file as it doesn't contain the right
> data to do this, but it will teach you how to do this for other files in future, most notably scripts.
> > ## Solution
> > To ensure that we don't make unintended changes to the other permissions currently assigned to the 
> > file, we need to first check what permissions it currently has
> > ~~~
> > $ ls -l methane.pdb
> > ~~~
> > {: .language-bash}
> > ~~~
> > -rw-r--r--  1 c.whcrm9  scw1148   422B  8 Aug  2019 methane.pdb
> > ~~~
> > {: .output}
> > We can see that both the read permission flags are set for groups and others. This makes creating the binary
> > reference here easy as we only need to take the integer 4 for both these flags. 
> > Now we have the end of the binary reference, we need to add up the rest to give execute permissions to the
> > file. As we already have read and write permissions as the owner of the file, we only need to add 1 to the 
> > binary reference to get 7. Therefore, the full binary reference we need to set is 744.
> > ~~~
> > $ cd ..
> > $ chmod 744 methane.pdb
> > ~~~
> > {: .language-bash}
> > ~~~
> > -rwxr--r--  1 c.whcrm9  scw1148   422B  8 Aug  2019 methane.pdb
> > ~~~
> > {: .output}
> > Here, the first 7 assigns **read, write, execute** to owner, the first 4 adds **read** to the group, 
> > and the last 4 adds **read** permissions to others.
> {: .solution}
{: .challenge}
{: .output}



