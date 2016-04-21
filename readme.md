# Git stuff done
## Oh yeah I went there

## The Git cheat sheet for *you*!
##### But in Soviet Russia, YOU cheat on GIT!

## SECTION 1
### Don't be a basic clone

Do you know what SSH is?

It stands for secure-shell, and here's a helpful definition:

> SSH IS THE ONLY WAY TO DO NETWORKING
> – Abraham Lincoln

Here's how some people will tell you to use git:

```bash

~ $ git clone https://github.com/NUisEPIC/epic-site-redesign.git

```

And those people are **wrong**. Don't listen to them, because
they are n00bs and they use HTTP. You don't wanna be a noob. You
gonna use SSH.

```bash

~ $ echo This is how you clone like a pro
This is how you clone like a pro

~ $ git clone git@github.com:NUisEPIC/epic-site-redesign

```

So why is SSH superior?

Because:

* It's encrypted by a private/public keypair that *you* control
  * Unlike a password, which -- although you came up with it! -- it's someone else's
    job to make sure it doesn't get stolen!
  * Sub-lesson: don't trust other people to store your identity!
* You can SSH into all the things
* You don't have to enter a password anymore
* You don't have to *remember* a password anymore
* You'll be one of the cool kids
  * Listen to Abe Lincoln
    * Honest Abe can't tell a lie

## SECTION 1.1
### How to set up SSH, combat evil, and impress that nerdy girl in your CS class

Setting up ssh is easy, assuming you're using a Unix-based computer. (OS X counts. Although
it is inferior to Ubuntu and other Linux distros. </judgment>)

```bash

~ $ ssh-keygen -t rsa -b 4096 -C "This is a comment about my SSH key, if I want one."

```

Let's break that down.

`-t rsa`: What type of encryption? We use RSA, because it's a strong, well-tested standard.

**NOTE**: DON'T TRY OUT THE OTHER ENCRYPTION OPTIONS. Many of them have security flaws, like DES.

`-b 4096`: How many bytes of security do we want? The trick here is picking a big
           number that isn't too cumbersome. We have to send this key in all our ssh requests,
           after all, so we don't want it to be too big. (In fact, TCP limits the size a payload
           can have, so there's a hard limit on how big you can make your SSH key.) In general,
           bigger is better. 4096 bytes is a pretty popular choice, and it's big enough to be secure.
           Now, that's only 4kb, but you'll be sending this around a lot, so again, size is of the essence.

Now ssh-keygen will ask you some questions, and you can accept the default answers.

You'll now have a folder called `.ssh` in your home directory, or User folder, depending on your OS.
Inside of that folder will be **TWO** SSH keys: the public key (id_rsa.pub) and the private key
(id_rsa). NEVER NEVER NEVER give ANYONE your PRIVATE KEY. EVER. If you do, you're giving away the
"secret" that only you are supposed to know. Think of your private key as if it's the pad of your
index finger. Would you cut off the pad of your index finger and give it to your friend so that
they could get into your iPhone? No. That's gross. Don't cut off your fingers. Don't give away
your private SSH keys.

Now, the last step: log into GitHub and upload your public key (the id_rsa.pub) to your account
under the "SSH Keys" tab in your user settings. You'll have to copy/paste the file into GitHub.

BAM! You just kicked it up a notch!

## SECTION 2
### Git-ting closer

Now let's actually talk about Git.

#### Git lets you time travel through infinite universes.

Branches and projects are "universes," and advanced git commands like `rebase` and `commit --amend` will allow you to travel through time.

Every git project has three "zones"

Here's a quick reference of most basic Git commands, with descriptions:

| Command                              | Arguments                                           | Explanation                                                                                                                                                         |
| -----------                          | ---------------                                     | ------------                                                                                                                                                        |
| git status                           | none                                                | The most important git command: gives a summary of what's going on in this git project folder                                                                       |
| git init                             | none                                                | Make a git project in this directory                                                                                                                                |
| git init \<directory\>               | a directory                                         | Make a git project in *that* directory                                                                                                                              |
| git add .                            | none                                                | Add the specified files to "staging"                                                                                                                                |
| git add --all                        | none                                                | ''                                                                                                                                                                  |
| git add \<files\>                    | files to stage                                      | Add the specified files to "staging"                                                                                                                                |
| git commit                           | none                                                | Commit the files in "staging" to history (aka "committed")                                                                                                          |
| git remote add \<name\> \<place\>    | a helpful name and an ssh url                       | Tell git about a far away place where you'd like to put things                                                                                                      |
| git push remote \<name\>             | push changes to a remote server                     | Synchronize my files with the server                                                                                                                                |
| git pull remote \<name\>             | pull changes from a remote server                   | ''                                                                                                                                                                  |
| git checkout \<branch-name\>         | checkout a 'branch'                                 | Get a *temporary* workspace by name                                                                                                                                 |
| git checkout -b \<branch-name\>      | make a new branch and check it out                  | ''                                                                                                                                                                  |
| git push remote :\<name\>            | delete a faraway branch                             | Clean up your remotes by deleting old branches with push-colon (push colon - kinda like what you do when you're pooping.)                                           |
| git branch -d \<name\>               | delete a branch here                                | Clean up your local project folder by deleting old branches                                                                                                         |
| git log --oneline --graph --decorate | none                                                | Tell me stories about my past conquests: this command gives a visual history of your commits                                                                        |
| git merge \<branch\>                 | branch to merge with                                | Don't use this, it makes your history really messy                                                                                                                  |
| git rebase -i \<branch\>             | branch to 'rebase' onto; -i is for 'interactive'    | Travel through history, rewriting it so that your changes happen in order on the other branch                                                                       |
| git commit -p                        | files to commit, otherwise defaults to staged       | Travel through my un-saved commits and pick and choose which ones to commit now, and which ones to leave for later                                                  |
| git pull -r remote \<branch-name\>   | pull changes and rebase them onto your working dir  | Uses the incredible time-traveling power of rebase to rewrite history so that you agree with the history on the remote server                                       |
| git push -f remote \<branch-name\>   | 'force' push your changes to the remote             | *CAUTION* use very carefully, this obliterates the remote record of history with your record, potentially losing anything the two of you didn't agree on beforehand |
| git checkout --theirs                | clobber your local changes when there are conflicts | If you're sure that some other history is better than yours, you can skip over correcting merge conflicts by accepting it as truth with this command                |
| git checkout --ours                  | throw away remote changes when there are conflicts  | If you're sure that you're on the right side of history, you can tell git to trust you and shut up with this command                                                |

