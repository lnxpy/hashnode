# Introduction to Interactive Rebase in Git

Commits represent the developments. Git is a line-based Version Control System meaning it always keeps its eyes on the changes you make on each codebase line. Thus, once we have made our changes, we do some quick `git commit` commands and sign the changes we've made globally.

Accordingly, Git commits play a pretty important role during the development process, and being aware of all actions that might happen to them is highly required for each developer.

In this article, we're going to get our hands on the actions we could have when working with commits. The actions that could help us at the times we may think that it's too late. What's done is done.

In a nutshell, *let me introduce you to the CTRL+Z or ⌘+Z implementation of Git*.

### No More Messy Commits

Using Interactive Rebase will help us rewrite the history of our project. Thus, it covers, commit modifications, commit deletions, and pretty much every possible operation that can happen to the development flow of your workspace. In this quick guide, we'll be talking about quite a few popular use cases of Interactive Rebase but in fact, there are lots of other use cases in this great tool. Pretty much all the ways you can make use of Interactive Rebase are..

* Changing the commit messages you made earlier.
    
* Deleting commit(s).
    
* Reordering commits.
    
* Merging a bunch of commits into one commit.
    
* Splitting commits into multiple commits.
    

So, follow till the end of the article and see the examples and keep your Git history clean and perfect.

### Commit Message Modification

Sometimes, you may make mistakes in writing proper messages for your commits. That's all good. No room for panicking. Let's retrieve them back and replace them with neat perfect messages!

To change the most recent commit message (the latest commit you've made), simply use `--amend` followed by the message you desire. Although it helps you satisfy what you need, it's not related to either rebasing or interactive rebasing tricks. (It actually does the same job)

Here is the commit message that I've made which contains a typo issue that we're going to fix using `--amend`.

```bash
$ git log -1 --oneline
c8a2425 (HEAD -> main) index titel changed     # contains typo issue
$ git commit --amend -m "index title changed"  # fixing the typo
```

There it is. Now, if we print out the logs once again, we have to see the same exact commit changes but a different message.

```bash
$ git log -1 --stat --oneline
0134dfd (HEAD -> main) index title changed     # volla!
```

Notice the difference between the commit ID we had and have now. After re-writing the commit message, there is a new SHA1 commit hash assigned to the same commit that also contains the same changes. Well, that's kind of interesting but there appears to be a huge concern here. <mark>Keep in mind, having commits with different commit IDs on different machines may cause troubles during the development</mark>. We'll talk about it later on.

What if you want to change the message of a commit that is a little older?! Since it's not your latest commit, you can't use `--amend` option anymore. In that case, Interactive Rebase does the job for you.

```bash
$ git log --oneline
f76fae3 (HEAD -> main) error file added   # HEAD >> 1
a7e00da base html added                   #         2
0e134ec index foile added                 #         3 >> HEAD~3
0134dfd index title changed               #         4
```

The message with the commit ID of `0e134ec` doesn't seem to be alright. In fact, it has made our history a little nasty but no worries. Interactive Rebase could fix it in a flash. To reach that commit, we need to move backward three commits in order to catch the commit we want and do the operations. That way, we select from HEAD to three commits before it.

```bash
$ git rebase -i HEAD~3
```

That way, we'll have three commit details in our default text editor. It probably looks like the same thing that I brought you here.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675116588732/c70b5474-6a13-476c-9d28-b30e5627c2c2.png align="center")

As described in more detail in the comments, replace the word `pick` with `reword` right before the commit, you want its message to be changed. (Don't touch the commit message you see on the right side)

Your history should look like the following three lines now.

```bash
pick f76fae3 error file added
pick a7e00da base html added
reword 0e134ec index foile added
```

Then save and close the editor. Now, you're being asked for changing the commit message you just specified. In my case, I just resolve the typo issue and then close it.

Once again, print out the logs and check for changes we've made. Notice the diversity between hashes again. The issued commit ID is used to be `0e134ec` but it's not the same now.

```bash
$ git log --oneline
f76fae3 (HEAD -> main) error file added
a7e00da base html added
37a3867 index file added    # used to be "foile" also different ID
0134dfd index title changed
```

### Commit Combination

This topic is about combining multiple commits into one general commit. It's basically a crucial point that helps you keep your Git history clean and neat and avoid having different commits with the same purposes as follows.

```bash
$ git log --oneline
ds1x1e3 (HEAD -> main) base stylesheet added
a7e00da base script file added
29d201c index heading tag changed      # same!
0134dfd index title changed            # same!
```

As you can see, we have two commits that almost do the same purpose for us. They're all responsible for even the same index file. They're logically equal as that would be fine if we keep all their changes into one single commit.

That would be nicer if we combine (squash) them together and choose a better more general commit message for them. Let's fix them interactively. Select them based on your HEAD. It would be HEAD~4 and it'll contain all the last four commits.

```bash
$ git rebase -i HEAD~4
```

Replace the word `pick` with `squash` where you want to combine the commit with its above commit. To combine the last two commits, we need to put `squash` right before the last commit. Here it is.

```bash
pick ds1x1e3 base stylesheet added
pick a7e00da base script file added
pick 29d201c index heading tag changed
squash 0134dfd index title changed
```

Now, if you close your text editor, Git will attempt to get a commit message from you and combine both `0134dfd` and `29d201c` together labeled with that commit message you've entered.

### Interactive Rebase as a Threat

We discovered some important abilities of Interactive Rebase so far but there are some cases, you better be more careful and act a bit moderately.

As a team member, please keep in mind that Interactive Rebase might break some parts of the history in some cases since it rewrites the history at the time you use it. Therefore, never use this command (or any other commands with the same functionalities) for changing the commits you've already pushed to a remote repository.

Otherwise, it's highly recommended to use it while working in a more protected space like cleaning up the branch assigned to you or cleaning up the history of your local repository.

### Conclusion

In this article, we learned about some common operations we could have on the commits we've made followed by a few examples in cases. Practicing them would help you become more professional at Git-based collaborations. Lastly, we looked at the issues with the Interactive Rebase during the development of remote repositories and the cons of it.