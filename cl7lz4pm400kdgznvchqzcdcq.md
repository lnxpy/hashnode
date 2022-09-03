## Branch Like a Pro

A branching strategy is a flow that a team follows to write, merge, or even deploy a software product in a Version Control System (VCS). Today, we're going to talk about some of the most popular strategies and the factors you should choose your proper strategy based on. That strategy is the flow of your project's development.

We are going to understand the strategies, and best branch naming conventions and find the techniques we can use to choose the best flow for our software or web application. We may not cover all strategies in this blog post, but you'll be introduced to the most useful ones by following them towards the end.

As we described in ["Commit Like a Pro"](https://imsadra.me/commit-like-a-pro), we are facing so many conventions here as well. The strategy that your team observes in the company may differ from other places (e.g. public marketplaces like GitHub) which means, companies may have their branching strategies which are rare these days and not recommended since we have so many perfect conventions and strategies introduced by the great teams, influencers, and companies as well.

Enough talking, let's dive in.

## 1. Private Repositories
First thing first, a private repository is a repository that a person or a group of people have access to and no anyone can read or write to it.

The repository that your coworkers work on is an example of this kind. We have multiple branching strategies to manage a private repository. Notice that there is only one code base here and all developers have access to the same repository. There are no forks.

### 1.1. Trunk-based Flow (Single-branch)
In almost all strategies, we have at least one branch called `main` or `master`. This flow is the easiest in understanding but it may cause some issues in your development process. In this strategy, everyone pushes to the `main` branch and you have no more branches and your production branch is `main` as well.

![trunkbased.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661790354548/1wqaS-ytG.png align="center")

#### 1.1.1. Feature-toggle implementation to control your software's features complement
Since you have only one branch, you may have so many unfinished features on `main`. Consider you have a critical push to the production. You need to implement a structure to not only handle those unfinished features to the end-user on production but ignore them in the deployment somehow.

#### 1.1.2. High code coverage & strong tests
Since pushing right straight to the `main` (production) branch is always a risky push, you have to be so confident while using the single-branch flow as your main flow. Therefore, you need so many strong tests to check all changes and modifications and catch bugs before they find their way to production.

### 1.2. Git Flow
You might have heard about this flow before. In this flow, things are a bit complicated compared to the Trunk-based. You have more branches, merge requests and so many more.

![gitflow.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661789085838/oe_lFdVnF.png align="center")

- `release`: We have a straight line called `release` that represents the last stable release of our project being served on deployment.
- `main`: The `main` branch is meant to keep the latest status of stability which is used for merging to the `release` branch as well.
- `develop` or `development`: This branch shows the latest status of the project. It may or may not be stable but it's the branch that all changes have effects on.
- `feature`: These short-living branches are made on top of the `develop` branch and they might be bug fixes, enhancements, improvements, new features, and so on. These branches are merged directly into the `develop` branch.

Now, let me bring an example to see this flow in practice. Let's see what happens for one of the feature branches you've worked on and it's completed now and ready to be merged.

You've worked on `cache-feature` and pushed it to the repository. If your team is working on a Git project management platform such as GitHub, you can open a pull request (PR) from `cache-feature` to `develop` and once your changes undergo tests and reviews, it'll be merged into the `develop` branch.

After a while, the `develop` branch will be merged into the `main` branch for the release time and your changes are also included there as well. Once the `develop` branch is merged into `main`, your team members create a new release and add a new tag to the `main` branch. It's time for the new release to go into production but something bad happens. Once the production is serving the new release, a critical bug could be found and it needs to be fixed ASAP. That's hotfix time!

#### 1.2.1. What is `hotfix`
This branch is placed right between the `release` branch and the `main` one. Once you spotted a bug in a release (probably the production), you simply check out into a `hotfix` branch and fix the bug, and merge the lately created `hotfix` branch into both `main` and `release`. Once your bug-fix commit(s) is created, then you can rebase/merge `main` back into the `development`. There you have all your important branches up to date and the bug is fixed. The main concept behind this branch is to make a quick change and push it into multiple branches.

### 1.3. GitHub Flow
Enough complexity. GitHub flow is so similar to the Git flow but with fewer branches acting here. Many developers prefer calling this strategy the "Feature Branching" strategy as each team can work on different features and that's because the only development is happening within the feature branches. For every change (including hotfixes) we..

- Create a new feature branch
- Develop the source code
- Open a PR

Once it's passed the tests, it'll be merged to the `main` line. Pretty easy, isn't it?

![githubflow.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661789105030/WNadaRtm8.png align="center")

#### 1.3.1. Feature-toggle is already implemented
We can consider the PRs as our feature toggles. In spite we can have tens of unfinished features (opened pull requests), we can have daily releases day and keep the features in control.

### 1.4. GitLab Flow
GitLab recommends users follow their promoted flows called GitLab Flow. There are two different strategies described here. The noticeable part is that with `environment` branches, we don't use our `main` as our production branch anymore. We could use the `main` branch as our pre-production role though. Let's see it in practice.

#### 1.4.1. Environment-based Flow
We got a new branch called `environment` here. This branch represents our source codes in different environments. We can have multiple `environment` branches for our pre-production, staging, testing, or even production. You can create however many `environment` branches per environment that your code base is deployed to. We still have the Feature-branching but it's just part of the game.

![gitlabflow1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661789137667/tLQ6F8a4n.png align="center")

When you're finished working on a feature branch, you open a merge request (GitHub fellows call it "pull requests") and after automation running and validating your changes, your feature branch gets merged into the `main` branch. Notice there is a merge commit with a message (probably like *`added the cache feature (#3)`*). This merge commit jumps the `main` branch one commit ahead and that's why we should fast-forward our pushes to the `environment` branches.

Once your feature branch is merged into `main`, your team does a quick fast-forward merge into the first environment layer which is the staging branch in our case. By doing that, the exact commit you've created throughout your feature branch will be added to the end of the `environment` branch. After testing your changes on the staging environment, it's time to push the changes into the real production environment which is the uppermost branch in the diagram. That merge flow should be a fast-forward merge as well but there is another theory behind that as well.

By doing a fast-forward merge, your commits will be uniquely the same on other branches. Since we tag the commit on the production branch in this strategy, it'll be tagged in all other `environment` branches as well.

#### 1.4.2. Release-based Flow
The other aspect of GitLab flow is related to the releases. You still have your Feature-branching aspect but we have `release` branches other than the environments. The cool part is that by following this flow, your software can support multiple releases at the same time. We're about to dive through the Release-branching strategy in the next section so no worries about its flows.

![gitlabflow2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661789190906/EG5dcp8Mb.png align="center")

As usual, you've opened a new merge request from your `feature` branch into the `main` one. A few whiles after your merged PR, your team goes for a new release. They create a new `release` branch called `v2-stable`. Now, you have two different `release` branches that are being supported by your team. As always, a new bug comes out of nowhere to mess up your new-release-reveal party. You create a `hotfix` feature branch. You do the fixes and merge back the `hotfix` into the `main`. Now, it's time to vanish the bug from the `release-v2-stable`. How would you do that?

Since you have different `release` branches branched from `main`, you can't pull directly from the `main` branch into the `v2-stable` branch because it'll take some commits that are not related to the `v2-stable` but instead, you can cherry-pick them!

#### 1.4.3. Cherry-picking
Cherry-picking allows you to pick some specific commits from a branch and add it to another branch. Git commits have a similar structure as follows.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662206460191/90Na5tBzc.png align="center")

Which includes all changes that happened during the commit time. By cherry-picking a commit, you're applying all those changes to your branch which is a good solution for fixing specific parts of environments.

### 1.5. Release Flow
Let's see how a flow might become your nightmare. Release flow is a true pain in the neck in my opinion. In this flow, we have different release branches branched from the `main` line. Different teams working on different releases. We also have the `hotfix` branch and here is where things get a messy turn but let's talk about the pros first.

The biggest advantage of this flow is that the product can still support multiple releases at the same time since its developers are working on different releases. In another word, I can still use the same application you're using on your brand new smartphone on my 90s phone and that's the magic of this flow.

The big problem is with the `hotfix` branch. Consider the same mobile application. A developer finds a critical bug. He does a quick `hotfix` and merges the `hotfix` into the `main` branch. All `release` branches need to retrieve the same hotfix, therefore they pull the same commits and there might be a huge mess with pulling the same structure into the different old and new releases.

## 2. Public Repositories
Unlike any private ones, everyone has access to public repositories. Consider a public GitHub repository like the one that is your friend's. You only have read access to that. You can check its commit history and some other GitHub-related information like its issues, PRs, contributors, and so more. You can't commit directly to the repository. All you can do (as a normal user) is to ask for a merge request. To make that happen, you need to ask for a merge request from a branch of yours to your friend's, and that leads us to the Fork flow.

## 3. Fork Flow
This flow is the best flow for open-source projects or when we care about privileges, and permissions and we have forks around the corner as well. All that upstream needs is a merge from someone else's branch into its branches. The upstream may use any strategy that it desires. That's what we don't care about. All we need is to branch off a new branch, make some changes, and open new pull/merge requests. We don't need to know whether the upstream is using Git Flow, GitLab flows, or any kind. As we described, we are collaborating within the Feature-branching part.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662212739815/pLyn_ss48.png align="center")

## 4. Branch Naming
In Fork flow, it doesn't matter the name you choose for your newly created branch since you're creating a new branch on a forked repository but if you aim to have your contributions continued, you better do the clean work and keep your forked repo's branches' names clean and understandable. Many maintainers refuse to keep the forked branches listed in their repository branches list so it doesn't matter the name you chose in a Fork flow. They also customize the merge commit messages so their Git history would be clear and understandable but it doesn't mean that you should not care about Branch Naming in other flows or strategies.

### 4.1. Long-living Branch Naming

We have pretty much described the long-living branch names such as `main`, `development`, `environment`, and `release`. These are straight names that show what this branch actually is. Naming for these branches is coming from developers' unwritten rules and some source code management platforms recognize these specific names by default. Of course, you can use the `building` name instead of `develop` or `development` but it'll raise confusion between the contributors and team members.

### 4.2. Short-living Branch Naming

The next subject is permanent branch (short-living branch) naming. These conventions are applied to the branches with permanent living periods. The `feature` branches are this kind. Once they're merged/closed, no one cares about them anymore and they'll be forgotten somehow.

#### 4.2.1. Give your branch an essence
Your feature branches may do different things. They might be either improvements and features or bug fixes and hotfixes. The best convention is to specify your branch essence in the first few characters as follows.

  - `bugfix` - If your branch fixes a bug.
  - `hotfix` - If your branch fixes a critical bug spotted on the production.
  - `feature` - If your branch is about a new feature.
  - `improvement` - If your branch improves an existing functionality or utility.

These keywords describe the branch in one word and that saves a decent amount of a developer's time. Even though the described keywords are widely used in many projects, you may work on a project with different domains of branching names and prefix keywords.

#### 4.2.2. Choose a proper name for your branch
After you choose your prefix, it's time for the actual branch name. You always better separate the essence prefix from the branch name via a slash (/) or a dash (-). It enhances your branch name readability.

Keep your branch name as short as you can. Describing the section you've worked on and replacing the spaces with hyphens or underscores might be the best choice. Check the following examples.

Good naming:
- `bugfix/paypal_webhook_callback`
- `feature/dark-mode`
- `hotfix-visual_banner_lag`

Bad naming:
- `bugfix-paypal-webhook-callback`
- `featuredarkmode`
- `hotfix visual banner lag`

Unfortunately, branch naming is conventional. There is no specification for your project to use a specific naming convention but the one we described here is safe, and popular and helps your team develop the code base with less pain. It's all about readability and consistency. Of course, `feature/paypal_webhook_callback` is way more readable than `featuredarkmode`.

## 5. Which Flow to Choose
It depends on your case but let me give you my opinion.

- **Trunk-based Flow**: Use this flow if you're the only person who contributes to the project or you have awesome tests validating your changes and making sure they don't break anything critical.
- **Git Flow**: If you have so many automation tasks. You care about safety and you want to check the changes multiple times in different phases.
- **GitHub Flow**: If your project is either open-source on GitHub or you're good with less complexity but make sure that accurate tests would help your feature branches be safe. By using this flow, you can have side work and automation as well.
- **GitLab Flows**: If you're maintaining a project on GitLab. You can have automation tasks here as well.
- **Release Flow**: If you want more stability and good support for multiple releases then use this flow. Be careful that this flow may make your project hard to maintain after a while.
- **Fork Flow**: Since the privileges are important, it's the best choice for your open-source projects. It's more a flow other than a strategy.

If you need the necessity of automation tasks in your repository, you better choose your flow carefully so there will be good support for your automation in the chosen strategy.

## Conclusion
We have other branching strategies out there but I decided to focus on the popular ones in this blog post. We talked about branch naming, cherry-picking, hotfixing, and all important long-living and short-living branch terms in different flows.