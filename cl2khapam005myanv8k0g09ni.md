## Commit Like a Pro

Committing changes is a common action that many developers do most of the time in case of contribution. You stage your changes and commit them so then they will be trackable in the [history](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History). But what about conventions? Any difference between a dirty commit and a clean fresh one? Using emojis for the commit message title? In this article, we are going to talk about some common conventions and `git commit` best practices in order to make perfect commits.

### 1. Staging Phase
Consider your changes as a performer. Before you commit your changes, your changes should have something to present on the stage. If they perform well, they are qualified to get committed otherwise, they'll be discarded. So it doesn't make sense if your changes don't perform but get committed.

#### When and what to stage
You have to make sure there is a relation between the changes you make on the lines. If you can describe the change in a few words so the next developer(s) can easily understand what you've done based on your commit message, you're all good. Even though you can make multiple lines of messages for your commits, never combine changes together.


### 2. Committing Phase

There is no problem if your project has hundreds of commits in its history. Git actually stores a manifest of files you have in your project so then you don't run out of space and resources so feel free to make commits whenever it's needed.

#### 2.1. What to commit
Git is a line-based version controlling system which means, it tracks the lines that have been changed not the actual phrase or word. If you change a single character from a line, that *line* will be tracked not the word. As we learned earlier, make sure the lines you've changed are related to each other as they work together to make a feature or serve something.

#### 2.2. How to combine hunks in commits
You can have multiple files changed in some blocks and add those blocks from any file and finally stage them and get ready for the commit. Consider a web project that has some CSS and JS files.  Imagine you add some paragraphs to the index file and now, you style them in the CSS file. Meanwhile, you make a function in the JS file for a contact form in your template. Simply use the `git add --patch` option to stage those specific blocks by answering some questions.

#### 2.3. Commit messages
Commit Message is the point where you contact the next contributor who's going to contribute to the same line(s) at a time. Let them feel pleased when they read your message. Basically, when you want to commit the staged changes, you need to put a message on them. Each commit message has a title and a description and some metadata. The developer needs to fill out the title. However, filling out the description is an optional task. The best practice is to keep it short and sensible that other developers be able to understand your changes via reading the commit title.

#### 2.4. Don't use emojis
I've seen some repositories have their own conventions in case of making commit messages. They actually use emojis to show the status of a commit whether it was a BugFix or Test or whatever kind of commit.

I personally avoid using emojis in my commit messages. You may have contributors from different platforms and interfaces. Since emojis use special ASCII codes (not commonly used and supported in the text-based interfaces like CLIs) and Unicode systems and most command-line interfaces need a third-party package or font to handle them, this convention might not look good to everyone. They might face some issues in terms of reading histories and checking the commit messages. (Like the emoji character in the message title might be rendered as its actual ASCII code or unknown question marks)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651235574920/H7a8bwc6d.png align="center")

In this case, the best practice is to use a prefix pattern to show the category of the commit like a word in a bracket at the beginning of the file. The following image uses the `type: message` convention by the way.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651236152821/JxWytytL3.png align="center")

#### 2.5. Message description
If you stage your changes and open the text editor once you want to commit your changes to submit a message, you can actually add some more information about the commit itself like necessities, bugs, TODOs (maybe), and so on. The title section is still the most important part of the commit message. In spite the description section is optional, feel free to write descriptions for your commits. If your changes are a bit complex that needs more explanations, you can write more about the different aspects of your changes in the description section.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1651237976985/Xi1FFKFOW.png align="center")

Finally, we can simply say that if you keep your commits simple and short as well as your commit messages, you'll almost hit the target.

### Different Git Conventions
Git doesn't make conventions at all. Conventions are designed by companies and teams. A team may find emojis so useful in their platform but the other one wants to keep it simple stupid. A team might push directly to the `main` branch (also known as the single-branch convention) but the other team has a `development` branch and only pushes the release commits to the `main` branch. If you're working somewhere where their conventions might not look good to you, you better follow them. The time you spend on changing their minds would probably help you to fix some bugs.

### Conclusion
In this article, we discover some basic `git commit` conventions and best practices. We talked about the pros and cons of each practice and finally, figured out that Git is not responsible for conventions and they are made by companies and startups.