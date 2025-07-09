# GitHub Foundations
## Introduction to Git
### Introduction

Imagine you're a new software developer at a firm that writes avionics software for commercial airliners. Quality control is critical, and developers work in small teams using Git for version control. You've heard of version control, but you've never used Git, so you're eager to catch up!

You decide to build a website that lets you and your friends share pictures of your cats, so you can learn Git in a fun environment before bringing that knowledge to work. You set out to build the site by using Git to keep track of changes and keep all the source code files backed up in case the server goes down. But before diving head-first into Git, you must cover the basics
### What is version control?

A version control system (VCS) is a program or set of programs that tracks changes to a collection of files. One goal of a VCS is to easily recall earlier versions of individual files or of the entire project. Another goal is to allow several team members to work on a project, even on the same files, at the same time without affecting each other's work.

Another name for a VCS is a software configuration management (SCM) system. The two terms often are used interchangeably—in fact, Git's official documentation is located at [git-scm.com](https://git-scm.com/). Technically, version control is just one of the practices involved in SCM. A VCS can be used for projects other than software, including books and online tutorials.

With a VCS, you can:

- See all the changes made to your project, when the changes were made, and who made them.
- Include a message with each change to explain the reasoning behind it.
- Retrieve past versions of the entire project or of individual files.
- Create _branches_, where changes can be made experimentally. This feature allows several different sets of changes (for example, features or bug fixes) to be worked on at the same time, possibly by different people, without affecting the main branch. Later, you can merge the changes you want to keep back into the main branch.
- Attach a tag to a version—for example, to mark a new release.

Git is a fast, versatile, highly scalable, free, open-source VCS. Its primary author is Linus Torvalds, the creator of Linux.

#### Distributed version control

Earlier instances of VCSes, including CVS, Subversion (SVN), and Perforce, used a centralized server to store a project's history. This centralization meant that the one server was also potentially a single point of failure.

Git is _distributed_, which means that a project's complete history is stored both on the client _and_ on the server. You can edit files without a network connection, check them in locally, and sync with the server when a connection becomes available. If a server goes down, you still have a local copy of the project. Technically, you don't even have to have a server. Changes could be passed around in e-mail or shared by using removable media, but no one uses Git this way in practice.

#### Git terminology

To understand Git, you have to understand the terminology. Here's a short list of terms that Git users frequently use. Don't be concerned about the details for now; all these terms will become familiar as you work your way through the exercises in this module.

- **Working tree**: The set of nested directories and files that contain the project that's being worked on.
    
- **Repository (repo)**: The directory, located at the top level of a working tree, where Git keeps all the history and metadata for a project. Repositories are almost always referred to as _repos_. A _bare repository_ is one that isn't part of a working tree; it's used for sharing or backup. A bare repo is usually a directory with a name that ends in _.git_—for example, _project.git_.
    
- **Hash**: A number produced by a hash function that represents the contents of a file or another object as a fixed number of digits. Git uses hashes that are 160 bits long. One advantage to using hashes is that Git can tell whether a file has changed by hashing its contents and comparing the result to the previous hash. If the file time-and-date stamp is changed, but the file hash isn’t changed, Git knows the file contents aren’t changed.
    
- **Object**: A Git repo contains four types of _objects,_ each uniquely identified by an SHA-1 hash. A _blob_ object contains an ordinary file. A _tree_ object represents a directory; it contains names, hashes, and permissions. A _commit_ object represents a specific version of the working tree. A _tag_ is a name attached to a commit.
    
- **Commit**: When used as a verb, _commit_ means to make a commit object. This action takes its name from commits to a database. It means you are committing the changes you have made so that others can eventually see them, too.
    
- **Branch**: A branch is a named series of linked commits. The most recent commit on a branch is called the _head_. The default branch, which is created when you initialize a repository, is called `main`, often named `master` in Git. The head of the current branch is named `HEAD`. Branches are an incredibly useful feature of Git because they allow developers to work independently (or together) in branches and later merge their changes into the default branch.
    
- **Remote**: A remote is a named reference to another Git repository. When you create a repo, Git creates a remote named `origin` that is the default remote for push and pull operations.
    
- **Commands**, **subcommands**, and **options**: Git operations are performed by using commands like `git push` and `git pull`. `git` is the command, and `push` or `pull` is the subcommand. The subcommand specifies the operation you want Git to perform. Commands frequently are accompanied by options, which use hyphens (-) or double hyphens (--). For example, `git reset --hard`.
    

These terms and others, like `push` and `pull`, will make more sense shortly. But you have to start somewhere, and you might find it helpful to come back and review this glossary of terms after you finish the module.

#### The Git command line

Several different GUIs are available for Git, including GitHub Desktop. Many programming editors, like Microsoft [Visual Studio Code](https://code.visualstudio.com/), also have an interface to Git. They all work differently and they have different limitations. None of them implement _all_ of Git's functionality.

The exercises in this module use the Git command line—specifically, Git commands executed in Azure Cloud Shell. However, Git's command-line interface works the same, no matter what operating system you're using. Plus, the command line lets you tap into _all_ of Git's functionality. Developers who see Git only through a GUI sometimes find themselves confronted with error messages they can't resolve, and they have to resort to the command line to get going again.

#### Git and GitHub

As you work with Git, you might wonder about differences between the features it offers and the features offered on [GitHub](https://github.com/).

As mentioned earlier, Git is a distributed version control system (DVCS) that multiple developers and other contributors can use to work on a project. It provides a way to work with one or more local branches and then push them to a remote repository.

GitHub is a cloud platform that uses Git as its core technology. GitHub simplifies the process of collaborating on projects and provides a website, more command-line tools, and overall flow that developers and users can use to work together. GitHub acts as the remote repository mentioned earlier.

Key features provided by GitHub include:

- Issues
- Discussions
- Pull requests
- Notifications
- Labels
- Actions
- Forks
- Projects

### Basic Git commands

Git works by remembering the changes to your files as if it's taking snapshots of your file system.

We'll cover a few basic commands to start tracking files in your repo. Then, you'll save your first "snapshot" for Git to compare against.

#### git status

The first and most commonly used Git command is `git status`. You've already used it once, in the preceding exercise, to see that you had initialized your Git repo properly.

`git status` displays the state of the working tree (and of the staging area—we'll talk more about the staging area soon). It lets you see which changes are currently being tracked by Git, so you can decide whether you want to ask Git to take another snapshot.

#### git add

`git add` is the command you use to tell Git to start keeping track of changes in certain files.

The technical term is _staging_ these changes. You'll use `git add` to stage changes to prepare for a commit. All changes in files that have been added but not yet committed are stored in the _staging area_.

#### git commit

After you've staged some changes for commit, you can save your work to a snapshot by invoking the `git commit` command.

_Commit_ is both a verb and a noun. It has essentially the same meaning as when you commit to a plan or commit a change to a database. As a verb, committing changes means you put a copy (of the file, directory, or other "stuff") in the repository as a new version. As a noun, a commit is the small chunk of data that gives the changes you committed a unique identity. The data that's saved in a commit includes the author's name and e-mail address, the date, comments about what you did (and why), an optional digital signature, and the unique identifier of the preceding commit.

#### git log

The `git log` command allows you to see information about previous commits. Each commit has a message attached to it (a commit message), and the `git log` command prints information about the most recent commits, like their time stamp, the author, and a commit message. This command helps you keep track of what you've been doing and what changes have been saved.

#### git help

You've already tried out the `git help` command, but it's worth reminding you about. Use this command to easily get information about all the commands you've learned so far, and more.

Remember, each command comes with its _own_ help page, too. You can find these help pages by typing `git <command> --help`. For example, `git commit --help` brings up a page that tells you more about the `git commit` command and how to use it.

## Introduction to GitHub
### Introduction

GitHub provides an AI-powered developer platform to build, scale, and deliver secure software. Whether you’re planning new features, fixing bugs, or collaborating on changes, GitHub is where over 100 million developers from across the globe come together to create things and make them even better.
### What is GitHub?

#### GitHub

![A conceptual image of the GitHub Platform with layers from top to bottom: AI, Collaboration, Productivity, Security, and Scale.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/github-enterprise-platform.png)

**GitHub** is a cloud-based platform that uses Git, a distributed version control system, at its core. The GitHub platform simplifies the process of collaborating on projects and provides a website, command-line tools, and overall flow that allows developers and users to work together.

As we learned earlier, GitHub provides an AI powered developer platform to build, scale, and deliver secure software. Let’s break down each one of the core pillars of the GitHub Enterprise platform, AI, Collaboration, Productivity, Security, and Scale.

##### AI

Generative AI is dramatically transforming software development as we speak. The GitHub Enterprise platform is enhancing collaboration through AI-powered pull requests and issues, productivity through Copilot, and security by automating security checks faster.

##### Collaboration

Collaboration is at the core of everything GitHub does. We know inefficient collaboration results in wasted time and money. We counteract that with a suite of seamless tools that allow collaboration to happen effortlessly.

Repositories, Issues, Pull Requests, and other tools help to enable developers, project managers, operation leaders, and others at the same company. It enables them to work faster together, cut down approval times, and ship more quickly.

##### Productivity

Productivity is accelerated with automation that the GitHub Enterprise Platform provides. With built-in CI/CD (Continuous Integration and Continuous Delivery) tools directly integrated into the workflow, the platform gives users the ability to set tasks and forget them, taking care of routine administration and speeding up day-to-day work. This gives your developers more time to focus on what matters most, creating innovative solutions.

##### Security

GitHub focuses on integrating security directly into the development process from the start. GitHub Enterprise platform includes native, first-party security features that minimize security risk with a built-in security solution. Plus, your code remains private within your organization. At the same time, you're able to take advantage of security overview and Dependabot.

GitHub has continued to make investments to ensure that our features are enterprise-ready. Microsoft and highly regulated industries trust GitHub, and we meet global compliance requirements.

##### Scale

GitHub is the largest developer community of its kind with real-time data on over 100M+ developers, 330M+ repositories, and countless deployments. We’ve been able to understand the shifting needs of developers and make changes to our product to match.

This has translated into an incredible scale that is unmatched and unparalleled by any other company on the planet. Everyday we're gaining more insights from this impressive community and evolving the platform to meet their needs.

In essence, the GitHub Enterprise Platform focuses on the developer experience. It has the scale to provide industry-changing insights, collaboration capabilities for transformative efficiency, the tools for increased productivity, security at every step, and AI to power it all to new heights in a single, integrated platform.

#### Introduction to repositories

##### What is a repository?

A repository contains all of your project's files and each file's revision history. It's one of the essential parts that helps you collaborate with people. You can use repositories to manage your work, track changes, store revision history, and work with others. Before we dive too deep, let’s first start with how to create a repository.

##### How to create a repository

You can create a new repository on your personal account or any organization where you have sufficient permissions.

Let’s tackle creating a repository from github.com.

1. In the upper-right corner of any page, use the drop-down menu, and select **New repository**.
    
    ![A screenshot of the drop-down menu of the plus sign in the top right corner of GitHub.com, with the first option being New repository.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-new-repo-option.png)
    
2. Use the **Owner** drop-down menu to select the account you want to own the repository.
    
    ![A screenshot of the drop-down menu of who should be the owner of the new repository.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-selecting-repo-owner.png)
    
3. Type a name for your repository, and an optional description.
    
    ![An image of the text box of the repository name highlighted.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-repo-name-text-box.png)
    
4. Choose a repository visibility.
    
    - **Public repositories** are accessible to everyone on the internet.
        
    - **Private repositories** are only accessible to you, people you explicitly share access with, and, for organization repositories, certain organization members.
        
5. Select **Create repository** and congratulations! You just created a repository!
    

##### How to add a file to your repository

Files in GitHub can do a handful of things, but the main purpose of files is to store data and information about your project. It's worth knowing in order to add a file to a repository that you must first have minimum **Write** access within the repository you want to add a file.

Let’s review how to add a file to your repository.

1. On GitHub.com, navigate to the main page of the repository.
    
2. In your repository, browse to the folder where you want to create a file by selecting the **creating a new file** link or **uploading an existing file**.
    
3. Once added, above the list of files select the **Add file ᐁ** drop-down menu. Then select **Create new file**.
    
    ![A screenshot of the option to add a file to your new repository highlighted in red with the add file button towards the right of the screen.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/add-file-options.png)
    
4. In the file name field, type the name and extension for the file. To create subdirectories, type the **/** directory separator.
    
5. In the file contents text box, type **content** for the file.
    
6. To review the new content, above the file contents, select **Preview**.
    
    ![Screenshot showing a yml file with the preview button highlighted in the top left.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-preview-option-in-a-file.png)
    
7. Select **Commit changes**.
    
8. In the **Commit message** field, type a short and meaningful commit message that describes the change you made to the file. You can attribute the commit to more than one author in the commit message.
    
9. If you have more than one email address associated with your account on GitHub.com, select the email address drop-down menu. Then select the email address to use as the Git author email address. Only verified email addresses appear in this drop-down menu. If you enabled email address privacy, then _[username]@users.noreply.github.com_ is the default commit author email address.
    
    ![Screenshot showing a commit change with a description box and the drop-down menu of the email to select as the author of the commit.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-commit-description-box.png)
    
10. Below the **Commit message** fields, decide whether to add your commit to the current branch or to a new branch. If your current branch is the default branch, you should choose to create a new branch for your commit, and then create a pull request.
    
    ![Screenshot showing creating a new branch from a commit option select with the textbox of the new branch below it.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-create-a-new-branch.png)
    
11. Select **Commit changes** or **Propose changes**.
    

Congratulations, you just created a new file in your repository! You have also created a new branch and made a commit.

##### What are gists

Now that we have a good understanding of repositories, we can review gists. Similarly to repositories, gists are a simplified way to share code snippets with others.

Every gist is a Git repository, which you can fork and clone and be made either public or secret. Public gists are displayed publicly where people can browse new ones as they’re created. Public gists are also searchable. Conversely, secret gists aren't searchable, but they aren’t entirely private. If you send the URL of a secret gist to a friend, they'll be able to see it.

##### What are wikis?

Every repository on GitHub.com comes equipped with a section for hosting documentation, called a wiki. You can use your repository's wiki to share long-form content about your project, such as how to use it, how you designed it, or its core principles. While a README file quickly tells what your project can do, you can use a wiki to provide additional documentation.

It’s worth a reminder that if your repository is private, only people who have at least read access to your repository will have access to your wiki.

### Components of the GitHub flow

#### What are branches

Branches are an essential part to the GitHub experience because they're where we can make changes without affecting the entire project we're working on.

Your branch is a safe place to experiment with new features or fixes. If you make a mistake, you can revert your changes or push more changes to fix the mistake. Your changes won't update on the default branch until you merge your branch.

>**Note**: Alternatively, you can create a new branch and check it out by using git in a terminal. The command would be `git checkout -b newBranchName`

#### What are commits

A **commit** is a change to one or more files on a branch. Every time a commit is created, it's assigned a unique ID and tracked along with the time and contributor. Commits provide a clear audit trail for anyone reviewing the history of a file or linked item, such as an issue or pull request.

![A screenshot of a list of GitHub commits to a main branch.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-commits.png)

Within a git repository, a file can exist in several valid states as it goes through the version control process. The primary states for a file in a Git repository are **Untracked** and **Tracked**.

**Untracked:** An initial state of a file when it isn't yet part of the Git repository. Git is unaware of its existence.

**Tracked:** A tracked file is one that Git is actively monitoring. It can be in one of the following substates:

- **Unmodified:** The file is tracked, but it hasn't been modified since the last commit.
- **Modified:** The file has been changed since the last commit, but these changes aren't yet staged for the next commit.
- **Staged:** The file has been modified, and the changes have been added to the staging area (also known as the index). These changes are ready to be committed.
- **Committed:** The file is in the repository's database. It represents the latest committed version of the file.

These states and substates are important to collaborating with your team to know where each and every commit is in the process of your project. Now let’s move on to pull requests.

#### What are pull requests?

A **pull request** is the mechanism used to signal that the commits from one branch are ready to be merged into another branch.

The team member submitting the **pull request** asks one or more reviewers to verify the code and approve the merge. These reviewers have the opportunity to comment on changes, add their own, or use the pull request itself for further discussion.

Once the changes have been approved (if required), the pull request's source branch (the compare branch) is merged into the base branch.

![A screenshot of a pull request and a comment within the pull request.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-pull-request.png)

#### The GitHub flow

![Screenshot showing a visual representation of the GitHub Flow in a linear format that includes a new branch, commits, pull request, and merging the changes back to main in that order.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/2-branching.png)

The GitHub flow can be defined as a lightweight workflow that allows for safe experimentation. You can test new ideas and collaboration with your team by using branching, pull requests, and merging.

Now that we know the basics of GitHub we can walk through the GitHub flow and its components.

1. Start by creating a branch so that the changes, features, and fixes you create don't affect the main branch.
2. Next, make your changes. We recommend deploying changes to your feature branch before merging into the main branch. Doing so ensures the changes are valid in a production environment.
3. Now, create a pull request to ask collaborators for feedback. Pull request review is so valuable that some repositories require an approving review before pull requests can be merged.
4. Then review and implement your feedback from your collaborators.
5. Once you feel great about your changes, it's time to get your pull request approved and merge it into the main branch.
6. Finally, you can delete your branch. Deleting your branch signals your work on the branch is complete and prevents you or others from accidentally using old branches.


### GitHub is a collaborative platform

Collaboration is at the core of everything GitHub does. We went over repositories in the first unit of the module and learned that repositories help you organize your project and its files. In the last unit, we learned about pull requests, which is a way to keep track of changes made to your project.
#### Issues

GitHub Issues were created to track ideas, feedback, tasks, or bugs for work on GitHub. Issues can be created in various ways, so you can choose the most convenient method for your workflow.

##### Creating an issue from a repository

1. On GitHub.com, navigate to the main page of the repository.
    
2. Under your repository name, select **Issues**.
    
    ![Screenshot showing the top portion of the main page of a repository with the Issues section highlighted.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/issues-tab.png)
    
3. Select **New issue**.
    
4. If your repository uses issue templates, next to the type of issue you'd like to open select **Get started**.
    
    If the type of issue you'd like to open isn't included in the available options, select **Open a blank issue**. If not using templates, skip to Step 5.
    
    ![A screenshot of the issue templates menu, with the Open a blank issue option highlighted.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/open-a-blank-issue.png)
    
5. In the **Add a title** field, enter a title for your issue.
    
6. In the **Add a description** field, type a description of your issue.
    
7. If you're a project maintainer, you can assign the issue to someone, add it to a project board, associate it with a milestone, or apply a label.
    
8. When you're finished, select **Submit new issue**.
    

Some conversations are more suitable for GitHub Discussions. You can use GitHub Discussions to ask and answer questions, share information, make announcements, and conduct or participate in conversations about a project.

#### Discussions

Discussions are for conversations that need to be accessible to everyone and aren't related to code. Discussions enable fluid, open conversation in a public forum.

##### Enabling a discussion in your repository

Repository owners and people with Write access can enable GitHub Discussions for a community on their public and private repositories. The visibility of a discussion is inherited from the repository the discussion is created in.

When you first enable GitHub Discussions, you're invited to configure a welcome post.

1. On GitHub.com, navigate to the main page of the repository.
    
2. Under your repository name, select **Settings**.
    
    ![A screenshot of the top portion of the main page of a repository with the Settings section highlighted.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/settings-tab.png)
    
3. Scroll down to the **Features** section and under **Discussions**, select **Setup discussions**.
    
    ![A screenshot of the Discussions box with the green Setup discussion button highlighted.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/set-up-discussion.png)
    
4. Under **Start a new discussion**, edit the template to align with the resources and tone you want to set for your community.
    
5. Select **Start discussion**.
    

You're now ready to create a new discussion.

##### Create a new discussion

Any authenticated user who can view the repository can create a discussion in that repository. Similarly, since organization discussions are based on a source repository, any authenticated user who can view the source repository can create a discussion in that organization.

1. On GitHub.com, navigate to the main page of the repository or organization where you want to start a discussion.
    
2. Under your repository or organization name, select **Discussions**.
    
    ![A screenshot of the top portion of the main page of a repository with the Discussions section highlighted.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/discussions-tab.png)
    
3. On the right side of the page, select **New discussion**.
    
4. Select a discussion category by selecting **Get started**. All discussions must be created in a category. For repository discussions, people with maintain or admin permissions to the repository define the categories for discussions in that repository.
    
    ![A screenshot of the select a discussion category menu selection, with the top option Announcements and the get started button highlighted.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/announcements.png)
    

Each category must have a unique name, emoji pairing, and a detailed description stating its purpose. Categories help maintainers organize how conversations are filed. They're customizable to help distinguish categories that are Q&A or more open-ended conversations. The following table shows the default categories for discussions and their purpose.

|**Category**|**Purpose**|**Format**|
|---|---|---|
|📣 Announcements|Updates and news from project maintainers|Announcement|
|#️⃣ General|Anything and everything relevant to the project|Open-ended discussion|
|💡 Ideas|Ideas to change or improve the project|Open-ended discussion|
|🗳️ Polls|Polls with multiple options for the community to vote for and discuss|Polls|
|🙏 Q&A|Questions for the community to answer, with a question/answer format|Question and Answer|
|🙌 Show and tell|Creations, experiments, or tests relevant to the project|Open-ended discussion|

1. Under **Discussion title** enter a title for your discussion, and under **Write** enter the body of your discussion.
    
    ![A screenshot of starting a new discussion page with the Discussion title box and content box empty.](https://learn.microsoft.com/en-us/training/github/introduction-to-github/media/start-a-new-discussion.png)
    
2. Select **Start discussion**.

### GitHub platform management

#### Managing notifications and subscriptions

You can choose to receive ongoing updates about specific activity on GitHub.com through a subscription. Notifications are the updates that you receive for specific activity to which you're subscribed.

##### Subscription options

You can choose to subscribe to notifications for:

- A conversation in a specific issue, pull request, or gist.
- CI activity, such as the status of workflows in repositories set up with GitHub Actions.
- Repository issues, pull requests, releases, security alerts, or discussions (if enabled).
- All activity in a repository.

In some instances, you're automatically subscribed to conversations on GitHub. Examples include opening a pull request or issue, commenting on a thread, or being assigned to an issue or pull request.

If you're no longer interested in a conversation, you can unsubscribe, unwatch, or customize the types of notifications you'll receive in the future.

If you're ever interested in issues that mention a certain user, you can use _mentions:_ as the qualifier to find those specific issues.

#### What are GitHub Pages?

To round out our journey of GitHub, let’s tackle GitHub pages. You can use GitHub Pages to publicize and host a website about yourself, your organization, or your project directly from a repository on GitHub.com.

GitHub Pages is a static site-hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub. Optionally, you can run the files through a build process and publish a website. Edit and push your changes, and your project is live for the public in a visually organized way.
## Introduction to GitHub's products
### Introduction

Whether you're just learning to code, working as a developer at a start-up, or a C-level executive at a Fortune 500 company, the GitHub platform can help you build, scale, and deliver secure software.

Depending on your specific situation, it's important to know what GitHub plans fit your needs.
### GitHub accounts and plans

#### GitHub account types

It's important to understand that there's a difference between the types of GitHub accounts and the GitHub plans. Here are the three types of GitHub accounts:

- Personal
- Organization
- Enterprise

##### Personal accounts

Every person who uses GitHub.com signs into a personal account (sometimes referred to as a user account). Your personal/user account is your identity on GitHub.com and has a username and profile.

Your personal/user account can own resources such as repositories, packages, and projects and has a straightforward way to manage your permission. Actions that you take on GitHub.com, such as creating an issue or reviewing a pull request, are attributed to your personal account.

Each personal account uses either GitHub Free or GitHub Pro. All personal accounts can own an unlimited number of public and private repositories, with an unlimited number of collaborators on those repositories. If you use GitHub Free, private repositories owned by your personal account have a limited feature set.

##### Organization accounts

Organization accounts are shared accounts where an unlimited number of people can collaborate across many projects at once. Unlike personal/user accounts, permissions with organization accounts are done with a tiered approach.

Similar to personal accounts, organizations can own resources such as repositories, packages, and projects. However, you can't sign into an organization. Instead, each person signs into their own personal account, and any actions the person takes on organization resources are attributed to their personal account. Each personal account can be a member of multiple organizations.

The personal accounts within an organization can be given different roles in the organization to grant different levels of access to the organization and its data. All members can collaborate with each other in repositories and projects. But only organization owners and security managers can manage the settings for the organization and control access to the organization's data with sophisticated security and administrative features.

##### Enterprise accounts

Enterprise accounts on GitHub.com allow administrators to centrally manage policies and billing for multiple organizations and enable inner sourcing between their organizations. An enterprise account must have a handle, like an organization or user account on GitHub.

Organizations are shared accounts for enterprise members to collaborate across many projects at once. In the enterprise settings, enterprise owners can invite existing organizations to join your enterprise account, transfer organizations between enterprise accounts, or create new organizations.

Your enterprise account allows you to manage and enforce policies for all the organizations owned by the enterprise. Each enterprise policy controls the options available for a policy at the organization level.

#### GitHub plans

Now that you have a better understanding of the different types of accounts you can have with GitHub, let's look at the different plans available to improve your software management process and team collaboration.

There are several free GitHub products, in addition to the paid ones:

- GitHub Free for personal accounts and organizations
- GitHub Pro for personal accounts
- GitHub Team
- GitHub Enterprise

##### GitHub Free

GitHub Free provides the basics for individuals and organizations. Anyone can sign up for the free version of GitHub.

###### GitHub Free for personal accounts

Signing up for GitHub Free gives a new user a _personal user account_. A personal user account includes unlimited public and private repositories and unlimited collaborators.

With GitHub Free, a personal account includes:

- GitHub Community Support
- Dependabot alerts
- Two-factor authentication enforcement
- 500-MB GitHub Packages storage
- 120 GitHub Codespaces core hours per month
- 15-GB GitHub Codespaces storage per month
- GitHub Actions:
    - 2,000 minutes per month
    - Deployment protection rules for public repositories

###### GitHub Free for organizations

With GitHub Free for organizations, you can work with unlimited collaborators on unlimited public repositories, with a full feature set. Or, unlimited private repositories with a limited feature set.

In addition to the features available with GitHub Free for personal accounts, GitHub Free for organizations includes:

- Team access controls for managing groups

##### GitHub Pro

GitHub Pro is similar to GitHub Free but comes with upgraded features. The plan is designed for individual developers (using their personal account) who want advanced tools and insight within their repositories but don't belong to a team.

GitHub Pro accounts include all of the features of a GitHub Free account, plus the following advanced features:

- GitHub Support via email
- 3,000 GitHub Actions minutes per month
- 2-GB GitHub Packages storage
- 180 GitHub Codespaces core hours per month
- 20-GB GitHub Codespaces storage per month
- Advanced tools and insights in private repositories:
    - Required pull request reviewers
    - Multiple pull request reviewers
    - Protected branches
    - Code owners
    - Autolinked references
    - GitHub Pages
    - Wikis
    - Repository insight graphs for pulse, contributors, traffic, commits, code frequency, network, and forks

##### GitHub Team

GitHub Team is the version of GitHub Pro for organizations. GitHub Team is better than GitHub Free for organizations because it provides increased GitHub Actions minutes and extra GitHub Packages storage.

Let's go over the extra features in GitHub Team that help with team collaboration:

- GitHub Support via email
- 3,000 GitHub Actions minutes per month
- 2-GB GitHub Packages storage
- Advanced tools and insights in private repositories:
    - Required pull request reviewers
    - Multiple pull request reviewers
    - Draft pull requests
    - Team pull request reviewers
    - Protected branches
    - Code owners
    - Scheduled reminders
    - GitHub Pages
    - Wikis
- Repository insight graphs for pulse, contributors, traffic, commits, code frequency, network, and forks
- The option to enable or disable GitHub Codespaces

##### GitHub Enterprise

GitHub Enterprise accounts enjoy a greater level of support and extra security, compliance, and deployment controls.

You can create one or more _enterprise accounts_ by signing up for the paid GitHub Enterprise product. When you create an enterprise account, you're assigned the role of _enterprise owner_. As an enterprise owner, you can add and remove organizations to and from the enterprise account. You can manage other administrators, enforce security policies across organizations, and so on.

In addition to the features available with GitHub Team, GitHub Enterprise includes:

- GitHub Enterprise Support
- More security, compliance, and deployment controls
- Authentication with security assertion markup language (SAML) single sign-on
- Access provisioning with SAML or System for Cross-domain Identity Management (SCIM)
- Deployment protection rules with GitHub Actions for private or internal repositories GitHub Connect
- The option to purchase GitHub Advanced Security

###### GitHub Enterprise options

There are two different GitHub Enterprise options:

- GitHub Enterprise Server
- GitHub Enterprise Cloud

The significant difference between GitHub Enterprise Server (GHES) and GitHub Enterprise Cloud is that GHES is a self-hosted solution that allows organizations to have full control over their infrastructure.

The other difference between GHES and GitHub Enterprise Cloud is that GitHub Enterprise Cloud includes a dramatic increase in both GitHub Actions minutes and GitHub Packages storage.

Here are the extra features of GitHub Enterprise Cloud:

- 50,000 GitHub Actions minutes per month
- 50-GB GitHub Packages storage
- A service level agreement for 99.9% monthly uptime
- Option to centrally manage policy and billing for multiple GitHub.com organizations with an enterprise account
- Option to provision and manage the user accounts for your developers, by using Enterprise Managed Users

### GitHub Mobile and GitHub Desktop

There are multiple ways to access your GitHub account aside from github.com. GitHub Mobile and GitHub Desktop allow you to have a seamless experience while accessing your account on the go.

#### GitHub Mobile

GitHub Mobile gives you a way to do high-impact work on GitHub quickly and from anywhere. GitHub Mobile is a safe and secure way to access your GitHub data through a trusted, first-party client application.

With GitHub Mobile you can:

- Manage, triage, and clear notifications from github.com.
- Read, review, and collaborate on issues and pull requests.
- Edit files in pull requests.
- Search for, browse, and interact with users, repositories, and organizations.
- Receive a push notification when someone mentions your username.
- Schedule your push notifications for specific custom hours.
- Secure your GitHub.com account with two-factor authentication.
- Verify your sign in attempts on unrecognized devices.

#### GitHub Desktop

GitHub Desktop is an open-source, stand-alone software application that enables you to be more productive. It facilitates collaboration between you and your team and the sharing of Git and GitHub best practices within your team.

Here are a few of the many things you can do with GitHub Desktop:

- Add and clone repositories.
- Add changes to your commit interactively.
- Quickly add coauthors to your commit.
- Check out branches with pull requests and view CI statuses.
- Compare changed images.

### GitHub billing

GitHub bills separately for each account. You receive a separate bill for your personal account and for each organization or enterprise account you own.

The bill for each account is a combination of charges for your subscriptions and usage-based billing.

- **Subscriptions** include your account's plan, such as GitHub Pro or GitHub Team, and paid products that have a consistent monthly cost, such as GitHub Copilot and apps from GitHub Marketplace.
- **Usage-based billing** applies when the cost of a paid product depends on how much you use the product. For example, the cost of GitHub Actions depends on how many minutes your jobs spend running and how much storage your artifacts use.
    
    >**Note**: Your plan might come with included amounts of usage-based products. For example, with GitHub Pro, your personal account gets 3,000 minutes of GitHub Actions usage for free each month. You can control usage beyond the included amounts by setting spending limits.
    

Understanding GitHub's billing structures is crucial for effective administration and cost management. This document focuses on differentiating how GitHub products are billed, including seat licenses, GitHub Actions, GitHub Packages, and the new billing platform's capabilities.

#### Pricing for GitHub Actions

GitHub Actions enables automation of workflows directly within repositories. Its pricing model varies based on repository visibility and account type:

- **Public Repositories**: Usage of GitHub Actions is **free** for public repositories, providing unlimited minutes on GitHub-hosted runners.
    
- **Private Repositories**: Each account receives a certain amount of free minutes and storage for GitHub-hosted runners, depending on the account's plan. For example, GitHub Free for personal accounts includes 2,000 CI/CD minutes per month. Usage beyond the included amounts is controlled by spending limits.
    

It's important to monitor usage to avoid unexpected costs, especially for private repositories with high activity.

#### Pricing and Support Options for Organizations

GitHub offers various plans tailored to organizational needs, each with distinct features and support options:

- **GitHub Free for Organizations**:
    - **Features**:
        - Unlimited public/private repositories
        - Community support
        - 2,000 CI/CD minutes per month
- **GitHub Team**:
    - **Features**:
        - Everything in Free, plus:
        - Additional collaboration tools
        - Code owners
        - Required reviews
        - Enforced branch protections
        - Email support
- **GitHub Enterprise**:
    - **Features**:
        - Everything in Team, plus:
        - SAML single sign-on
        - Advanced auditing
        - GitHub Connect
        - 24/7 support
        - Enterprise-level security features For more information about available features and pricing tiers, see GitHub’s [pricing page](https://github.com/pricing).

Organizations should evaluate their collaboration needs and security priorities to choose the plan that best fits their goals.

#### Usage-Based Billing for Licenses (Metered Billing)

With the enhanced billing platform, GitHub has introduced a usage-based billing model for licenses:

- **Monthly Billing**: Organizations are billed monthly for the exact number of GitHub Enterprise and GitHub Advanced Security licenses used.
    
- **Pro Rata Charges**: If a user starts consuming a license partway through the month, the organization is charged a pro rata amount for that user's usage.
    
- **Dynamic Adjustments**: If a user stops consuming a license during the month, the billing for the following month reflects this change, ensuring organizations only pay for active users.
    

This model eliminates the need to purchase a predefined number of licenses in advance, offering flexibility and cost efficiency.

#### Billing Platform’s New Capabilities

GitHub's enhanced billing platform provides improved tools for financial management:

- **Granular Spending Controls**: Administrators can set specific spending limits for services like GitHub Actions and GitHub Packages, preventing unexpected overages.
    
- **Detailed Usage Insights**: The platform offers in-depth visibility into product usage, allowing organizations to monitor consumption patterns and optimize resource allocation.
    
- **Automated Reporting**: Features for automating usage reporting streamline financial oversight and facilitate internal chargebacks.
    

These capabilities enhance an organization's ability to manage expenses effectively and align GitHub usage with budgetary constraints.


### License Usage Stats

As a **GitHub Enterprise administrator**, tracking **license usage** is crucial for managing costs, optimizing resources, and ensuring compliance. GitHub provides various methods for obtaining license statistics at **organization, enterprise, and instance levels**.

#### Finding License Usage for a Specific Organization

To find **license usage statistics** for a single **GitHub organization**:

##### Method 1: Using GitHub Enterprise Cloud (GHEC) Admin Console

1. Navigate to **GitHub Enterprise Cloud Admin Panel**.
2. Go to **Settings > Billing & plans**.
3. Locate the **License usage** section.
4. View details such as:
    - **Total seats assigned**
    - **Active seats in use**
    - **Available licenses**
    - **Pending invitations**

**Command-Line Alternative (GraphQL API)**

For more granular data, admins can use **GraphQL API**:

```json
{
  organization(login: "org-name") {
    billingInfo {
      totalSeats
      seatsUsed
      seatsAvailable
    }
  }
}
```

##### Method 2. Finding License Usage Across Multiple Organizations

For organizations under the same **enterprise account**, admins can analyze usage across all organizations.

###### Using the Enterprise Account Billing Page

1. Navigate to **GitHub Enterprise Cloud > Enterprise settings**.
2. Go to **Billing** > **License Usage**.
3. Review license usage for **each organization under the enterprise account**.

**GraphQL API Query for All Organizations**

To fetch usage data for all organizations in an enterprise:

```json
{
  enterprise(slug: "enterprise-name") {
    organizations(first: 50) {
      nodes {
        name
        billingInfo {
          totalSeats
          seatsUsed
          seatsAvailable
        }
      }
    }
  }
}

```

##### Method 3. Finding License Usage for Enterprise Accounts

For enterprises using **GitHub Enterprise Cloud or GitHub Enterprise Server**, admins can track licenses at the **enterprise level**.

**GitHub Enterprise Server (GHES) Dashboard**

Next, you'll dive into how to gain access to view track these licenses .

1. Log in to the **GitHub Enterprise Server Admin Console**.
2. Go to **Settings > License Usage**.
3. View:
    - **Total allocated licenses**
    - **Active users**
    - **Available seats**
    - **Historical license usage trends**

_REST API Alternative_

For **programmatic access**, use the REST API:

```bash
curl -H "Authorization: token YOUR-TOKEN" \
"https://api.github.com/enterprises/YOUR-ENTERPRISE/license"
```

##### Method 4. Finding License Usage Across Multiple GitHub Instances

For **large enterprises** with multiple GitHub Enterprise **Server instances**, admins must track **license consumption** across deployments.

**GitHub Enterprise Metrics API**

4. Access **GitHub Enterprise Server** admin settings.
5. Use the **Metrics API**:

```bash
curl -H "Authorization: token YOUR-TOKEN" \
"https://api.github.com/enterprise/settings/licenses"

```

6. Extract:
    - **Total enterprise-wide licenses**
    - **Usage per GitHub instance**
    - **Available capacity per region**

##### Best Practices for License Usage Management

The following strategies can help you manage licenses more efficiently across your organization:

- **Automate Monitoring**: Use **GraphQL/REST API queries** to **track usage trends**.
- **Optimize Unused Seats**: Identify **inactive users** and **reclaim unused licenses**.
- **Enable Usage-Based Billing**: Ensure **billing reflects actual consumption**.
- **Regular Audits**: Conduct **monthly/quarterly** **license reviews** to optimize cost.

### License Usage Stats in Machine and Peripheral Devices

Tracking **license usage** is essential for cost optimization and security compliance. **Machine accounts** (used for automation) and **peripheral services** (such as CI/CD, integrations, and API consumers) can consume licenses, impacting enterprise costs and resource management.

#### Understanding Machine Accounts and Peripheral Services

##### Machine Accounts

Machine accounts are **GitHub accounts** used for automation, running scripts, or integrating with third-party tools.

**Characteristics**: - They act **independently of human users**. - Often used by CI/CD tools (e.g., GitHub Actions, Jenkins, CircleCI). - **Each machine account consumes a GitHub license**, like a standard user.

##### Peripheral Services

Peripheral Services are external integrations that interact with GitHub via **API requests**.

**Examples**: - **CI/CD Pipelines** (e.g., GitHub Actions, GitHub Runners, Jenkins). - **Security Scanning Tools** (e.g., Dependabot, Snyk, CodeQL). - **Third-party Integrations** (e.g., Slack, Jira, Datadog). - **Self-hosted GitHub Runners**.

**Why Track These?**

- To **identify unused or excessive licenses**.
- To **optimize costs** and prevent unnecessary spending.
- To **monitor security risks** from inactive or misconfigured automation accounts.

#### Finding License Usage Statistics for Machine Accounts

##### Method 1: GitHub Enterprise Admin Console

1. **Navigate to Enterprise Settings**.
2. Select **Billing & License Management**.
3. Look for a **Machine Accounts** section (if available).
4. Identify:
    - **Number of active machine accounts**.
    - **License consumption per machine account**.
    - **Last active date**.

##### Method 2: GraphQL API Query for Machine Accounts

To retrieve **machine account usage statistics**, use the **GraphQL API**:

```json
{
  enterprise(slug: "enterprise-name") {
    organizations(first: 50) {
      nodes {
        name
        machineAccounts {
          totalCount
          nodes {
            login
            createdAt
            lastActiveAt
          }
        }
      }
    }
  }
}

```

**Why Track These?**

- To identify **inactive machine accounts**.
- To track **when each machine account was last active**.
- To help **reduce unnecessary license allocation**.

#### Finding License Usage for Peripheral Services

##### Method 1: GitHub Actions & Runners Usage Metrics

1. Go to Enterprise Settings** → **Actions**.
2. View:
    - **Total GitHub-hosted runner minutes used**.
    - **Self-hosted runner usage**.
    - **Billing for extra runner minutes**.

##### Method 2: REST API for Self-Hosted Runners

To track **self-hosted runners** and their license usage:

```bash
curl -H "Authorization: token YOUR-TOKEN" \
"https://api.github.com/enterprises/YOUR-ENTERPRISE/actions/runners"
```

**Key Insights**:

- Identifies **how many runners are consuming licenses**.
- Tracks **idle runners that may be wasting resources**.
- Helps **optimize billing for GitHub-hosted runner minutes**.

##### Method 3: Peripheral Services API Usage Tracking

Monitor API-based integrations using:

```bash
curl -H "Authorization: token YOUR-TOKEN" \
"https://api.github.com/enterprises/YOUR-ENTERPRISE/audit-log"
```

**This helps you:**

- Detect Inactive Services: Find services no longer in use.
- Audit Third-Party Tools: Ensure external tools are necessary and properly configured.
- Reduce Costs: Disable services that are not providing value."

#### Best Practices for Managing Machine Accounts & Peripheral Services Licenses

The following best practices will help you audit usage, enforce policies, and streamline your automation footprint:

- **Audit Machine Accounts Regularly**: Identify and deactivate **unused machine accounts**.
    - Over time, organizations accumulate **unused or stale machine accounts** that may still have access to repositories and systems.
    - Unused accounts **increase security risks**, as they can be exploited if compromised.
    - Regular audits ensure that only **active and necessary** machine accounts exist, reducing exposure to unauthorized access.
- **Monitor API Usage**: Track third-party tools consuming enterprise licenses.
    - Many third-party applications, CI/CD pipelines, and integrations consume GitHub **API resources and enterprise licenses**.
    - Excessive API calls can lead to **rate limits**, affecting developers' workflows.
    - Unauthorized or unknown API usage can expose sensitive data and security vulnerabilities.
- **Optimize Runner Usage**: Identify **idle self-hosted runners** and **reduce GitHub-hosted runner costs**.
    - Self-hosted and GitHub-hosted **runners** execute CI/CD workflows. Inefficient use leads to **unnecessary costs**.
    - Idle self-hosted runners **waste computing resources** and may expose organizations to security risks if left unmonitored.
    - GitHub-hosted runners operate on a **pay-as-you-go** basis, and optimizing usage can **significantly reduce costs**.
- **Restrict Machine Accounts**: Limit their **permissions** and **enforce security policies**.
    - Machine accounts should **not have unnecessary access** to repositories, reducing the risk of privilege escalation.
    - If compromised, machine accounts **can be exploited to manipulate source code, deploy malicious changes, or expose secrets**.
    - Enforcing security policies helps ensure compliance and **minimizes potential breaches**.

Tracking **license usage for machine accounts and peripheral services** is crucial for **cost optimization, security, and compliance** in GitHub Enterprise. Admins should leverage **GitHub UI, GraphQL, and REST APIs** to **identify inactive accounts, optimize usage, and prevent unnecessary spending**.
### Metered Usage Reports

GitHub provides detailed billing and consumption reports to track the usage of **metered products**. These reports help administrators monitor costs, allocate resources efficiently, and ensure compliance with organizational policies.

#### GitHub Actions Minutes

GitHub Actions is a CI/CD automation tool where workflows run on virtual machines. The minutes consumed in these workflows are metered based on repository type, runner type, and usage.

##### Tracking Consumption

- Navigate to **Settings → Billing** in your GitHub organization or account.
- Under the **GitHub Actions** section, you can see the number of minutes used.
- Usage is broken down by repository, runner type (Linux, macOS, Windows), and remaining quota.

##### Billing Details

- **Free Allocation:**
    - Public repositories get **unlimited** free minutes.
    - Private repositories receive free minutes based on the plan:
        - **GitHub Free:** 2,000 minutes/month
        - **GitHub Pro:** 3,000 minutes/month
        - **GitHub Team:** 3,000 minutes/month
        - **GitHub Enterprise:** 50,000 minutes/month
- **Pricing per Runner Type (as of 2024):**
    - **Linux:** $0.008 per minute
    - **Windows:** $0.016 per minute
    - **macOS:** $0.08 per minute

##### Optimization Strategies

- Use **self-hosted runners** for high-volume workflows to reduce costs.
- Optimize workflow scripts by caching dependencies and reducing redundant jobs.
- Limit workflows to **only trigger when necessary** (e.g., push to `main` branch only).

#### Storage for GitHub Packages

GitHub Packages allows storing artifacts, container images, and dependencies. Storage is metered based on the volume of stored data and data transfer usage.

##### Tracking Consumption

- Navigate to **Settings → Billing → GitHub Packages** to view storage usage.
- Breakdown includes **storage (GB) and data transfer (GB)** used per repository.

##### Billing Details

- **Free Allocation:**
    - **Public repositories:** Free storage and bandwidth.
    - **Private repositories:**
        - Storage up to 2GB
        - Data transfer up to 1GB per month

For details on storage limits and usage beyond the free allocation, see [GitHub’s pricing page](https://github.com/pricing).

##### Optimization Strategies

- Regularly **delete unused packages** or enable retention policies.
- Store frequently accessed images in a **centralized registry** to reduce duplication.
- Use **compressed formats** to reduce storage consumption.

#### GitHub Enterprise (GHE) Licenses

GitHub Enterprise provides advanced features for organizations, and the number of **active users** determines license consumption.

##### Tracking Consumption

- Go to **Enterprise Settings → Billing** to view **license usage reports**.
- Monitor active users vs. allocated licenses.

##### Billing Details

- **Pricing Model:**
    - Each user with access to private repositories consumes **one license**.
    - Organizations pay per user annually or monthly.
- **Inactive Users:**
    - If an admin **removes** a user, the license remains **assigned** for the billing period but can be reallocated.

##### Optimization Strategies

- Audit **inactive users** and revoke access to free up licenses.
- Use **SSO and SCIM provisioning** to automate user management.

#### GitHub Advanced Security (GHAS) Licenses

GitHub Advanced Security (GHAS) offers **code scanning, secret scanning, and dependency review** for enhanced security.

##### Tracking Consumption

- View reports in **Settings → Billing → GHAS Usage** to see active committers.
- The report shows **unique committers per billing period**.

##### Billing Details

- **Pricing Model:**
    - Charged per **unique committer** per month.
    - If a committer contributes to multiple repositories, they **only count once**.
- **Free Tier:** Not available (only for public repositories).

##### Optimization Strategies

- **Restrict GHAS** to repositories that **truly need advanced security**.
- Use **branch protections** to limit unnecessary scans on feature branches.

#### GitHub Copilot

GitHub Copilot provides **AI-driven code completion** and suggestions, billed per user.

##### Tracking Consumption

- Admins can track **Copilot usage** under **Billing → Copilot** in organization settings.
- The report shows **active users** and monthly billing estimates.

##### Billing Details

- **Access Model:**
    - Available for individuals and businesses with different subscription options.
- **Free Access:**
    - Free for students and verified open-source maintainers.
    - Free for **select enterprise customers** (trial-based).

For current Copilot plans and subscription details, see [GitHub Copilot pricing](https://github.com/features/copilot#pricing).

##### Optimization Strategies

- Regularly **review and deactivate Copilot** for users who don’t need it.
- Encourage developers to **disable Copilot** in projects where AI-generated code is unnecessary.

#### Large File Storage (LFS)

GitHub LFS is used for storing large binary files separately from Git repositories.

##### Tracking Consumption

- View LFS usage in **Billing → LFS Usage**.
- Report includes **storage (GB) and bandwidth usage (GB)**.

##### Billing Details

- **Free Tier:**
    - 1GB of storage per repository
    - 1GB of bandwidth per month

For more information on Git Large File Storage (LFS) usage and limits, see [GitHub's LFS documentation](https://docs.github.com/en/github/managing-large-files/about-git-large-file-storage#about-storage-and-bandwidth-usage).

##### Optimization Strategies

- **Use external storage services** (e.g., AWS S3, Azure Blob Storage) for large files.
- **Delete unused large files** to optimize storage.
- **Enable Git LFS file pruning** to remove unreferenced objects.



## Configure code scanning on GitHub
### Introduction

Imagine that you're the GitHub administrator for a project, and you want to make sure that the code doesn't include any security vulnerabilities or errors. It can be very time consuming to manually check your code base, especially if it's large. Your company just purchased a GitHub Advanced Security license that helps save time and effort by allowing you to use code scanning. With code scanning, you receive alerts indicating any problematic code. Then, you can quickly find the problem areas and make the necessary changes. In order to enable code scanning, you need to know what tools are available and what their features are. You also need to understand how often to perform code scanning and the types of events you can use to trigger scans.
### What is code scanning?

Code scanning uses CodeQL to analyze the code in a GitHub repository to find security vulnerabilities and coding errors. Code scanning is available for all public repositories, and for private repositories owned by organizations where GitHub Advanced Security is enabled. If code scanning finds a potential vulnerability or error in your code, GitHub displays an alert in the repository's Security tab. After you fix the code that triggered the alert, GitHub closes the alert.

You can use code scanning to find, triage, and prioritize fixes for existing problems in your code. Code scanning also prevents developers from introducing new problems. You can schedule scans for certain days and times, or trigger scans when a specific event occurs in the repository, such as a push.

#### About code scanning with CodeQL

CodeQL is the code analysis engine GitHub developed to automate security checks. You can analyze your code using CodeQL and display the results as code scanning alerts. There are three main ways to set up CodeQL analysis for code scanning:

- Use default setup to quickly configure CodeQL analysis for code scanning on your repository. The default setup handles choosing the languages to analyze, query suite to run, and events that trigger scans with the option to manually configure the languages and query suites. This setup option runs code scanning as a GitHub Action.
- Use advanced setup to add the CodeQL workflow directly to your repository. Adding the CodeQL workflow directly into your repository generates a customizable workflow file, which uses the [github/codeql-action](https://github.com/github/codeql-action/) to run the CodeQL CLI as a GitHub Action.
- Run the CodeQL CLI directly in an external CI system and upload the results to GitHub.

CodeQL treats code like data, allowing you to find potential vulnerabilities in your code with greater confidence than traditional static analyzers. You generate a CodeQL database to represent your codebase, then run CodeQL queries on that database to identify problems in the codebase. The query results are shown as code scanning alerts in GitHub when you use CodeQL with code scanning.

CodeQL supports both compiled and interpreted languages, and it can find vulnerabilities and errors in code written in the following supported languages:

- C or C++
- C#
- Go
- Java/Kotlin
- JavaScript/TypeScript
- Python
- Ruby
- Swift

#### Enable CodeQL in your repository with the Default Setup

If you have write permissions to a repository, you can set up or configure code scanning for that repository.

Follow these steps to set up code scanning using the CodeQL GitHub Actions workflow:

1. On GitHub.com, navigate to the repository's main page.
    
2. Under your repository name, select **Security**.
    
    ![Screenshot of the security tab.](https://learn.microsoft.com/en-gb/training/github/configure-code-scanning/media/2-security-tab-screenshot.png)
    
3. Select **Set up code scanning**. If this option isn't available, ask an organization owner or repository administrator to enable GitHub Advanced Security.
    
    ![Screenshot of the set up code scanning button.](https://learn.microsoft.com/en-gb/training/github/configure-code-scanning/media/3-set-up-code-scanning-button-screenshot.png)
    
4. In the **Set up** drop-down, select **Default**.
    
5. Review the default options. If needed, select the **Edit** button in the bottom left corner of the new window to customize how CodeQL runs.
    
    The `on:pull_request` and `on:push` triggers are the default for code scanning are each useful for different purposes. You'll learn more about these triggers in the _Configure Code Scanning_ unit.
    
6. Select **Enable CodeQL** once you're ready to turn on code scanning.
    
    In the default CodeQL analysis workflow, code scanning is configured to analyze your code each time you either push a change to any protected branches or raise a pull request against the default branch. Once the push is made, code scanning runs automatically.
    

In the previous section, we enabled code scanning using the default setup, which runs code scans as a GitHub Action without needing to maintain a workflow file. The other option is **Advanced** setup, which generates the default workflow file you can edit for advanced configuration and more steps. We'll cover using the advanced setup for configuring code scanning in a later unit.

Running code scanning with GitHub Actions affects your monthly billing minutes. If you want to use GitHub Actions beyond the storage or minutes included in your account, you'll be billed for more usage.

#### About Billing for Actions

Code scanning uses GitHub Actions, and each run of a code-scanning workflow consumes minutes for GitHub Actions. GitHub Actions usage is free for both public repositories and self-hosted runners. For private repositories, each GitHub account receives a certain number of free minutes and storage, depending on the product used with the account. Spending limits control any usage beyond the included amounts. If you're a monthly billed customer, your account has a default spending limit of zero US dollars (USD), which prevents extra usage of minutes or storage for private repositories beyond the amounts included with your account. If you pay your account by invoice, your account will have an unlimited default spending limit. Minutes reset every month, while storage usage doesn't.
### Enable code scanning with third party tools

Instead of running code scanning in GitHub, you can perform analysis elsewhere and then upload the results. Alerts for code scanning that you run externally are displayed in the same way as those you run within GitHub. You can upload Static Analysis Results Interchange Format (SARIF) files generated outside GitHub or with GitHub Actions to see code scanning alerts from third-party tools in your repository.

##### About SARIF file uploads for code scanning

GitHub creates code-scanning alerts in a repository using information from SARIF files. You can generate SARIF files using many static analysis-security testing tools, including CodeQL. The results must use SARIF version 2.1.0.

You can upload the results using the code-scanning API, the CodeQL CLI, or GitHub Actions. The best upload method will depend on how you generated the SARIF file.

###### Code-scanning API

The code-scanning API lets you retrieve information on code scanning alerts, analyses, databases, and default setup configuration from a repository. Additionally, you can update code-scanning alerts and the default setup configuration. You can use the endpoints to create automated reports for the code-scanning alerts in an organization or upload analysis results generated using offline code-scanning tools.

You can access the GitHub API over HTTPS from `https://api.github.com`. All data is sent and received as JSON. The API uses custom media types to let consumers choose the format of the data they wish to receive. Media types are specific to resources, allowing them to change independently and support formats that other resources don't.

There's one supported custom media type for the code scanning REST API, `application/sarif+json`.

You can use this media type with GET requests sent to the `/analyses/{analysis_id}` endpoint. When you use this media type with this operation, the response includes a subset of the actual data that was uploaded for the specified analysis, rather than the summary of the analysis that's returned when you use the default media type. The response also includes additional data such as the `github/alertNumber` and `github/alertUrl` properties. The data is formatted as SARIF version 2.1.0.

The following is an example cURL command using the API to list the code scanning alerts for an organization:

```bash
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/orgs/ORG/code-scanning/alerts
```

Review the [GitHub REST API docs](https://docs.github.com/rest/code-scanning/code-scanning) for more information about the using the code scanning API.

###### CodeQL CLI

The CodeQL CLI is a standalone product that you can use to analyze code. Its main purpose is to generate a database representation of a codebase, a CodeQL database. Once the database is ready, you can query it interactively, or you can run a suite of queries to generate a set of results in SARIF format and upload the results to GitHub.com. The CodeQL CLI is free to use on public repositories maintained on GitHub.com, and it's available to use on customer owned private repositories with an Advanced Security license. Download the CodeQL bundle from [https://github.com/github/codeql-action/releases](https://github.com/github/codeql-action/releases).

The bundle contains:

- CodeQL CLI product
- A compatible version of the queries and libraries from [https://github.com/github/codeql](https://github.com/github/codeql)
- Precompiled versions of all the queries included in the bundle

You should always use the CodeQL bundle, because this ensures compatibility and also gives much better performance than a separate download of the CodeQL CLI and checkout of the CodeQL queries.

###### Code-scanning analysis with GitHub Actions

To use GitHub Actions to upload a third-party SARIF file to a repository, you'll need a GitHub Actions workflow. A GitHub Actions workflow is an automated process, made up of one or more jobs, configured as a `.yml` file. Workflows are stored in the `.github/workflows` directory for your repository.

Your workflow uses the `upload-sarif` action, which is part of the `github/codeql-action` repository. This workflow includes input parameters that you can use to configure the upload.

The main input parameter is `sarif-file`, which configures the file or directory of SARIF files to be uploaded. The directory or file path is relative to the root of the repository.

The `upload-sarif` action can be configured to run when the `push` and `scheduled` event occurs.

This example outlines the elements of the `upload-sarif` action yml file:

```yaml
name: 'Code Scanning : Upload SARIF'
description: 'Upload the analysis results'
author: 'GitHub'
inputs:
  sarif_file:
    description: |
      The SARIF file or directory of SARIF files to be uploaded to GitHub code scanning.
      See https://docs.github.com/en/code-security/code-scanning/integrating-with-code-scanning/
      uploading-a-sarif-file-to-github#uploading-a-code-scanning-analysis-with-github-actions
      for information on the maximum number of results and maximum file size supported by code scanning.
    required: false
    default: '../results'
  checkout_path:
    description: "The path at which the analyzed repository was checked out. 
    Used to relativize any absolute paths in the uploaded SARIF file."
    required: false
    default: ${{ github.workspace }}
  token:
    default: ${{ github.token }}
  matrix:
    default: ${{ toJson(matrix) }}
  category:
    description: String used by Code Scanning for matching the analyses
    required: false
  wait-for-processing:
    description: If true, the Action will wait for the uploaded SARIF to be processed before completing.
    required: true
    default: "false"
runs:
  using: 'node12'
  main: '../lib/upload-sarif-action.js' 
```

Each time the results of a new code scan are uploaded, the results are processed and alerts are added to the repository. GitHub uses properties in the SARIF file to display alerts. For example, to prevent duplicate alerts for the same problem, code scanning uses fingerprints to match results across various runs so they only appear once in the latest run for the selected branch. SARIF files created by the CodeQL analysis workflow include this fingerprint data in the `partialFingerprints` field. If you upload a SARIF file using the `upload-sarif` action and this data is missing, GitHub attempts to populate the `partialFingerprints` field from the source files.

If your SARIF file doesn't include `partialFingerprints`, the `upload-sarif` action will calculate the `partialFingerprints` field for you and attempt to prevent duplicate alerts. GitHub can only create `partialFingerprints` when the repository contains both the SARIF file and the source code used in the static analysis.

SARIF upload supports a maximum of 5,000 results per upload. Any results over this limit are ignored. If a tool generates too many results, you should update the configuration to focus on results for the most important rules or queries.

For each upload, SARIF upload supports a maximum size of 10 MB for the gzip-compressed SARIF file. Any uploads over this limit will be rejected. If your SARIF file is too large because it contains too many results, you should update the configuration to focus on results for the most important rules or queries.

###### Upload SARIF files generated outside your repository

You can also create a new workflow that uploads SARIF files after you commit them to your repository. This is useful when the SARIF file is generated as an artifact outside of your repository.

In the following example, the workflow runs anytime commits are pushed to the repository. The action uses the `partialFingerprints` property to determine if changes have occurred.

In addition to running when commits are pushed, the workflow is scheduled to run once per week. This workflow uploads the `results.sarif` file located in the root of the repository. You could also modify this workflow to upload a directory of SARIF files. For example, you could place all SARIF files in a directory in the root of your repository called `sarif-output` and set the action's input parameter `sarif_file` to `sarif-output`.

```yml
name: "Upload SARIF"

// Run workflow each time code is pushed to your repository and on a schedule. 
//The scheduled workflow runs every Thursday at 15:45 UTC.

on:
  push:
  schedule:
    - cron: '45 15 * * 4'

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      security-events: write
  steps:
    # This step checks out a copy of your repository.
    - name: Checkout repository
      uses: actions/checkout@v2
    - name: Upload SARIF file
      uses: github/codeql-action/upload-sarif@v1
      with:
        # Path to SARIF file relative to the root of the repository
        sarif_file: results.sarif 
```

###### Upload SARIF files generated as part of a CI workflow

If you generate your third-party SARIF file as part of a continuous integration (CI) workflow, you can add the `upload-sarif` action as a step after running your CI tests. If you don't already have a CI workflow, you can create one using a starter workflow in the [https://github.com/actions/starter-workflows](https://github.com/actions/starter-workflows) repository.

In this example, the workflow runs anytime commits are pushed to the repository. The action uses the `partialFingerprints` property to determine if changes have occurred. In addition to running when commits are pushed, the workflow is scheduled to run once per week.

This example shows the ESLint static analysis tool as a step in a workflow. The `Run ESLint` step runs the ESLint tool and outputs the `results.sarif` file. The workflow then uploads the `results.sarif` file to GitHub using the `upload-sarif` action.

````
  ```
  name: "ESLint analysis"

// Run workflow each time code is pushed to your repository and on a schedule.
// The scheduled workflow runs every Wednesday at 15:45 UTC.
on:
  push:
  schedule:
    - cron: '45 15 * * 3'

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      security-events: write
    steps:
      - uses: actions/checkout@v2
      - name: Run npm install
        run: npm install
      // Runs the ESlint code analysis
      - name: Run ESLint
        // eslint exits 1 if it finds anything to report
        run: node_modules/.bin/eslint build docs lib script spec-main -f node_modules/@microsoft/eslint-formatter-sarif/sarif.js -o results.sarif || true
      // Uploads results.sarif to GitHub repository using the upload-sarif action
      - uses: github/codeql-action/upload-sarif@v1
        with:
          // Path to SARIF file relative to the root of the repository
          sarif_file: results.sarif
  ```
````
### Configure code scanning

You can configure how GitHub scans the code in your project for vulnerabilities and errors. When you choose your own configuration, you save time and decide the best frequency of code scanning for your project. In this unit, you'll learn the basics of code scanning configuration. You'll also learn how to configure the frequency of scans and schedule them to best fit your repository and development needs.

As we discussed in the previous units, you can run code scanning on GitHub, using GitHub Actions, or from your continuous integration (CI) system. Selecting the **Advanced** setup option on GitHub generates a customizable workflow file that you can then commit directly to your repository. You usually don't need to edit this workflow. However, if necessary, you can customize some of the settings.

For example, you can edit GitHub's CodeQL analysis workflow to specify the frequency of scans, the languages or directories to scan, and what CodeQL code scanning looks for in your code. You might also need to edit the CodeQL analysis workflow if you use a specific set of commands to compile your code. CodeQL analysis is just one type of code scanning you can perform in GitHub. The GitHub Marketplace contains several other code scanning workflows.

##### Switching from Default to Advanced Code Scanning Setup

If you already have a repository set up to use code scanning using the default setup method, you can switch to using the Advanced setup in the settings. Navigate to the **Code scanning** section under **Settings > Code security and analysis**, and then select the three dots overflow icon (**...**). In the drop-down, select **Switch to advanced**. Then, follow the prompts to disable CodeQL, and re-enable it with the advanced setup's generated workflow file.

#### Edit code-scanning workflow

GitHub saves workflow files in the _.github/workflows_ directory of your repository. You can find a workflow you have added by searching for its file name. For example, by default, the workflow file for CodeQL code scanning is called _codeql-analysis.yml_.

Follow these steps to edit a workflow file:

1. To open the workflow editor, select the **Edit** icon in the upper-right corner of the file view.
    
    ![Screenshot of the Edit button](https://learn.microsoft.com/en-gb/training/github/configure-code-scanning/media/2-edit-button-screenshot.png)
    
2. Make your edits.
    
3. After you have edited the file, select **Commit changes** and complete the Commit changes form. You can choose to commit directly to the current branch, or create a new branch and start a pull request.
    
    ![Screenshot of the Commit changes form.](https://learn.microsoft.com/en-gb/training/github/configure-code-scanning/media/4-commit-changes.png)
    

Review the following sections for some common code scanning configuration options.

##### Configure frequency

A common edit to the workflow file is to adjust the frequency with which code scanning occurs. You can configure the CodeQL analysis workflow to scan code on a schedule or when specific events occur in a repository. You can also edit the workflow file to scan code when someone pushes a change and whenever a pull request is created. Adjusting this frequency prevents developers from introducing new vulnerabilities and errors into the code. Scanning code on a schedule informs you about the latest vulnerabilities and errors that GitHub, security researchers, and the community discover. Even when developers aren't actively maintaining the repository.

###### Scan on Push

By default, the CodeQL analysis workflow uses the `on:push` event to trigger a code scan on every push to the default branch of the repository and any protected branches. For code scanning to be triggered on a specified branch, the workflow must exist in that branch. If you scan on push, the results appear in the **Security** tab for your repository.

Additionally, when an `on:push` scan returns a result that can be mapped to an open pull request, these alerts automatically appear on a pull request in the same place as other pull request alerts. The alerts are identified by comparing the existing analysis of the head of the branch to the analysis for the target branch.

###### Scan on PR

The default CodeQL analysis workflow uses the `pull_request` event to trigger a code scan on pull requests targeted against the default branch. If a pull request is from a private fork, the `pull_request` event is only triggered if you've selected the "Run workflows from fork pull requests" option in the repository settings. If you scan pull requests, the results appear as alerts in a pull-request check.

If you use the `pull_request` trigger, configured to scan the pull request's merge commit rather than the head commit, it produces more efficient and accurate results than scanning the branch head on each push. However, if you use a CI/CD system that can't be configured to trigger on pull requests, you can still use the `on:push` trigger so that code scanning maps the results to open pull requests on the branch and adds the alerts as annotations on a pull request.

##### Define the severities causing pull request check failure

By default, only alerts with the severity level of `Error` or security severity level of `Critical` or `High` cause a pull-request check failure. Pull-request failures don't stop a code scan but represent a blocker when trying to merge code. You can find the list of pull-request failures in the **Code scanning alerts** tab under your repository's **Security**. In your repository settings, you can change the levels of alert severities and of security severities that cause a pull request check failure.

1. On GitHub.com, navigate to the repository main page. Under your repository name, select **Settings**.
    
    ![screenshot of the Settings button](https://learn.microsoft.com/en-gb/training/github/configure-code-scanning/media/3-severities-2-settings-screenshot.png)
    
2. In the left sidebar, select **Code security and analysis**.
    
    ![screenshot of the Code security and analysis button.](https://learn.microsoft.com/en-gb/training/github/configure-code-scanning/media/3-severities-3-security-analysis-screenshot.png)
    
3. In the **Code scanning** section under **Protection rules**, use the drop-down menu to select the severity level you would like to trigger a pull request check failure.
    
    ![screenshot of the code scanning alert severity drop-down menu.](https://learn.microsoft.com/en-gb/training/github/configure-code-scanning/media/3-severities-4-level-severity-screenshot.png)
    

##### Avoid unnecessary scans of pull requests

You might want to avoid a code scan being triggered on specific pull requests targeted against the default branch, irrespective of which files have been changed. You can configure this setting by specifying `on:pull_request:paths-ignore` or `on:pull_request:paths` in the code-scanning workflow. For example, if the only changes in a pull request are to files with the file extensions `.md` or `.txt` you can use the following `paths-ignore` array.

```yaml
on:
   push:
      branches: [main, protected]
   pull_request:
      branches: [main]
      paths-ignore:
         - '**/*.md'
         - '**/*.txt'
```

##### Adjust scanning schedule

If you use the default CodeQL analysis workflow, the workflow scans the code in your repository once a week at a randomly generated day and time, in addition to the scans triggered by events. To adjust this schedule, edit the `cron` value in the workflow.

The following example shows a CodeQL analysis workflow for a repository with a default branch called `main` and one protected branch called `protected`:

```yaml
on:
   push:
      branches: [main, protected]
   pull_request:
      branches: [main]
   schedule:
      - cron: '20 14 * * 1'
```

This workflow scans:

- Every push to the default branch and the protected branch
- Every pull request to the default branch
- The default branch every Monday at 14:20 UTC

## Introduction to GitHub Copilot
### Introduction

GitHub Copilot is the world's first at-scale AI developer tool that can help you write code faster with less work. GitHub Copilot draws context from comments and code to suggest individual lines and whole functions instantly.

Research finds that when GitHub Copilot helps developers code faster, they can focus on solving bigger problems, stay in the flow longer, and feel more fulfilled with their work.

OpenAI created the generative pretrained language model in GitHub Copilot, powered by OpenAI Codex. An extension is available for Visual Studio Code (VS Code), Visual Studio, Neovim, and the JetBrains suite of integrated development environments (IDEs).
### GitHub Copilot, your AI pair programmer

![The logo icon for GitHub Copilot that shows the Copilot icon in the middle with a blue and green swirl around the logo.](https://learn.microsoft.com/en-us/training/github/introduction-to-github-copilot/media/github-copilot.png)

It's no secret that AI is disrupting the technology landscape. AI is profoundly changing the way the world works and how each organization and team operates. These advancements in AI serve as a catalyst and can dramatically improve the productivity of developers around the world as they use and apply it well.

The addition of AI features to the developer tools that you use and love helps you collaborate, develop, test, and ship your products faster and more efficiently than ever before. GitHub Copilot is a service that provides you with an AI pair programmer that works with all of the popular programming languages.

In recent research, GitHub and Microsoft found that developers experience a significant productivity boost when they use GitHub Copilot to work on real-world projects and tasks. In fact, in the three years since its launch, developers have experienced the following benefits while using GitHub Copilot:

- 46% of new code now written by AI
- 55% faster overall developer productivity
- 74% of developers feeling more focused on satisfying work

Microsoft developed GitHub Copilot in collaboration with OpenAI. GitHub Copilot is powered by the OpenAI Codex system. OpenAI Codex has broad knowledge of how people use code and is more capable than GPT-3 in code generation. OpenAI Codex is more capable, in part, because it was trained on a dataset that included a larger concentration of public source code.

GitHub Copilot is available as an extension for VS Code, Visual Studio, Vim/Neovim, and the JetBrains suite of IDEs.

#### GitHub Copilot features

GitHub Copilot started a new age of software development as an AI pair programmer that keeps developers in the flow by autocompleting comments and code. But AI-powered autocompletion was just the starting point.

Here are some features of GitHub Copilot that truly make it a developer tool of the future. With these features, GitHub Copilot is more than just an editor. It's becoming a readily accessible AI assistant throughout the entire development life cycle.

##### Copilot for chat

GitHub Copilot brings a ChatGPT-like chat interface to the editor. The chat interface focuses on developer scenarios and natively integrates with VS Code and Visual Studio. It's deeply embedded in the IDE, and it recognizes what code a developer has typed and what error messages appear. A developer can get in-depth analysis and explanations of what code blocks are intended to do, generate unit tests, and even get proposed fixes to bugs.

##### Copilot for pull requests

OpenAI's GPT-4 model adds support in GitHub Copilot for AI-powered tags in pull-request descriptions through a GitHub app that organization admins and individual repository owners can install. GitHub Copilot automatically fills out these tags based on the changed code. Developers can then review or modify the suggested descriptions.

##### Copilot for the CLI

Next to the editor and pull requests, the terminal is the place where developers spend the most time. However, even the most proficient developers need to scroll through many pages to remember the precise syntax of many commands. The GitHub Copilot command-line interface (CLI) can compose commands and loops, and it can and throw obscure `find` flags to satisfy your query.

#### Subscription plans

The service is available through GitHub personal accounts with GitHub Copilot Free and GitHub Copilot Pro, through organization accounts with GitHub Copilot Business, or through enterprise accounts with GitHub Copilot Enterprise.

##### GitHub Copilot Free

GitHub Copilot Free allows individual developers to use GitHub Copilot at no cost. To get started, open Visual Studio Code, click on the GitHub Copilot icon, and then click "Sign in to Use GitHub Copilot for Free". Log in to your GitHub account in the window that will open in the browser.

The GitHub Copilot Free tier includes 2000 code completions per month, 50 chat requests per month, and access to both GPT-4o and Claude 3.5 Sonnet models. [Learn more.](https://gh.io/copilot)

##### GitHub Copilot Business

GitHub Copilot Business allows you to control who can use GitHub Copilot in your company. After you give access to an organization, its admins can give access to individuals and teams.

With GitHub Copilot Business, GitHub Copilot is open to every developer, team, organization, and enterprise.

With the following features, GitHub Copilot Business is focused on making organizations more productive, secure, and fulfilled:

- Code completions
- Chat in IDE and mobile
- Filter for security vulnerabilities
- Code referencing
- Filter for public code
- IP indemnity
- Enterprise-grade security, safety, and privacy

##### GitHub Copilot Enterprise

GitHub Copilot Enterprise is available for organizations through GitHub Enterprise Cloud. This subscription plan enables your teams of developers to:

- Quickly get up to speed on your codebase.
- Search through and build documentation.
- Get suggestions based on internal and private code.
- Quickly review pull requests.

GitHub Copilot Enterprise includes everything in GitHub Copilot Business, plus a layer of personalization for organizations. It provides integration into GitHub as a chat interface, so developers can converse about their codebase. It also provides action buttons throughout the platform.

GitHub Copilot Enterprise can index an organization's codebase for a deeper understanding and for suggestions that are more tailored. It offers access to GitHub Copilot customization to fine-tune private models for code completion.
### Interact with Copilot

#### Inline suggestions

Inline suggestions are the most immediate form of assistance in Copilot. As you type, Copilot analyzes your code and context to offer real-time code completions. This feature predicts what you might want to write next and displays suggestions in a subtle, unobtrusive way.

The suggestions that Copilot offers appear as grayed-out text ahead of your cursor.

- To accept a suggestion, select the `Tab` key or the `>` (right arrow) key.
- To reject a suggestion, keep typing or select the `Esc` key.

Inline suggestions are especially useful when you're working on repetitive tasks or you need quick boilerplate code.

Here's an example:

```python
def calculate_average(numbers):
    # Start typing here and watch Copilot suggest the function body
```

#### Command palette

The command palette provides quick access to the various functions in Copilot, so you can perform complex tasks with only a few keystrokes.

1. Open the command palette in Visual Studio Code by selecting `Ctrl+Shift+P` (Windows or Linux) or `Cmd+Shift+P` (Mac).
2. Enter **Copilot** to see available commands.
3. Select actions like **Explain This** or **Generate Unit Tests** to get assistance.

#### Copilot chat

Copilot chat is an interactive feature that enables you to communicate with Copilot by using natural language. You can ask questions or request code snippets, and Copilot provides responses based on your input.

1. Open the Copilot chat panel in your IDE.
2. Enter questions or requests in natural language, and then evaluate the Copilot response.

For example, you might enter: "How do I implement a binary search in Python?" Copilot chat is ideal for exploring new coding concepts or getting help with unfamiliar syntax.

Copilot might respond with:

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

#### Inline chat

Inline chat enables context-specific conversations with Copilot directly within your code editor. You can use this feature to request code modifications or explanations without switching contexts.

1. Place your cursor where you want assistance.
2. Use the keyboard shortcut `Ctrl+I` (Windows or Linux) or `Cmd+I` (Mac) to open inline chat.
3. Ask questions or request changes specific to that code location.

Inline chat helps you focus on a specific section of your code and receive targeted advice. Additionally, you can utilize slash commands for more efficient interaction.

Slash commands are shortcuts that allow you to quickly perform actions in Copilot. These commands provide a convenient way to interact with Copilot without needing to navigate through menus.

Here are some common slash commands and their usage:

- `/explain` - Provides an explanation of the selected code.
- `/suggest` - Offers code suggestions based on the current context.
- `/tests` - Generates unit tests for the selected function or class.
- `/comment` - Converts comments into code snippets.

To use a slash command, just type the command in your editor and press `Enter`. For example:

```python
# Select the function, use the shortcut to open the inline chat, and type: /explain
def calculate_average(numbers):
```

#### Comments to code

Copilot uses natural language processing to convert comments into code. You can describe the functionality that you want in a comment. When you select the `Enter` key, Copilot generates code based on your description.

Here's an example:

```python
# Function to reverse a string
def reverse_string(s):
    # Copilot suggests the function body here
```

```python
## Function to reverse a string
def reverse_string(s):
    return s[::-1]
```

This approach is beneficial for drafting code quickly, especially when your task is straightforward.

#### Multiple suggestions

For complex code snippets, Copilot can offer multiple alternatives.

1. When Copilot offers a suggestion, look for the light bulb icon.
2. Select the icon or use `Alt+]` (Windows/Linux) or `Option+]` (Mac) to cycle through alternatives.

Multiple suggestions help you explore different coding approaches and select the most appropriate one.

#### Explanations

Understanding existing code is crucial, especially in large projects. You can use the **Explain This** feature to get explanations for code snippets.

1. Select a block of code.
2. Right-click the code block, and then select **Copilot: Explain This** on the shortcut menu.
3. Read the explanation that Copilot provides for the selected code.

This feature is useful for learning purposes and when you're reviewing code that someone else wrote.

#### Automated test generation

Unit tests are essential for ensuring code quality and reliability. Copilot can save you time and effort by generating unit tests for your functions or classes.

1. Select a function or class.
2. Use the command palette to select **Copilot: Generate Unit Tests**.
3. Review the test cases that Copilot suggests for your code.

Here's an example:

```python
def add(a, b):
    return a + b

# Copilot might generate a test like this:
def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0
    assert add(0, 0) == 0
```

Automated test generation helps you maintain code integrity and catch bugs early in the development process.

Keep in mind that Copilot learns from context. Keeping your code well structured and commented helps Copilot provide more accurate and relevant assistance. The more you interact with Copilot, the better it becomes at understanding your coding style and preferences.
### Set up, configure, and troubleshoot GitHub Copilot

#### Sign up for GitHub Copilot

Before you can start using GitHub Copilot, you need to set up a free trial or subscription for your account.

To get started, select your GitHub profile photo, and then select **Settings**. Copilot is on the left menu under **Code, planning, and automation**.

After you sign up, you need to install an extension for your preferred environment. GitHub Copilot supports GitHub.com (which doesn't need an extension), VS Code, Visual Studio, JetBrains IDEs, and Neovim as an unobtrusive extension.

For this module, you'll just review extensions and configurations for VS Code. The exercise that you'll complete in the next unit uses VS Code.

#### Configure GitHub Copilot in VS Code

##### Add the VS Code extension for GitHub Copilot

1. In Visual Studio Marketplace, go to the [GitHub Copilot extension page](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) and select **Install**.
2. A popup dialog asks you to open VS Code. Select **Open**.
3. In VS Code, on the **Extension: GitHub Copilot** tab, select **Install**.
4. If you didn't previously authorize VS Code in your GitHub account, you're prompted to sign in to GitHub in VS Code. Select **Sign in to GitHub**.

GitHub Copilot can autocomplete code as you type when you use VS Code. After installation, you can enable or disable GitHub Copilot, and you can configure advanced settings within VS Code.

##### Enable or disable GitHub Copilot in VS Code

1. On the bottom pane of the VS Code window, select the status icon, and then select **Enable** or **Disable**.
    
    ![Screenshot of the status icon for GitHub Copilot in Visual Studio Code. When GitHub Copilot is enabled, the background color matches the color of the status bar.](https://learn.microsoft.com/en-us/training/github/introduction-to-github-copilot/media/status-icon-visual-studio-code.png)
    
2. When you're disabling GitHub Copilot, VS Code asks whether you want to disable completions globally or for the language of the file that you're currently editing.
    
    - To disable GitHub Copilot completions globally, select **Disable completions**.
    - To disable GitHub Copilot completions for a specified language, select **Disable completions for LANGUAGE**.

##### Enable or disable inline suggestions in VS Code

1. On the **File** menu, select **Preferences** > **Settings**.
    
    ![Screenshot of the File menu in Visual Studio Code. The Preferences dropdown submenu is open with the Settings command selected.](https://learn.microsoft.com/en-us/training/github/introduction-to-github-copilot/media/vsc-settings.png)
    
2. On the left-side pane of the **Settings** tab, select **Extensions**, and then select **GitHub Copilot**.
    
3. Under **Editor: Enable Auto Completions**, select or clear the checkbox to enable or disable inline suggestions.
    

Additionally, you can choose to enable or disable inline suggestions and specify for which languages you want to enable or disable GitHub Copilot.

#### Troubleshoot GitHub Copilot in VS Code

In VS Code, the log files are useful for diagnosing connection problems. The GitHub Copilot extension stores the log files in the standard log location for VS Code extensions. You can find the log files by opening the command palette and then entering either **Developer: Open Log File** or **Developer: Open Extensions Logs Folder**.

In rare cases, errors might not be logged in the regular locations. If you encounter errors and nothing is in the logs, you might try to view the logs from the process that's running VS Code and the extension. This process enables you to view the Electron logs. You can find these logs by selecting **Help** > **Toggle Developer Tools** in VS Code.

Network restrictions, firewalls, or your proxy might cause problems when you're connecting to GitHub Copilot. If a problem occurs, use the following steps to open a new editor with the relevant information that you can inspect yourself or share with the support team:

1. Open the VS Code command palette, and then:
    
    - For Mac, use `Shift+Command+P`.
    - For Windows or Linux, use `Ctrl+Shift+P`.
2. Enter **Diagnostics**, and then select **GitHub Copilot: Collect Diagnostics** from the list.
## Code with GitHub Codespaces
### Introduction

GitHub Codespaces is an instant, cloud-based development environment that uses a container to provide you with common languages, tools, and utilities for development.
### The Codespace lifecycle

GitHub Codespaces is configurable, allowing you to create a customized development environment for your project. By configuring a custom development environment for your project, you can have a repeatable Codespace configuration for all users of your project.

A Codespace's lifecycle begins when you create a Codespace and ends when you delete it. You can disconnect and reconnect to an active Codespace without affecting its running processes. You can stop and restart a Codespace without losing the changes that you make to your project.

![Diagram of a circular lifecycle of a Codespace that starts with creating and ends with deleting.](https://learn.microsoft.com/en-us/training/github/code-with-github-codespaces/media/codespace-circular-lifecycle.png)

#### Create a Codespace

You can create a Codespace on GitHub.com, in Visual Studio Code, or by GitHub CLI. There are four ways to create a Codespace:

- From a GitHub template or any template repository on GitHub.com to start a new project.
- From a branch in your repository, for new feature work.
- From an open pull request, to explore work-in-progress.
- From a commit in a repository's history to investigate a bug at a specific point in time.

You can temporarily use a Codespace in order to test code or you can return to the same Codespace to work on long-running feature work.

You can create more than one Codespace per repository or even per branch. However, there are limits to the number of Codespaces you can create and run at the same time. When you reach the maximum number of Codespaces and try to create another, a message is displayed. The message tells you that an existing Codespace needs to be removed/deleted before a new Codespace can be created.

You can create a new Codespace each time you develop in GitHub Codespaces or keep a long-running Codespace for a feature. If starting a new project, create a Codespace from a template and publish it to a repository on GitHub later.

When creating a new Codespace each time you work on a project, you should regularly push your changes to ensure that any new commits are on GitHub. When using a long-running Codespace for a new project, pull from the repository's default branch each time you start working in Codespace to enable your environment to get the latest commits. The workflow is similar to working with a project on a local machine.

Repository administrators can enable GitHub Codespaces prebuilds for a repository to speed up Codespace creation.

For an in-depth walkthrough and step-by-step guidance, see the resources titled **A beginner’s guide to learning to code with GitHub Codespaces** and **Developing in a Codespace** located in the Summary unit at the end of this module.

##### Codespace creation process

![Diagram of a GitHub codespace and how it connects from your code editor and into a docker container.](https://learn.microsoft.com/en-us/training/github/code-with-github-codespaces/media/codespace-connection-editor.png)

When you create a GitHub Codespace, four processes occur:

1. A virtual machine and storage are assigned to your Codespace.
2. A container is created.
3. A connection to the Codespace is made.
4. A post-creation setup is made.

##### Save changes in a Codespace

When you connect to a Codespace through the web, AutoSave is automatically enabled to save changes after a specific amount of time passes. When you connect to a Codespace through Visual Studio Code running on your desktop, you must enable AutoSave.

Your work saves to a virtual machine in the cloud. You can close and stop a Codespace and return to the saved work at a later time. If you have unsaved changes, you receive a prompt to save them before exiting. However, if your Codespace is deleted, then your work is lost. To save your work, you must commit your changes and push them to your remote repository or publish your work to a new one if you created your Codespace from a template.

##### Open an existing Codespace

You can reopen any of your active or stopped Codespaces on GitHub.com, in a JetBrains IDE, in Visual Studio Code, or by using GitHub CLI.

To resume an existing Codespace, you can go to the repository where the Codespace exists, select the `,` key and then select **Resume this codespace**. Or, you can open [https://github.com/codespaces](https://github.com/codespaces) in the browser, select the repository, and then select the existing Codespace.

##### Timeouts for a Codespace

If a Codespace is inactive, or if you exit your Codespace without explicitly stopping, the application times out after a period of inactivity and stops running. The default timeout is after 30 minutes of inactivity. When a Codespace times out, your data is kept from the last time your changes were saved.

##### Internet connection while using GitHub Codespaces

A Codespace requires an internet connection. If the connection to the internet is lost while working in a Codespace, you aren't able to access your Codespace. However, any uncommitted changes are saved. When you reestablish the internet connection, you can access the Codespace in the same state that it was left in when the connection was lost.

If you have an unstable internet connection, you should frequently commit and push your changes.

#### Close or stop a Codespace

If you exit the Codespace without running the stop command or leave the Codespace running without interaction, the Codespace and its running processes continue during the inactivity timeout period. The default inactivity timeout period is 30 minutes. You can define your personal timeout setting for the Codespaces you create, but an organization's timeout policy can overrule the setting.

Only running Codespaces incur CPU charges. A stopped Codespace incurs only storage costs.

You can stop and restart a Codespace to apply changes. For example, if you change the machine type used for your Codespace, you need to stop and restart it for the change to take effect. When you close or stop your Codespace, all uncommitted changes are preserved until you connect to the Codespace again.

You can also stop Codespace and choose to restart or delete it if you encounter an error or something unexpected.

#### Rebuild a Codespace

You can rebuild your Codespace to implement changes to your dev container configuration. For most uses, you can create a new Codespace as an alternative to rebuilding a Codespace. When you rebuild your Codespace, images from the cache speed-up the rebuild process. You can also perform a full rebuild to clear the cache and rebuild the container with fresh images.

When you rebuild the container in a Codespace, changes you made outside the `/workspaces` directory are cleared. Changes you made inside the `/workspaces` directory, including the clone of the repository or template you created the Codespace from, are preserved over a rebuild.

#### Delete a Codespace

You can create a Codespace for a particular task. After you push your changes to a remote branch, then you can safely delete that Codespace.

If you try to delete a Codespace with unpushed git commits, the editor notifies you that you have changes that aren't yet pushed to a remote branch. You can push any desired changes and then delete your Codespace. You can also continue to delete your Codespace and any uncommitted changes or export the code to a new branch without creating a new Codespace.

Stopped Codespaces that remain inactive for a specified amount of time are deleted automatically. Inactive Codespaces delete after 30 days, but you can customize your Codespace retention intervals.
### Personalize your Codespace

GitHub Codespaces is a dedicated environment for you. You can configure your repositories with a dev container to define their default GitHub Codespaces environment and personalize your development experience across all of your Codespaces with dotfiles and Settings Sync.

#### What you can customize

There are many ways you can customize your Codespace. Let's review each one.

- **Settings Sync:** You can synchronize your Visual Studio Code (VS Code) settings between the desktop application and the VS Code web client.
- **Dotfiles:** You can use a dotfiles repository to specify scripts, shell preferences, and other configurations.
- **Rename a Codespace:** When you create a Codespace, an autogenerated display name is assigned to it. If you have multiple Codespaces, the display name helps you to differentiate between Codespaces. You can change the display name for your Codespace.
- **Change your shell:** You can change your shell in a Codespace to keep the setup you're used to. When you're working in a Codespace, you can open a new terminal window with a shell of your choice, change your default shell for new terminal windows, or install a new shell. You can also use dotfiles to configure your shell.
- **Change the machine type:** You can change the type of machine that's running your Codespace, so that you're using resources appropriate for the work you're doing.
- **Set the default editor:** You can set your default editor for Codespaces in your personal settings page. Set your editor preference so that when you create a Codespace or open an existing Codespace, it opens to your default editor.
    - Visual Studio Code (desktop application)
    - Visual Studio Code (web client application)
    - JetBrains Gateway - for opening Codespaces in a JetBrains IDE
    - JupyterLab - the web interface for Project Jupyter
- **Set the default region:** You can set your default region in the GitHub Codespaces profile settings page to personalize where your data is held.
- **Set the timeout:** A Codespace will stop running after a period of inactivity. By default this period is 30 minutes, but you can specify a longer or shorter default timeout period in your personal settings on GitHub. The updated setting applies to any new Codespaces you create, or to existing Codespaces the next time you start them.
- **Configure automatic deletion:** Inactive Codespaces are automatically deleted. You can choose how long your stopped Codespaces are retained, up to a maximum of 30 days.

#### Add to your Codespace with extensions or plugins

You can add plugins and extensions within a Codespace to personalize your experience in JetBrains and VS Code.

##### VS Code extensions

If you work on your Codespaces in the VS Code desktop application or the web client, you can add any extensions you need from the Visual Studio Code Marketplace. Refer to [Supporting Remote Development and GitHub Codespaces](https://code.visualstudio.com/api/advanced-topics/remote-extensions) in the VS Code documentation for information on how extensions run in GitHub Codespaces.

If you already use VS Code, you can use Settings Sync to automatically sync extensions, settings, themes, and keyboard shortcuts between your local instance and any Codespaces you create.

##### JetBrains plugins

If you work on your Codespaces in a JetBrains IDE, you can add plugins from the JetBrains Marketplace.
### Codespaces versus GitHub.dev editor

You're probably asking yourself, when should I use GitHub Codespaces and when should I use GitHub.dev?

You can use GitHub.dev to navigate files and sources code repositories from GitHub, and make and commit code changes. You can open any repository, fork, or pull request in GitHub.dev editor.

If you want to do more heavy lifting like testing your code, use GitHub Codespaces. It has compute associated with it so you can build your code, run your code, and have terminal access. GitHub.dev doesn't have compute in it. With GitHub Codespaces, you get the power of a personal Virtual Machine (VM) with terminal access, the same way you could use your local environment, just in the cloud.

##### Comparison of Codespaces and GitHub.dev

The following table lists the main differences between Codespaces and GitHub.dev:

||GitHub.dev|GitHub Codespaces|
|---|---|---|
|Cost|Free|Free monthly quota of usage for personal accounts.|
|Availability|Available to everyone on GitHub.com|Available to everyone on GitHub.com.|
|Startup|GitHub.dev opens instantly with a key-press and you can start using it right away without having to wait for configuration or installation.|When you create or resume a Codespace, the Codespace is assigned a VM. The container is then configured based on the contents of a devcontainer.json file. This setup takes a few minutes to create the development environment.|
|Compute|There are no associated compute resources, so you can't build and run your code or use the integrated terminal.|With GitHub Codespaces, you get the power of a dedicated VM to run and debug your application.|
|Terminal access|None|GitHub Codespaces provides a common set of tools by default, meaning that you can use the Terminal exactly as you would in your local environment.|
|Extensions|Only a subset of extensions that can run on the web appear in the extensions view and can be installed|With GitHub Codespaces, you can use most extensions from the Visual Studio Code Marketplace.|

##### Continue working on Codespaces

You can start your workflow in GitHub.dev and continue working on a Codespace. If you try to access the Run and Debug View or the Terminal, you see a notification that they're not available in GitHub.dev.

To continue your work in a Codespace, select **Continue Working on…**. Select **Create New Codespace** to create a Codespace on your current branch. Before you choose this option, you must commit any changes.
## Manage your work with GitHub Projects
### Introduction

We know your work is dynamic. Priorities can change quickly and needing to stay current and aware of everything is how you and your team can be successful.

Luckily, GitHub Projects can help you stay organized, connected, and up-to-date in order to keep your team on track.

Projects connect your planning directly to the work your team is doing and flexibly adapts to whatever your team needs at any point. Project tables are built like a spreadsheet and give you a live canvas to filter, sort, and group issues and pull requests. You can use Project tables, Project boards, and custom fields to track a sprint, plan a feature, or manage a large-scale release.
### Projects versus Projects Classic

Before we dive into learning how to utilize the new and improved Projects, let's take a moment to walk through what has changed from Projects (Classic).

Let's first go over some of the enhancements in a side-by-side glance and then dive deeper into each section of updates.

#### Projects vs Projects (Classic)

||Projects|Projects (Classic)|
|---|---|---|
|Tables and Boards|Boards, Lists, Timeline Layout|Boards|
|Data|Sort, rank, and group items by custom fields such as text, number, date, iteration and single select|Columns and Cards|
|Insights|Create visuals to help understand your work through historical and current charts with Projects|Progress bar|
|Automation|Use GraphQL API, Actions, and Column presets to manage your Project|Configure Column presets for when issues and pull requests are added, edited, or closed|

The new GitHub Projects provides a richer experience that enables you to keep track of your work, where you work. Let's dive a bit deeper into the changes that have been made.

#### Comprehensive lists of Project enhancements

##### Tables and boards

- Plan and track work in a table or board view
- Rank, sort, and group within a table by any custom field
- Create draft issues with detailed descriptions and metadata
- Materialize any perspective with tokenized filtering and saved views
- Customize cards and group-by in Project boards
- Real-time Project updates and user presence indicators

##### Data

- Define custom fields of type: text, number, date, iteration, and single select
- Configure iterations with flexible date ranges and breaks to represent your sprints, cycles, or quarterly roadmap
- View linked pull requests and reviewers in both table and board views

##### Insight

- Create and configure custom bar, column, line, and stacked area charts
- Use aggregation functions like sum, count, average, min, and max to get the proper insight
- Persist charts and share them with a URL to keep everyone in the know

##### Automation

- GraphQL ProjectsV2 API
- GitHub app Project scopes
- Webhooks events for Project item metadata updates
- GitHub Action to automate adding issues to Projects

### How to create a project

Imagine you want to organize your team's feature backlog. Projects, GitHub's built-in program-management tool, is a perfect way to organize and prioritize your team's work in a single space.

#### Creating an organization-level Project

First, you want to lay the foundation by creating a new Project. Creating is relatively quick and simple.

1. In the top right corner of GitHub.com, select your profile photo, then select **Your organizations**.
    
    ![Screenshot of the Profile Dropdown Menu.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/3-github-profile-drowdown.png)
    
    Screenshot of the Profile Dropdown Menu that includes Your profile, Your repositories, Your Codespaces, Your organizations, and Your enterprises with Your Organization option highlighted.
    
2. Scroll down to select the organization for your new Project.
    
3. Navigate from the **Overview** tab to the **Projects** tab.
    
4. Select the green button labeled **New Project**.
    
5. A pop-up prompts you to select either a template or start from scratch. Let's choose the **Start from scratch** option and select **Table**.
    
6. Select the green **Create project** button.
    

You just created a Project!

You can also create a personal Project by selecting your profile photo and navigating to **Your projects**. Once you're on your Projects page, select the green button titled **New project**.

#### Set your Project's name, description, and README

Let's define your Project in a couple of different ways so that your team can easily understand what you're tracking.

1. Navigate to your newly created Project to edit your Project's name, description, and README.
    
2. At the top right of the page, select the three dots to open the menu and select **Settings**.
    
3. **Project Name** is where you edit the name of the Project.
    
4. **Short description** allows you to add a few words about the Project.
    
5. **README** lets you add information for your team to understand why you created this Project and what you hope to accomplish with it. Once finished, select **Save changes**.
    
    ![Screenshot of a Project README that is highlighted with example text that describes the user's Project.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/3-project-readme-example.png)
    

#### Add issues and pull requests to your Project

Adding issues and pull requests to your Project is what makes the tool so powerful. Projects enable you to know the status of tasks your team is working on to coordinate and complete your goals.

Let's go through the different ways to add issues and pull requests to your Project.

##### Add an existing issue and pull request

1. Copy the url of an existing issue or pull request.
    
2. Place your cursor in the bottom row of the Project next to the **+** and paste the URL of your issue or pull request.
    
    ![Screenshot of a Project in List view with an example of a URL of an Issue pasted into the Project.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/3-project-list-view-url-sample.png)
    
3. Press **Enter** and your issue or pull request appears as a task in your Project.
    

##### Search for an existing issue and pull request

You can search for existing issues or pull requests by adding a new item.

1. Enter # to search repositories. You can type part of the repository name to narrow down your options.
    
    ![Screenshot of a Project in List view, focused on searching for an existing issue or pull request by adding a # and typing in key phrases.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/3-project-list-view-search.png)
    
2. Select the repository where the pull request or issue is located, which prompts to search issues and pull requests.
    
3. Start typing the title of the issue or pull request to find the one you want.
    
4. Select the issue or pull request.
    

##### Bulk add issues and pull requests

You can bulk add issues and pull requests to an existing repository to save time. It allows you to start organizing your team faster.

1. Select **+** in the bottom row of the Project.
    
2. Select **Add item from repository**.
    
3. To change the repository, select the dropdown and choose a repository. The issues and pull requests then populate.
    
4. You can either select all or select those issues or pull requests you want to include.
    
    ![Screenshot of bulk adding issues and pull requests from a repository, with the option to search for specific issues or pull requests highlighted.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/3-bulk-add-issues-and-pr.png)
    
5. Once you're ready to add the issues and pull requests to your Project, select the green button titled **Add selected items** in the bottom right corner.

### How to organize your project

Now that you added issues and pull requests to your Project, it's time to organize to keep track of the great work you and your team are doing.

#### Create a field to track and group by priority

To group a set of issues and pull requests by priority, you need to first create a new field.

1. In the table view, in the rightmost field header, select **+**.
    
2. Select **New field**.
    
    ![Screenshot of the top of a Project showing the columns for Notes and Priority. The New Field Button as a plus sign is highlighted.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/4-project-new-field.png)
    
3. Type the name of your field. In this case, it's _Priority_.
    
4. Select the **Field Type** drop-down.
    
5. To create your own classification for your new field, select the **Single select** option.
    
    ![Screenshot of the drop-down menu for a New Field.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/4-new-field-drop-down.png)
    
    Screenshot of the drop-down menu for a New Field that contains Text, Number, Date, Single select, and Iteration with the Single Select option highlighted.
    
6. In the **Options** text box, start to add your different priority levels. You can label them as **Urgent**, **High**, **Medium**, and **Low**.
    
7. Select **Save**.
    

Now that you have your priority classification set up, you need to classify your issues and pull requests based on priority. To make a classification, select the issue or pull request you want to classify in the field row titled **Priority**. Now, in the drop-down field, select the priority you want to choose for this particular issue or pull request.

Repeat for your remaining pull requests and issues.

Great!

Now, let's group your issues and pull requests by priority to make it easier to focus on urgent and high priority items.

1. Select the **down arrow** next to the name of your currently opened view.
2. Select the **Group by** option.
3. Select **Priority**.

Now you should be able to view issues and pull requests based on the priority you assigned them. One of the great features of this particular view is you can now drag and drop issues into new priority fields easily.

![Screenshot example of Priority Classification within Project List view.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/4-priority-classification-example.png)

Screenshot example of Priority Classification within Project List view with Issues and Pull Requests that are organized and grouped as High, Medium, and Low classifications.

Now that you have your work prioritized, let's tackle timelines and iterations.

If you want to save this view, select the **Save changes** button on the top-right of the list view.

#### Add an iteration field

Adding an iteration field to your Project can help you and your team visualize the balance of upcoming work in order to help everyone stay on track. An iteration field enables you to set up phases for your tasks in a tangible timeframe to keep you and your team organized.

1. To add an iteration field, go to your Project's table view.
    
2. In the rightmost field header, select **+**.
    
3. Select **New field**.
    
4. Add a **Field name**, such as _Project Phase_ or _Sprint_.
    
5. Under **Field Type**, select _Iteration_.
    
6. Choose a **Starts On** date.
    
7. Change the **Duration** of each iteration by typing a new number, and select the drop-down for either **days** or **weeks** as follows.
    
    ![Screenshot of the Iteration Field Date Editing Field with the options to edit start date and duration in weeks.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/4-iteration-field.png)
    
8. Select **Save and create**.
    

Once you have your iteration field set up, you can now assign what iteration phase you want each of your issues and pull requests to fall under.

Now that you've prioritized and organized your Project, let's take a look at how to view your Project from a board view perspective.

#### Create a board view

A board view of your Project enables you to view upcoming tasks in a more visual way.

Let's walk through how to get your board view up and running.

1. On the currently open view, select the **down arrow**.
2. Under **Layout**, select **Board**. When you change the layout, your Project displays an indicator to show the view was modified.
3. Select the **Save** button at the top-right of the board.
4. You can rename the view by double-clicking the view's tab, and selecting out of the tab to automatically save.
5. Note these steps can also be accomplished by selecting **New View** to the right of your existing views.

Now, you can drag and drop issues and pull requests to the various columns.

![Screenshot example of a Project board with four columns labeled; no status, todo, in-progress, done.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/4-project-boards.png)
### How to organize and automate your project

You created your Project, added issues and pull requests, and organized it. Now, let's talk about how to:

- Provide visibility and access to your Project.
- Close and delete your Project.

#### Project visibility and access

##### Control visibility to your Project

You have the ability to control whether your Project is public or private. When your Project is public, everyone on the internet can view it. When your Project is private, only users granted at least read access can see your Project.

To change your Project's visibility:

1. Navigate to your Project.
    
2. In the top-right, select the three dots at the top menu and choose **Settings**.
    
3. Scroll down to **Danger zone**, and under **Visibility** select Private or Public from the drop-down.
    
    ![Screenshot of the Danger Zone settings with the option to make your Project Public or Private.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/5-danger-zone-settings.png)
    

##### Manage access to your Project

Access to your Project depends on if your Project is an organization-level Project or a personal/user-level Project. Managing access is similar between the two levels.

Admins of organization-level Projects can manage access for the entire organization, for teams, for individual organization members, and for outside collaborators. Admins of user-level Projects can invite individual collaborators and manage their access.

###### Organization-level Project

- **No access**: Only organization owners and users granted individual access can see the Project. Organization owners are also admins for the Project.
- **Read**: Everyone in the organization can see the Project. Organization owners are also admins for the Project.
- **Write**: Everyone in the organization can see and edit the Project. Organization owners are also admins for the Project.
- **Admin**: Everyone in the organization is an admin for the Project.

###### Personal/User-level Project

- **Read**: The individual can view the Project.
- **Write**: The individual can view and edit the Project.
- **Admin**: The individual can view, edit, and add new collaborators to the Project.

##### Invite collaborators and change roles

1. Navigate to your Project.
    
2. In the top right, select the three dots to open the menu and choose **Settings**.
    
3. In the left-hand navigation bar, select **Manage access**.
    
4. Once on the page you can either:
    
    - Invite individuals and teams by searching in the **Invite collaborators** search bar.
    - Change their role or remove them under **Manage access**.
    
    ![Screenshot of the Manage access settings with the ability to add a single collaborator or team and select their role or remove them.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/5-manage-access-settings.png)
    

##### Add a Project to a team

You can add Projects to your team to give them collaborator access to their Projects. Adding lists them on the team's Projects page, which makes it easier for members to identify which Project a particular team uses. Teams are granted read permissions on any Project they get added to.

Here's how to add Projects to teams:

1. In the top right corner of GitHub.com, select your profile photo and choose **Your organizations**.
2. Select the name of your organization.
3. Navigate to the **Teams** tab and select the name of the team to which you want to grant access.
4. Select **Projects** and choose **Link a project**.
5. Start typing the name of the Project you want to add and then select the Project in the list of matches.

##### Add a Project to a repository

You can list relevant Projects in a repository so your team can access information they need to stay up to date. However, you can only list Projects if the same user or organization owns both the Projects and the repository. In order for repository members to see a Project listed in a repository, they must have visibility to the Project.

Here are the steps to add a Project to a repository:

1. Navigate to the main page of your repository.
    
2. Select the **Projects** tab and choose to **Link a project**.
    
    ![screenshot of the green Link a project button to add to a repository.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/5-add-project.png)
    
3. Search for Projects owned by the same user or organization as the repository owner.
    
4. Select a Project to list the Project in your repository.
    

#### Close and delete Projects

Once you complete a Project or you no longer need to use it, you can either close or delete it.

Closing a Project enables you to remove it from the list of Projects but retain the content and ability to reopen the Project later. We recommend this option to preserve your data.

However, deleting a Project permanently removes it from the platform along with any saved views, custom fields and associated values, insights data, and drafted issues.

Regardless of which option you choose, both closing and deleting Project settings are in the same location.

Here are steps on how to navigate to them:

1. Navigate to your Project.
    
2. In the top-right, select the three dots to open the menu and choose **Settings**.
    
3. Scroll down to the **Danger zone** section and either select **Close project** or **Delete project**.
    
    - Selecting **Delete project** prompts you to read the warnings, and then type the name of your Project into the text box.
    
    ![Screenshot of the Danger zone section with the option to change visibility, close Project and delete Project with delete Project highlighted.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/5-danger-zone-options.png)
    

### Insight and automation with projects

#### Insights with Projects

##### Insights and how they can be useful

Insights with Projects enables you to view, create, and customize charts that use items added to your Project as source data. When you create a chart, you set the filters, chart type, and information displayed. The chart is available to anyone who can view the Project. You can generate two types of charts: current charts and historical charts. Let's dive into the differences between the two.

###### Current charts

You can create current charts to visualize your Project items. For example, you can create charts to show the number of items assigned to each individual, or the number of issues assigned to each upcoming iteration.

You can use filters to manipulate the data used to build your chart. For example, you can create a chart showing how much upcoming work you have, but limit those results to particular labels or assignees.

![Screenshot example of a current bar chart that tracks the number of hours spent per seven iteration phases. Color coded by amount of time spent on Bugs, Feedback, Backend, and UI work.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/6-current-chart-example.png)

###### Historical charts

Historical charts are available with GitHub Team and GitHub Enterprise Cloud for organizations. Historical charts are time-based charts that allow you to view your Project's trends and progress. You can view the number of items over time grouped by status and other fields. The default _Burn up_ chart shows item status over time, allowing you to visualize progress and spot patterns.

![Screenshot example of a historic stacked area line graph showing progress during the month of July.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/6-historical-chart-example.png)

Screenshot example of a historic stacked area line graph showing the number of hours spent on to dos, in progress, and completed tasks during the month of July.

##### Create and customize charts

Follow these steps to create a new chart:

1. Navigate to your Project.
2. In the top-right, select the line graph button. When you hover over the button, the **Insights** label appears.
3. In the menu on the left, select **New chart**.
4. Filter by keyword or field to change the data used to build the chart.
5. To the right of the filter text box, select **Save**.

Now that you created a new chart, let's customize your new chart to fit your needs.

1. In the menu on the left, select the chart you'd like to configure.
2. On the right side of the page, select **Configure**, and a panel opens.
3. Select the **Layout** dropdown to change the type of chart you want to use.
4. Select the **X-axis** dropdown and choose the field you want to use.
5. Optionally, select **Group by** to group items on your X-axis. Choose the field you want to use or _None_ to disable grouping.

##### Automation with Projects

Let GitHub do some of the work for you by automating your Project. There are three different ways you can do so:

- Built-in automated workflows
- GraphQL API
- GitHub Actions with workflows

The easiest way to automate your Project is built-in workflows. GraphQL and Actions give more control over customizing automation. In the following sections, you learn how to utilize Project's built-in automation and briefly go over GraphQL API and GitHub Actions automation.

##### Configure built-in workflows

Built-in workflows help you stay aware of all your work. Your Project takes newly created issues or pull requests and automatically puts them into your Project with a _Todo_ status. Here's how to enable:

1. In the top-right corner of your Project, select the three dots menu and choose **Workflows**.
    
    ![Screenshot of the Workflows menu on Projects that contains the options, Workflows, Archived items, and Settings with Workflows highlighted.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/6-automation-workflows-menu.png)
    
2. In the left column, under Default workflows, select **Item added to project**.
    
    ![Screenshot of the menu to enable workflows once an action occurs.](https://learn.microsoft.com/en-us/training/github/manage-work-github-projects/media/6-automation-default-workflows-items.png)
    
    Screenshot of the menu to enable workflows once an action occurs. Options include Item added to Project, Item reopened, Item closed, Code changes requested, Code review approved, Pull request merged with Item added to Project highlighted.
    
3. Select the **Edit** button to make changes to the workflow.
    
4. In the **When an item is added to the project** section, ensure that both issues and pull requests are selected.
    
5. In the **Set Value** section, select **Status:Todo**.
    
6. Select **Save and turn on workflow**.
    

Congratulations, you automated your Project!

#### GitHub Actions with workflows

GitHub Actions enables the most customization for your Project's automation. You can use GitHub Actions to automate your project management tasks by creating workflows. Each workflow contains a series of tasks that are performed automatically every time the workflow runs. An example workflow triggers upon issue creation that adds a label, leaves a comment, and moves the issue to a project board.

An issue creation triggers a workflow that adds a label, leaves a comment, and moves the issue to a project board.

Learn more about automating workflows for your Project in the article _Automating Projects using Actions_ at the end of this module.

##### GraphQL API

If you're using GraphQL in GitHub, you can utilize an API to help automate your Project. 
## Communicate effectively on GitHub using Markdown
### Introduction
Markdown allows you to organize and emphasize what you're trying to communicate on GitHub.

A markup language, Markdown offers a lean approach to content editing. It defines a concise, lightweight syntax that strips out the overhead inherent to HTML, providing a more approachable creation experience. It's become the standard for sites like GitHub, and enjoys broad editor support in both client and browser forms.
### What is Markdown?

Markdown is a markup language that offers a lean approach to content editing by shielding content creators from the overhead of HTML. While HTML is great for rendering content exactly how it was intended, it takes up a lot of space and can be unwieldy to work with, even in small doses. Markdown offers a great compromise between the power of HTML for content description and the ease of plain text for editing.

In this unit, we'll discuss Markdown's structure and syntax. We'll also cover features of GitHub-Flavored Markdown (GFM), which are syntax extensions that allow you to integrate GitHub features into content.

#### Emphasize text

The most important part of any communication on GitHub is usually the text itself, but how do you show that some parts of the text are more important than others?

Using italics in text is as easy as surrounding the target text with single asterisks (`*`) or single underscores (`_`). Just be sure to close an emphasis with the same character with which you opened it. Be observant of how you combine the use of asterisks and underscores. Here are several examples:

```markdown
This is *italic* text.
This is also _italic_ text.
```

> This is _italic_ text. This is also _italic_ text.

Create bold text by using two asterisks (`**`) or two underscores (`__`).

```markdown
This is **bold** text.
This is also __bold__ text.
```

> This is **bold** text. This is also **bold** text.

You can also mix different emphases.

```markdown
_This is **italic and bold** text_ using a single underscore for italic and double asterisks for bold.
__This is bold and *italic* text__ using double underscores for bold and single asterisks for italic. 
```

> _This is **italic and bold** text_ using a single underscore for italic and double asterisks for bold. **This is bold and _italic_ text** using double underscores for bold and single asterisks for italic.

To use a literal asterisk, precede it with an escape character; in GFM, that's a backslash (`\`). This example results in the underscores and asterisks being shown in the output.

```markdown
\_This is all \*\*plain\*\* text\_.
```

> _This is all **plain** text_.

#### Declare headings

HTML provides content headings such as the `<h1>` tag. In Markdown, this is supported via the # symbol. Just use one # for each heading level from 1 to 6.

```markdown
###### This is H6 text
```

> ###### This is H6 text

#### Link to images and sites

Image and site links use a similar syntax.

```markdown
![Link an image.](/learn/azure-devops/shared/media/mara.png)
```

> ![Link an image.](https://learn.microsoft.com/en-us/training/azure-devops/shared/media/mara.png)

```markdown
[Link to Microsoft Training](/training)
```

> [Link to Microsoft Training](https://learn.microsoft.com/en-us/training)

#### Make lists

You can define ordered or unordered lists. You can also define nested items through indentation.

- Ordered lists start with numbers.
- Unordered lists can use asterisks or dashes (`-`).

Here's the Markdown for an ordered list:

```markdown
1. First
2. Second
3. Third
```

Result:

> 1. First
> 2. Second
> 3. Third

Here's the Markdown for an unordered list:

```markdown
- First
  - Nested
- Second
- Third
```

> - First
>     - Nested
> - Second
> - Third

#### Build tables

You can construct tables using a combination of pipes (`|`) for column breaks and dashes (`-`) to designate the prior row as a header.

```markdown
First|Second
-|-
1|2
3|4
```

> |First|Second|
> |---|---|
> |1|2|
> |3|4|

#### Quote text

You can create blockquotes using the greater than (`>`) character.

```markdown
> This is quoted text.
```

> > This is quoted text.

#### Fill the gaps with inline HTML

If you come across an HTML scenario not supported by Markdown, you can use that HTML inline.

```markdown
Here is a<br />line break
```

> Here is a  
> line break

#### Work with code

Markdown provides default behavior for working with inline code blocks delimited by the backtick (`) character. When decorating text with this character, it's rendered as code.

```markdown
This is `code`.
```

> This is `code`.

If you have a code segment spanning multiple lines, you can use three backticks (```) before and after to create a fenced code block.

````
```markdown
var first = 1;
var second = 2;
var sum = first + second;
```
````

```
var first = 1;
var second = 2;
var sum = first + second;
```

GFM extends this support with syntax highlighting for popular languages. Just specify the language as part of the first tick sequence.

````
```javascript
var first = 1;
var second = 2;
var sum = first + second;
```
````

```JavaScript
var first = 1;
var second = 2;
var sum = first + second;
```
#### Cross-link issues and pull requests

GFM supports various shortcode formats to make it easy to link to issues and pull requests. The easiest way to do this is to use the format `#ID`, such as `#3602`. GitHub automatically adjusts longer links to this format if you paste them in. There are also additional conventions you can follow, such as if you're working with other tools or want to specify other projects/branches.

|Reference type|Raw reference|Short link|
|---|---|---|
|Issue or pull request URL|`https://github.com/desktop/desktop/pull/3602`|[#3602](https://github.com/desktop/desktop/pull/3602)|
|`#` and issue or pull request number|#3602|[#3602](https://github.com/desktop/desktop/pull/3602)|
|`GH-` and issue or pull request number|GH-3602|[GH-3602](https://github.com/desktop/desktop/pull/3602)|
|`Username/Repository#` and issue or pull request number|desktop/desktop#3602|[desktop/desktop#3602](https://github.com/desktop/desktop/pull/3602)|


#### Link specific commits

You can link to a commit by either pasting in its ID or simply using its secure hash algorithm (SHA).

|Reference type|Raw reference|Short link|
|---|---|---|
|Commit URL|[https://github.com/desktop/desktop/commit/](https://github.com/desktop/desktop/commit/)||
|8304e9c271a5e5ab4fda797304cd7bcca7158c87|[8304e9c](https://github.com/desktop/desktop/commit/8304e9c271a5e5ab4fda797304cd7bcca7158c87)||
|SHA|8304e9c271a5e5ab4fda797304cd7bcca7158c87|[8304e9c](https://github.com/desktop/desktop/commit/8304e9c271a5e5ab4fda797304cd7bcca7158c87)|
|User@SHA|desktop@8304e9c271a5e5ab4fda797304cd7bcca7158c87|[desktop@8304e9c](https://github.com/desktop/desktop/commit/8304e9c271a5e5ab4fda797304cd7bcca7158c87)|
|Username/Repository@SHA|desktop/desktop@8304e9c271a5e5ab4fda797304cd7bcca7158c87|[desktop/desktop@8304e9c](https://github.com/desktop/desktop/commit/8304e9c271a5e5ab4fda797304cd7bcca7158c87)|

#### Mention users and teams

Typing an `@` symbol followed by a GitHub username sends a notification to that person about the comment. This is called an "@mention", because you're mentioning the individual. You can also `@mention` teams within an organization.

```markdown
@githubteacher
```

[@githubteacher](https://github.com/githubteacher)

#### Track task lists

You can create task lists within issues or pull requests using the following syntax. These can be helpful to track progress when used in the body of an issue or pull request.

```markdown
- [x] First task
- [x] Second task
- [ ] Third task
```

![Screenshot of a GitHub task list.](https://learn.microsoft.com/en-us/training/github/communicate-using-markdown/media/2-task-list.png)

#### Slash commands

Slash commands can save you time by reducing the typing required to create complex Markdown.

You can use slash commands in any description or comment field in issues, pull requests, or discussions where that slash command is supported.

|Command|Description|
|---|---|
|`/code`|Inserts a Markdown code block. You choose the language.|
|`/details`|Inserts a collapsible detail area. You choose the title and content.|
|`/saved-replies`|Inserts a saved reply. You choose from the saved replies for your user account. If you add `%cursor%` to your saved reply, the slash command places the cursor in that location.|
|`/table`|Inserts a Markdown table. You choose the number of columns and rows.|
|`/tasklist`|Inserts a tasklist. This slash command only works in an issue description.|
|`/template`|Shows all of the templates in the repository. You choose the template to insert. This slash command works for issue templates and a pull request template.|
## Contribute to an open-source project on GitHub
### Introduction

Open-source software relies heavily on the community for its long-term sustainability. One way to contribute to open-source projects is by making contributions to the project's repository and conducting code reviews.

Suppose you've been using open-source libraries for your projects and at work for quite some time. In the spirit of open source, you've decided to contribute back to some of these libraries and frameworks.

However, you've never contributed before, and you're not sure how to get started.
### Identify where you can help

**Open-source** software can be freely used, modified, and shared by anyone. Using open-source software, anyone can view, modify, and distribute a project for any purpose. The idea behind open-source software is that sharing code leads to better, more reliable software.

There are many ways to contribute to open-source projects. Making your first contribution can often be a scary experience, but it shouldn't be. Open source is a place for everyone, and contributions happen at all levels.

#### Find an open-source project that needs contributions

You can get started by thinking about the projects you already use, or want to use. Contributing is easier when you're familiar with the project and its community.

Perhaps while reading a project's README file, you find a broken link or some typos. Maybe you noticed something isn't working as expected, or the documentation is out of date. These are all great opportunities to help and contribute to the project.

>**Tip**: One important tip: _All_ kinds of contributions are valuable. Your level of experience or knowledge of the project doesn't matter here. We all have something we can contribute. Be confident in yourself. The most important thing here is the will to help.

#### Use GitHub search

You can also use GitHub search to explore topics and related projects. Head to [GitHub search](https://github.com/search), and enter your topic word.

Let's say you're interested in machine learning.

![Screenshot showing GitHub search topics.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/2-code-search.png)

You can then narrow your search by selecting **Topics** in the left sidebar.

![Screenshot showing the results of a GitHub narrow search.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/2-topic-search.png)

From there, you can find repositories relevant to your search keyword and repositories curated by community members.

#### Familiarize yourself with an open-source project

Something worth mentioning here is that every open-source community is different. After you've found a project, you'll need to familiarize yourself with the project and its participation guidelines.

Most projects will have these documents at the top level of the repository:

- **LICENSE:** The project must contain an [open-source license](https://choosealicense.com/). If the project doesn't have a license, it's not open source.
- **README:** The README file usually serves as the welcome page for the project. It generally provides information on how to get started using the project. It's also common for it to add information on how to engage with the community.
- **CONTRIBUTING:** As its name suggests, this document provides guidance on how to contribute to the project. It usually describes how the contribution process works, and includes details on how to set up your development environment.
- **CODE_OF_CONDUCT:** The code of conduct sets ground rules for community members. By doing so, it helps make the community a safe and welcoming environment for all.

Although not all projects have CONTRIBUTING or CODE_OF_CONDUCT documents, having these documents is a good indication of how friendly and welcoming a project is.

Open-source contributors and maintainers come from all over the world. Projects usually have multiple communication channels to organize discussions and ask for help. A good way to familiarize yourself with the community is by reading through some of these communication channels:

- **Issue tracker:** Where folks discuss issues and tasks related to the project. To find the issues in GitHub, you can go to the main page of the repository on GitHub and add `/issues` to the end of the URL, for example: [https://github.com/jupyter/notebook/issues](https://github.com/jupyter/notebook/issues).
- **Pull request:** Where folks discuss and review changes to the project. You can find it in GitHub by adding `pulls` to the project's URL, for example, [https://github.com/jupyter/notebook/pulls](https://github.com/jupyter/notebook/pulls).
- **Chat channels and forums:** Some projects use chat channels, such as Slack, Gitter, and IRC, or forums like Discourse for conversations and discussions.

#### Identify tasks to work on

You've found a project, you've read the contribution guidelines, and now you're ready to contribute.

Perhaps you've already identified something to work on, such as fixing broken links or updating the docs. A good way to find beginner-friendly issues to help with is by visiting the project's `/contribute` URL, for example: [https://github.com/jupyter/notebook/contribute](https://github.com/jupyter/notebook/contribute).

![Screenshot showing the Contribute to a project section on GitHub.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/2-contribute.png)

You'll notice that most of the issues displayed in the `contribute` URL will have labels such as `good-first-issue`, `help wanted`, `beginner-friendly`, and so on. Labels are often used to provide top-level information of the issue and the type of help needed.

You can head to the labels page, for example: [https://github.com/jupyter/notebook/labels](https://github.com/jupyter/notebook/labels). Then, select issues that have labels like `help wanted`, `discussion`, or other labels relevant to the type of contribution in which you're interested.

As you explore issues, you might also notice that some have other issues or pull requests linked.

![Screenshot showing a pull request linked to an issue.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/2-linked-pr.png)

#### Sponsor a project

There are many ways to contribute to open source. You can financially support the folks who build and maintain the open-source ecosystem through code, leadership, mentorship, design, and beyond.

Open source heavily relies on volunteer work. GitHub Sponsors allow you to fund projects and individuals to help them keep doing their open-source work, while giving them the recognition they deserve.

If a project is eligible for sponsorship through GitHub Sponsors, you'll find a **Sponsor** button on the project's main page.

![Screenshot showing the sponsoring box on a GitHub project page.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/2-sponsor.png)

You can select the sponsorship tier and if you want your contribution to be public.

![Screenshot showing sponsorship tiers.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/2-tier.png)
### Contribute to an open-source repository

After you identify an area where you can contribute, the next step is to prepare your contribution. We'll review here how you can communicate your intent to participate in a project, forge a pull request, and improve your chances of getting it accepted.

When it comes to contributing work to an open-source project, communication is a key success factor. You might find it uncomfortable to communicate with others on your proposed changes or improvements. Often, this dialogue will lead to discussions and compromises on your original vision.

Avoiding active communication with others who are involved in an open-source project means risking your time working on tasks that someone else is already working on. Or, you might work on features or improvements that don't align with the project's values or best practices. In either case, everyone's time is wasted. Conversely, committing to active communication ensures that your work will be well received and impactful.

How can you ensure success when you communicate with other project members about new features and changes? First, try to keep an open mind. Be open to feedback and practice patience. Open-source project maintainers most likely have a day job and a private life to tend to. If you don't get an answer immediately, wait a little longer before you ping the maintainers.

#### Communicate your intent to maintainers

You should always start by communicating your intent to contribute before you do any actual work. Unless indicated otherwise in the README file, the issue tracker is usually the best place for doing that.

- If you want to work on an existing issue, check that nobody is assigned to it by looking at the **Assignees** section. Also check the **Linked pull requests** section. A linked pull request means somebody is already working on it. Look through the comments to see if someone stated their interest to work on the issue. If everything's clear, post a comment on the issue to indicate your interest to work on it. That way, you're telling people who might come later that someone's working on the issue. Also, if needed, maintainers can reply to you with guidance and advice.
    
    ![Screenshot showing the Assignees and Linked pull requests sections.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-checks.png)
    
- If you want to work on a new feature or a bug that's not already present in the issue tracker, create a new issue. Make sure to follow the issue template if one is proposed, and clearly express your intent to work on the issue. If it's a new feature proposition or if the issue requires many changes, make sure to get the maintainers' approval before you move on to the next step.
    

#### Create a pull request on a GitHub repository

After you've communicated your intent to help the project, you're now ready to start working on your actual contribution.

Your contribution will take the form of a _pull request_ or _PR_. A pull request is a special place on GitHub that contains a few things:

- A title and description for your changes.
- One or more commits that constitute the changes you're proposing.
- Comments, where everyone can participate in a discussion about the changes.
- Code reviews, where you can find detailed feedback on your changes and eventually commit suggestions.
- Status checks that come, for example, from automated tests that the maintainers might have put in place. Status checks can serve different purposes. For example, they can ensure that your changes follow the project's rules, or that your changes don't break the code.

After a pull request is created, it can be updated with new commits, comments, or code reviews. This process continues until the project maintainers approve and merge the pull request or reject the changes and close the pull request. When your pull request is merged, it means that your changes have been integrated into the project's codebase.

##### Create a pull request step by step

1. Open the GitHub page of the project to which you want to contribute.
    
2. Select the **Fork** button to create a copy of the repository on your GitHub account. This step is necessary because, by default, you don't have the permissions to make any changes on a public repository unless it's your own copy. By forking the project, you're creating a copy where you can make changes.
    
    ![Screenshot showing the Fork button of a GitHub project.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-fork.png)
    
3. Select **Your repositories** from your account profile menu.
    
    ![Screenshot showing the profile drop-down menu and the entry called Your repositories.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-my-repositories.png)
    
4. Select the repository fork.
    
5. Select the **Code** button to get information on how to "clone" the Git repository to your local machine.
    
    ![Screenshot showing the options for cloning a GitHub project.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-clone.png)
    
6. Select the **clipboard** icon to copy the repository URL, then enter in a terminal:
    
    ```shell
    git clone <REPOSITORY_URL>
    ```
    
    This command will create a copy of the repository on your local machine.
    
    Alternatively, you can use [GitHub Desktop](https://desktop.github.com/) if you prefer to use an application. Or, you can use [GitHub Codespaces](https://github.com/features/codespaces) if the option is proposed to you. If you're a Visual Studio Code user, GitHub Codespaces will feel familiar to you.
    
7. After the project has finished cloning, enter the project folder:
    
    ```shell
    cd <PROJECT_FOLDER>
    ```
    
8. (Optional) Create a new branch by using the following command:
    
    ```shell
    git checkout -b <BRANCH_NAME>
    ```
    
    This step isn't mandatory, but is highly recommended. With a new branch, you can work on multiple contributions separately, each one using a different branch.
    
9. Make the desired changes to the project and commit them:
    
    ```shell
    git add .
    git commit -m "<COMMIT_MESSAGE>"
    ```
    
    These commands will stage your changes for commit, then create a commit with the specified message. Be sure to describe your changes accurately in the commit message. It's also a good idea to check if there are mentions in the CONTRIBUTING file for commit-message conventions you need to follow.
    
10. Push your changes to the remote by using the command:
    
    ```shell
    git push --set-upstream origin <BRANCH_NAME>
    ```
    
    This command creates a new branch on the upstream repository on GitHub (your fork), and pushes all your commits to it.
    
     >**Note**: When we talk about an _upstream_ repository, we refer to the remote repository linked to your local repository. The `origin` is the default alias for the repository URL, which was created by Git in step 4.
    
    If you didn't create a branch previously, enter only `git push`.
    
11. Open your project fork on GitHub, and select the **Compare & pull request** button in the suggestion box that appears.
    
    ![Screenshot showing the pull request suggestion box on GitHub.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-pr-suggestion.png)
    
12. Fill in the title and description and select **Create pull request**.
    
    ![Screenshot showing the pull request creation interface.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-create-pr.png)
    
    If there's a template for the pull request description, take the time to fill in all the required information. If there isn't one now, make sure to provide enough context for maintainers to understand what changes you're proposing and why. You should also link back to the related issue by mentioning its number by using `#<ISSUE_NUMBER>`. You can find the issue number next to its title.
    
    ![Screenshot showing issue number.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-issue-number.png)
    

#### Pass the status checks

After you've created the pull request, you might see a section with status checks at the bottom, like this:

![Screenshot showing status checks results on a pull request.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-pr-checks.png)

These status checks are automated checks that the maintainers have put in place to ensure a consistent quality of the project.

To get your pull request accepted, it needs to pass all automated checks. If one is failing like in the preceding screenshot, select the **Details** button to learn more about the failure and to find out what you need to do to fix it.

If you're unsure about what to do with a failing check, you can always use the comments to ask for the maintainers' guidance or help to fix it.

#### Ask for guidance or reviews on pull requests

You might be unsure about some changes you made and want to get the maintainers' opinions. The best way to do that is to comment directly on the pull requests. If you consider your changes a work-in-progress, you also have the option to create a _draft pull request_ instead to ask for guidance or help from other contributors.

![Screenshot showing the draft pull request option.](https://learn.microsoft.com/en-us/training/github/contribute-open-source/media/3-draft-pr.png)

After the project maintainers come by your pull request, they can reply to the conversation or directly review your changes. There are multiple possible outcomes following a pull request review:

- Your changes are approved. Congratulations!
- Your pull request requires some changes. Don't get discouraged! Look closely at the feedback provided. If you make the requested changes, there's a good chance that your pull request will be accepted. If you push new commits to your branch, the pull request will automatically update with the new changes.
- The reviewer made some comments. It usually means that more details are needed about your changes or the motivation behind it.

##### Respond to comments on your pull request

Remember to always be respectful in all your exchanges and to follow the code of conduct. It's likely that before your changes can be accepted, there will be an ongoing discussion with the maintainers or other contributors.

Contributing to open source requires patience. Sometimes you don't get immediate feedback. Don't reach out to the maintainers privately via email, X, or any other means hoping to get a faster answer. This behavior is considered harmful. Discussing things publicly also gives other contributors or passersby the opportunity to learn about the process behind the changes and the best practices to follow.
### Next steps

You've added context to an issue, contributed a code review, and maybe even submitted a pull request of your own. Now, you want to immerse yourself further in the community around the project.

#### Get involved in the community

You'll find frequent contributors to the project in the comment section for issues and pull requests. Or, you can select **Insights** in the repository's navigation, and then select **Contributors** to find other active community members. Visit their GitHub profiles. Sometimes they'll suggest ways to get in touch with them.

You can also [follow organizations and enterprises on GitHub](https://docs.github.com/en/get-started/exploring-projects-on-github) to stay in touch. Your personal dashboard shows public activity for every enterprise, user, or organization you follow.

You can also find like-minded folks by attending meetups or conferences on open-source topics. Or, you can meet people if the project or ecosystem is large enough around the project you're interested in. Find archives with talk recordings for past events, podcasts, newsletters, and mailing lists.

Some projects have centralized communication, which is often referenced on the project's website or in the README file. There might be a Discord server, a Slack community, Gitter, IRC, or even regular "office hours."

#### Code reusability

Code, and solutions, can sometimes be reused across projects. Have you solved a very scoped issue for one project? Chances are other projects can benefit from it as well. You can:

- Publish as a stand-alone library (dependency).
- Mirror the project with your added functionality.
- [Create a GitHub Action](https://learn.microsoft.com/en-us/training/modules/github-actions-automate-tasks/) for others to include in their workflow.

The first option is probably the best course of action when your bit of code is like a plug-in that could be used across web-development projects. Mirroring or forking a project with the addition of your code is useful when you're solving a narrow use case for a small subset of customers, or even a single customer. Consider that you'll need to keep your fork up to date with the upstream repository if you want to benefit from (for instance) security patches.

GitHub Actions are packaged scripts that automate tasks in a software-development workflow in GitHub. The two different types of actions are container actions and JavaScript actions. You can submit your action to the GitHub Marketplace for discoverability. [GitHub Marketplace](https://docs.github.com/en/apps/publishing-apps-to-github-marketplace/github-marketplace-overview/about-github-marketplace-for-apps) connects you to developers who want to extend and improve their GitHub workflows. Use this platform to publish actions and share apps with other users for free.

For all three of the suggested paths, consider that you're now a maintainer of a project. People will come to you with praise, questions, and complaints. Are you ready for such a commitment?

If your project takes off, people's apps might depend on your bit of code. Can you involve more people to take some of the potential load off? Do you have time to add documentation, triage issues, and review suggestions from people you've likely never met before? Consider your "bandwidth," and instead set expectations in your project's README file. Or, you can release your code in a public gist or a blog post. Code doesn't need to be on GitHub to be open source, after all.

## Manage an InnerSource program by using GitHub
### Introduction

Not long ago, the software-development world offered two sharply distinct models: open source and proprietary. Open-source software benefited from its trademark openness: anyone is allowed to offer contributions, so many people do. Proprietary software, on the other hand, limits access via a closed system that prizes the privacy of its intellectual property (IP).

Suppose you're a leader at a company that made significant investments in its proprietary software. It doesn't need to be a technology company; businesses of all shapes and sizes build and maintain their own software and other IP to enjoy a competitive edge in their industry. However, you developed a great respect for the patterns used in open source, such as source-code visibility, project bug awareness, and feature request transparency. You also like the pull-request model that simplifies the integration of external contributions. You'd really like to bring those benefits to your development teams, but don't want to open source the company's valuable software. What you really need is a hybrid that delivers the advantages of both approaches. What you need is InnerSource.
### How to manage a successful InnerSource program

Here, we discuss how you can design an InnerSource program to enjoy the best of open-source patterns within any software development organization.

#### What is InnerSource?

Anyone can freely use, modify, and share open-source software. Using open-source software, anyone can view, modify, and distribute a project for any purpose with the idea that sharing code leads to better, more reliable software.

**InnerSource** is the practice of applying open-source patterns to projects with a limited audience. For example, a company might establish an InnerSource program that mirrors the structure of a typical open-source project, except that it's only accessible to the employees of that company. In effect, it's an open-source program behind your company's firewall.

##### InnerSource benefits

An InnerSource program can offer numerous benefits beyond what traditional closed-source models provide.

First, they _encourage transparency_. Access to the source code of other company projects can help developers be more productive when working on their own projects. They can see how different teams solve problems similar to the ones they're facing, and often find code and other assets that they can reuse. Access to team issues, pull requests, and project plans also provide better data for them to understand the velocity and direction of the project.

Next, they _reduce friction_. Let's say that a consumer team is dependent on a bug fix or new feature for a project owned by a different team. IN an InnerSource program, they have a channel through which they can propose the changes they need. And if those changes can't be merged in for any reason, the consumer team has the option of forking the project to meet their needs.

Finally, they _standardize practices_. A common challenge development organizations face is that different teams often diverge in the ways they operate. Building an InnerSource program is a great opportunity to adopt standard conventions that can be used across every development team, even if they don't follow identical practices. For example, two teams might prefer different processes for accepting contributions. Having them standardize on the way they communicate their different processes makes it much easier for anyone to contribute to either.

These examples are just a few of the benefits enjoyed by InnerSource programs. To learn more, see [An introduction to InnerSource](https://resources.github.com/whitepapers/introduction-to-innersource/).

#### Set up an InnerSource program on GitHub

##### Set repository visibility and permissions

You can configure GitHub repositories with three levels of visibility. Users who don't meet the visibility requirement see "not found" pages when they try to access your repository. The levels are:

- **Public** repositories are visible to everyone. Use this visibility for projects that are truly open source and offer access to people inside and outside of your organization.
- **Internal** repositories are only visible to members of the organization that owns them. Use this visibility for InnerSource projects.
- **Private** repositories are only visible to the owner and any teams or individuals they add. Use this visibility for projects that only specific users and groups should have access to.

Once you establish repository visibility, you can configure permissions on an individual or team basis. There are five permission levels:

- **Read** level is recommended for noncode contributors who want to view or discuss the project.
- **Triage** level is recommended for contributors who need to proactively manage issues and pull requests without write access.
- **Write** level is recommended for contributors who actively push to the project.
- **Maintain** level is recommended for project managers who need to manage the repository without access to sensitive or destructive actions.
- **Admin** level is recommended for people who need full access to the project, including sensitive and destructive actions like managing security or deleting a repository.

Learn more about [repository access permissions by level](https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization).

##### Create discoverable repositories

As an InnerSource program grows, the number of repositories likely scales up significantly. While it's great to have all these assets available to the organization, it can become a challenge to efficiently find content. To proactively address this issue, it's a best practice for teams to consider what they can do to make it easier for others to find and work with their repositories.

A few best practices include:

- Use a descriptive repository name, such as `warehouse-api` or `supply-chain-web`.
- Include a concise description. A sentence or two should be enough for potential users to know if the project might fit their needs.
- [License your repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository) so that customers know how they can use, change, and distribute the software.
- Include a `README.md` file in the repository. GitHub uses this file as the landing page when people visit the repository.

##### Add a README file

A README file communicates expectations for your project and helps you manage contributions. README files can:

- Articulate the purpose and vision of the project so potential consumers understand whether it fits their needs.
- Offer visual aids, such as screenshots or code samples, to illustrate the project in action.
- Include links to a production or demo version of the app for review.
- Set expectations for prerequisites and deployment procedures.
- Include references to the projects on which you depend. These references are a good way to promote the work of others.
- Use Markdown to guide readers through properly formatted content.

If you put your README file in your repository's root directory, or in the hidden `.github` or `docs` directory, GitHub recognizes and automatically surfaces your README to repository visitors. If a repository contains more than one README file, then the file shown is chosen from locations in the following order: the `.github` directory, then the repository's root directory, and finally the `docs` directory.

Check out some [Awesome README examples](https://github.com/matiassingers/awesome-readme).

Once the project launches, use email and other networking channels to promote it. Reaching an appropriate audience could produce a significant boost in project participation.

##### Manage projects on GitHub

As projects gain traction, the influx of users and contributions can require lots of work to manage. Depending on the project, a significant amount of work might be required just to manage the expectations of project participants.

To proactively address this issue, GitHub looks for a `CONTRIBUTING.md` file in the root (or `/docs` or `/.github`) of a repository. Use this file to explain the contribution policy for the project. The exact details might vary, but it's a good idea to let potential contributors know what conventions the project follows. For example, where the team is looking for pull requests, what details are requested for bug reports, and so on.

If a `CONTRIBUTING.md` exists, GitHub presents a link to it when users create issues or pull requests to encourage them to follow it.

![Contributing guidelines links.](https://learn.microsoft.com/en-gb/training/github/manage-innersource-program-github/media/2-contributing-guidelines.png)

Check out some [Awesome CONTRIBUTING.md examples](https://github.com/mntnr/awesome-contributing)

Additionally, consider [adding a CODEOWNERS file](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) to the repository to define individuals or teams that are responsible for reviewing code modifications.

##### Create issue and pull request templates

GitHub supports starter templates for new issues and pull requests. Use these templates to provide the initial description text for a newly created issue or pull request.

For example, if your project has `.github/ISSUE_TEMPLATE.md`, anytime a user starts the process of creating an issue, they see this content. Rather than having to constantly reference the required details from a `CONTRIBUTING.md`, they're able to just fill out the issue like a form using the template text.

![A new issue using the template.](https://learn.microsoft.com/en-gb/training/github/manage-innersource-program-github/media/2-new-issue-template.png)

It's the same for pull requests, except that the path is `.github/PULL_REQUEST_TEMPLATE.md`.

Check out some [Awesome GitHub issue & pull request templates](https://github.com/devspace/awesome-github-templates).

##### Define workflows

For projects that encourage external contributions, be sure to specify what workflow the project follows. The workflow should include details about where and how branches should be used for bugs and features. It should also include how pull requests should be opened, and any other details people outside the repository team should know before they push code. If you don't yet have a workflow in mind, you should consider [the GitHub flow](https://guides.github.com/introduction/flow/).

You should communicate a strategy for managing releases and deployments. These parts of the workflow affect day-to-day branching and merging, so it's important to communicate them to contributors. Learn more about how they relate to your [Git branching strategy](https://learn.microsoft.com/en-us/azure/devops/repos/git/git-branching-guidance).

##### Measuring program success

Any team venturing into InnerSource should think about the kinds of metrics they want to track to gauge the success of their program. While traditional metrics like "time to market" and "bugs reported" are still applicable, they aren't necessarily going to illustrate the benefits achieved through InnerSource.

Instead, consider adding metrics that show how external participation improved project quality. Is the repository receiving pull requests from external sources that fix bugs and add features? Are there active participants in discussions around the project and its future? Is the program inspiring an InnerSource expansion that drives benefits elsewhere in the organization?

In short, metrics are hard, especially when it comes to measuring the value and effect of individual and team contributions. If misused, metrics can harm the culture, existing processes, and diminish the collective sentiment towards the organization or leadership team. When thinking about measuring InnerSource adoption, consider the following guidance on metrics:

- Measure process, not output
    - Code review turnaround time
    - Pull request size
    - Work in progress
    - Time to open
- Measure against targets and not absolutes
- Measure teams and not individuals
    - Number of unique contributors to a project
    - Number of projects reusing code
    - Number of cross-team @mentions

Learn about the successes others enjoyed in these [InnerSource case studies](https://gist.github.com/githubteacher/9fe53687a5f173d1d64c24c68625349e).


## Maintain a secure repository by using GitHub best practices
### Introduction

Software security is always important, and it spans the entire software-development lifecycle. Focus is often dedicated towards writing secure code and locking down infrastructure. It's also important to protect the processes that occur during every stage of the software-development lifecycle.

Suppose you're managing an important GitHub repository. You want to enforce the highest level of security, but also want to offer a welcoming experience for contributors. Unfortunately, being secure often introduces friction that obstructs everyone's productivity. To mitigate this overhead, GitHub offers various automated features that allow you to efficiently administer a secure repository without slowing everyone down throughout the entire development process.
### How to maintain a secure GitHub repository

Here, we discuss some of the essential security tools and techniques available to GitHub repository administrators.

>**Note***: The following content doesn't cover the fundamentals of writing secure code, but rather important security considerations, tools, and features to use within a GitHub repository.

#### The importance of a secure development strategy

Application security is important. News services frequently carry stories about some breach of a company's systems and private company and customer data that was stolen.

So, what are the issues to think about when planning a secure development strategy? Clearly, we need to protect information from being disclosed to people that shouldn't have access to it, but more importantly, we need to ensure that information is only altered or destroyed when it's appropriate.

We need to make sure we properly authenticate who's accessing the data and that they have the correct permissions to do so. Through historical or archival data or logs, we need to be able to find evidence when something is wrong.

There are many aspects to building and deploying secure applications. Here are three things to consider:

- **There's a general knowledge problem**: Many developers and other staff members assume they understand security, but they don't. Cybersecurity is a constantly evolving discipline. A program of ongoing education and training is essential.
    
- **Code must be created correctly and securely**: We need to be sure that the code is created correctly and securely implements the required features. We also need to make sure that the features were designed with security in mind.
    
- **Applications must comply with rules and regulations**: We need to make sure that the code complies with required rules and regulations. We have to test for compliance while building the code and then retest periodically, even after deployment.
    

##### Security at every step

![Image of a GitHub shield with security written underneath.](https://learn.microsoft.com/en-gb/training/github/maintain-secure-repository-github/media/github-security.png)

Security isn't something you can just add later to an application or a system. Secure development must be part of every stage of the software-development life cycle. This concept is even more important for critical applications and those applications that process sensitive or highly confidential information.

In practice, to hold teams accountable for what they develop, processes need to **shift left**, or be completed earlier in the development lifecycle. By moving steps from a final gate at deployment time to an earlier step, fewer mistakes are made, and developers can move more quickly.

Application-security concepts weren't a focus for developers in the past. Apart from the education and training issues, it's because their organizations emphasized fast development of features.

However, with the introduction of DevOps practices, security testing is easier to integrate into the pipeline. Rather than being a task performed by security specialists, security testing should just be part of the day-to-day delivery processes.

Overall, when the time for rework is taken into account, adding security to your DevOps practices earlier in the development lifecycle allows development teams to catch issues earlier. Catching issues earlier can actually reduce the overall time it takes to develop quality software.

Shifting left is a process change, but it isn’t a single control or specific tool. It’s about making all of your security more developer-centric and giving developers security feedback where they are.

##### Security tab features

GitHub offers security features that help keep data secure in repositories and across organizations. To locate the security tab:

1. On GitHub.com, go to the repository's main page.
    
2. Under the repository name, select **Security**.
    

![Screenshot showing where to locate the Security tab in GitHub.](https://learn.microsoft.com/en-gb/training/github/maintain-secure-repository-github/media/security-tab.png)

From the Security tab, you can add features to your GitHub workflow to help avoid vulnerabilities in your repository and codebase. These features include:

- **Security policies** that allow you to specify how to report a security vulnerability in your project by adding a `SECURITY.md` file to your repository.
- **Dependabot alerts** that notify you when GitHub detects that your repository is using a vulnerable dependency or malware.
- **Security advisories** that you can use to privately discuss, fix, and publish information about security vulnerabilities in your repository.
- **Code scanning** that helps you find, triage, and fix vulnerabilities and errors in your code.

For more information, see [GitHub security features](https://docs.github.com/code-security/getting-started/github-security-features).

Next, we explore some of these features and learn ways to distribute security and operational responsibilities across all phases of the software-development lifecycle.

#### Communicate a security policy with SECURITY.md

GitHub's community benefits are substantial, but they also carry potential risks. The fact that anyone can propose bug fixes publicly comes with certain responsibilities. The most important is the responsible disclosure of information that could lead to security exploits before their underlying bugs can be fixed. Developers looking to report or address security issues look for a `SECURITY.md` file in the root of a repository in order to responsibly disclose their concerns. Providing guidance in this file ultimately speeds up the resolution of these critical issues.

To learn more about `SECURITY.md`, see [Adding a security policy to your repository](https://docs.github.com/code-security/getting-started/adding-a-security-policy-to-your-repository).

#### GitHub Security Advisories

GitHub Security Advisories allow repository maintainers to privately discuss and fix a security vulnerability in a project. After repository maintainers collaborate on a fix, they can publish the security advisory to publicly disclose the security vulnerability to the project's community. By publishing security advisories, repository maintainers make it easier for their community to update package dependencies and research the consequences of the security vulnerabilities. GitHub stores the published advisories in the Common Vulnerabilities and Exposures (CVE) list. This list is used for automatically notifying affected repositories that use software that has a listed vulnerability. For more information, see [About repository security advisories](https://docs.github.com/code-security/security-advisories/working-with-repository-security-advisories/about-repository-security-advisories).

#### Keep sensitive files out of your repository with .gitignore

It's easy for developers to overlook files included in a commit. Sometimes these overlooked files are benign, such as intermediate build files. However, there's always the risk that someone might inadvertently commit sensitive data. For example, someone could commit an API key or private configuration data that a malicious actor could use. One technique to help avoid this risk is to build and maintain `.gitignore` files. These files instruct client tools, such as the `git` command line utility, to ignore paths and patterns when aggregating files for a commit.

The following sample illustrates some of the common use cases for ignoring files:

```gitignore
# User-specific files - Ignore all files ending in ".suo"
*.suo

# Mono auto generated files - Ignore all files starting with "mono_crash."
mono_crash.*

# Build results - Ignore all files in these folders found at any folder depth
[Dd]ebug/
[Rr]elease/
x64/
x86/

# Root config folder - Ignore this directory at the root due to leading slash
# Removing the slash would ignore "config" directories at all depths 
/config

# Ignore intermediate JS build files produced during TypeScript build at any 
# folder depth under /Web/TypeScript. This won't ignore JS files elsewhere. 
/Web/TypeScript/**/*.js
```

Your repository might include multiple `.gitignore` files. Settings are inherited from parent directories, with overriding fields in new `.gitignore` files taking precedence over parent settings for their folders and subfolders. It's significant effort to maintain the root `.gitignore` file, although adding a `.gitignore` file into a project directory can be helpful when that project has specific requirements that are easier to maintain separately from the parent, such as files that should _not_ be ignored.

To learn more about `.gitignore`, see [Ignoring files](https://docs.github.com/get-started/git-basics/ignoring-files). Also check out the collection of starter `.gitignore` files offered for various platforms in the [gitignore repository](https://github.com/github/gitignore).

#### Remove sensitive data from a repository

While `.gitignore` files can be useful in helping contributors avoid committing sensitive data, they're just a strong suggestion. Developers can still work around a `.gitignore` file to add files if they're motivated enough, and sometimes files might slip through because they don't meet the `.gitignore` file configuration. Project participants should always be on the lookout for commits that contain data that shouldn't be included in the repository or its history.

>**Important**: You should assume that any data committed to GitHub at any point has been compromised. Simply overwriting a commit isn't enough to ensure the data won't be accessible in the future. For the complete guide to removing sensitive data from GitHub, see [Removing sensitive data from a repository](https://docs.github.com/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository).

#### Branch protection rules

You can create a [branch protection rule](https://docs.github.com/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule) to enforce certain workflows for one or more branches. For example, you can require an approving review or passing status checks for all pull requests merged into the protected branch.

You can use the workflows that protect the branch to:

- Run a build to verify the code changes can be built;
- Run a linter to check for typos and conformation to the internal coding conventions;
- Run automated tests to check for any behavior changes of the code;
- And so on.

#### Add a CODEOWNERS file

By adding a [CODEOWNERS](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#codeowners-syntax) file to your repository, you can assign individual team members or entire teams as code owners to paths in your repository. These code owners are then required for pull-request reviews on any changes to files in a path for which they're configured.

```
# Changes to files with the js extensions need to be reviewed by the js-owner user/group:
*.js    @js-owner

# Changes to files in the builds folder need to be reviewed by the octocat user/group:
/build/ @octocat
```

You can create the CODEOWNERS file in either the root of the repository or in the `docs` or `.github` folder.
### Automated security

Here, we discuss some ways you can automate security checks in a repository that are available to GitHub repository administrators.

#### Detect and fix outdated dependencies with security vulnerabilities

Virtually every project these days takes dependencies on external packages. While these components can offer substantial benefits in productivity, they can introduce other security risks. Staying on top of these packages and their vulnerability status can be time consuming, especially given how each dependency might have its own dependencies that can become difficult to track and maintain. Fortunately, GitHub provides features that reduce this workload.

##### Repository dependency graphs

One default feature every repository includes is dependency graphs. GitHub scans common package manifests, such as `package.json`, `requirements.txt`, and others. These graphs allow project owners to recursively track all of the dependencies their project relies on.

![Screenshot of a GitHub dependency graph.](https://learn.microsoft.com/en-gb/training/github/maintain-secure-repository-github/media/2-dependency-graph.png)

For the list of supported dependency manifests, see [About the dependency graph](https://docs.github.com/code-security/supply-chain-security/understanding-your-software-supply-chain/about-the-dependency-graph).

##### Dependabot alerts

Even with a visual dependency graph, it can still be overwhelming to stay on top of the latest security considerations for every dependency a project has. To reduce this overhead, GitHub provides [Dependabot alerts](https://docs.github.com/code-security/dependabot/dependabot-alerts/about-dependabot-alerts) that watch your dependency graphs for you. It then cross-references target versions with versions on known vulnerability lists. When a risk is discovered, the project is alerted. Input for the analysis comes from [GitHub Security Advisories](https://docs.github.com/code-security/security-advisories/working-with-repository-security-advisories/about-repository-security-advisories#dependabot-alerts-for-published-security-advisories).

![Screenshot of Dependabot alerts for vulnerable dependencies.](https://learn.microsoft.com/en-gb/training/github/maintain-secure-repository-github/media/2-dependency-alert.png)

##### Automated dependency updates with Dependabot

A dependency alert can lead to a project contributor bumping the offending package reference to the recommended version and creating a pull request for validation. Wouldn't it be great if there was a way to automate this effort? Well, good news! **Dependabot** does just that. It scans for dependency alerts and creates pull requests so that a contributor can validate the update and merge the request.

To learn more about Dependabot's flexibility, see [Configuring Dependabot security updates](https://docs.github.com/code-security/dependabot/dependabot-security-updates/configuring-dependabot-security-updates).

##### Automated code scanning

Similar to how Dependabot scans your repository for dependency alerts, you can use code scanning to analyze and find security vulnerabilities and errors in the code in a GitHub repository. Code scanning has several benefits. You can use it to find, triage, and prioritize fixes for existing problems or potential security vulnerabilities. It's also useful to help prevent developers from introducing any new security problems into the code.

Another advantage to code scanning is its ability to use CodeQL. CodeQL lets you query code as data, which lets you create custom queries or use queries maintained by the open-source community. Code scanning gives you the freedom to customize and maintain how the code within your repository is being scanned.

You can enable code-scanning alerts and workflows in the security tab of a GitHub repository:

![Screenshot of a list of policies, advisories, and alerts with links to more information.](https://learn.microsoft.com/en-gb/training/github/maintain-secure-repository-github/media/security-overview.png)

Learn more about [Code scanning and CodeQL](https://docs.github.com/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning).

##### Secret scanning

Another automated scanning feature within a GitHub repository is secret scanning. Similar to the previous security scanning features, secret scanning looks for known secrets or credentials committed within the repository. This scanning is done to prevent the use of fraudulent behavior and to secure the integrity of any sensitive data. By default, secret scanning occurs on public repositories and you can enable secret scanning on private repositories by repository administrators or organization owners.

When secret scanning detects a set of credentials, GitHub notifies the service provider who issued the secret. The service provider validates the credential. Then, it decides whether they should revoke the secret, issue a new secret, or reach out to you directly. The action depends on the associated risks to you or the service provider.

Learn more about [Secret scanning for public and private repositories](https://docs.github.com/code-security/secret-scanning/introduction/about-secret-scanning).

## Introduction to GitHub administration
### Introduction

GitHub administrators work to protect their organization's code and content assets while providing each team access to the repositories they rely on to collaborate and share their work.

Imagine that your CIO (Chief Information Officer) asks you for an adoption plan to help the entire company benefit from GitHub. You want to ensure every group has adequate access to the right repositories and that there's a sustainable way to provide adequate permissions to the appropriate software development and content teams. You'll need to think through the kinds of tasks that administrators need to perform and assign them the right level of access. But first, you really need to understand what options are available to you from GitHub.
### What is GitHub administration?

As a GitHub administrator, your goal is to keep everything working smoothly for your users. In this unit, you learn about the different levels in the GitHub organizational hierarchy and the administration tasks associated with each level.

#### Administration at team level

![Screenshot of the organization screen with the Teams tab highlighted.](https://learn.microsoft.com/en-gb/training/github/github-introduction-administration/media/teams.png)

In GitHub, each user is an organization member that you can add to a team. You can create teams in your organization with cascading access permissions and mentions reflecting your company or group's structure. A team is a useful substructure for refining repository permissions on a more granular level and enabling communication and notification between team members.

Additionally, GitHub allows you to sync your teams with identity provider (IdP) groups such as Microsoft Entra ID. When you synchronize a GitHub team with Microsoft Entra ID, you can replicate changes to GitHub automatically. This sync reduces the need for manual updates and custom scripts. You can use Microsoft Entra ID with team synchronization to manage administrative tasks such as onboarding new members, granting new permissions, and removing member access to the organization.

Members of a team with _team maintainer_ or repository _admin_ permissions can:

- Create a new team and select or change the parent team.
- Delete or rename a team.
- Add or remove organization members from a team, or synchronize a GitHub team's membership with an IdP group.
- Add or remove outside collaborators (people who aren't explicitly members of your organization, such as consultants or temporary employees) from team repositories.
- Enable or disable team discussions on the team's page.
- Change the visibility of the team within the organization.
- Manage automatic code review assignment for pull requests, utilizing GitHub's review assignment routing algorithm.
- Schedule reminders.
- Set the team profile picture.

##### Best practices for team-level administration

Creating teams in your organization enables greater flexibility for collaboration and can make it easier to separate repositories and permissions. The following are some best practices for setting up teams on GitHub:

- Create nested teams to reflect your group or company's hierarchy within your GitHub organization.
- Help streamline PR review processes by creating teams based on interests or specific technology (JavaScript, data science, etc.). Individuals can choose to join these teams according to their interests or skills.
- Enable team synchronization between your IdP and GitHub to allow organization owners and team maintainers to connect teams in your organization with IdP groups. When you synchronize a GitHub team with an IdP group, you can replicate changes to GitHub automatically, reducing the need for manual updates and custom scripts. You can use an IdP with team synchronization to manage administrative tasks such as onboarding new members, granting new permissions, and removing member access to the organization.

#### Administration at organization level

In GitHub, organizations are shared spaces enabling users to collaborate across many projects at once. Owners and administrators can manage member access to the organization's data and repositories with sophisticated security and administrative features.

Members of an organization with the _owner_ permission can perform a wide range of activities at the organization level including:

- Invite users to join the organization, and remove members from the organization.
- Organize users into a team, and grant _team maintainer_ permissions to organization members.
- Add or remove outside collaborators (people who aren't explicitly members of your organization, such as consultants or temporary employees) to organizational repositories.
- Grant repository permission levels to members, and set the base (default) permission level for a given repository.
- Set up organization security.
- Set up billing or assign a billing manager for the organization.
- Extract various types of information about repositories via the use of custom scripts.
- Apply organization-wide changes such as migrations via the use of custom scripts.

We recommend setting up only one organization for your users and repositories. If specific constraints in your company require you to create multiple organizations, you should be aware of the following points:

- Duplicating an organization or sharing configurations between two organizations isn't possible. This means that you must set up everything from scratch every time you create an organization, which increases the risk of errors in your settings.
- Depending on your software providers' policies, you might incur extra costs if you need to install some applications in multiple organizations.
- Managing multiple organizations is more difficult!

#### Administration at enterprise level

Enterprise accounts include GitHub Enterprise Cloud and Enterprise Server instances and enable owners to centrally manage policy and billing for multiple organizations.

At the enterprise level, members of an enterprise with the _owner_ permissions can:

- Enable security assertion markup language (SAML) single sign-on for their enterprise account, allowing each enterprise member to link their external identity on your IdP to their existing GitHub account.
- Add or remove organizations from the enterprise.
- Set up billing or assign a billing manager for all organizations in the enterprise.
- Set up repository management policies, project board policies, team policies, and other security settings that apply to all the organizations, repositories, and members in the enterprise.
- Extract various types of information about organizations via the use of custom scripts.
- Apply enterprise-wide changes such as migrations via the use of custom scripts.

### How does GitHub authentication work?

In the previous unit, you learned about typical administration tasks at the team, organization, and enterprise level. In this unit, you'll deep dive into one of the most common administrative tasks performed by organization owners, which is setting up and controlling users' authentication to GitHub.

#### GitHub's authentication options

There are several options for authenticating with GitHub:

##### Username and password

Administrators can allow users to continue using the default username and password authentication method, sometimes known as the "basic" HTTP authentication scheme. In recent years, basic authentication has proven to be too risky when dealing with highly sensitive information. We strongly recommend using one (or several) of the other options listed in this unit.

##### Personal access tokens

![Screenshot of the personal access token screen.](https://learn.microsoft.com/en-gb/training/github/github-introduction-administration/media/personal-access-token.png)

Personal access tokens (PATs) are an alternative to using passwords for authentication to GitHub when using the GitHub API or the command line. Users generate a token via the GitHub's settings option, and tie the token permissions to a repository or organization. When users interact with GitHub by using the git command-line tool, they can enter the token information when they're asked for their username and password.

##### SSH keys

As an alternative to using personal access tokens, users can connect and authenticate to remote servers and services via SSH with the help of SSH keys. SSH keys eliminate the need for users to supply their username and personal access token for every interaction.

When setting up SSH, users generate an SSH key, add it to the ssh-agent, and then add the key to their GitHub account. Adding the SSH key to the ssh-agent ensures that the SSH key has a passphrase as an extra layer of security. Users can configure their local copy of git to automatically supply the passphrase, or they can supply it manually each time they use the git command-line tool to interact with GitHub.

You can even use SSH keys with a repository owned by an organization that uses SAML single sign-on (SSO). If the organization provides SSH certificates, users can also use it to access the organization's repositories without adding the certificate to their GitHub account.

##### Deploy keys

Deploy keys are another type of SSH key in GitHub that grants a user access to a single repository. GitHub attaches the public part of the key directly to the repository instead of a personal user account, and the private part of the key remains on the user's server. Deploy keys are read-only by default, but you can give them write access when adding them to a repository.

#### GitHub's added security options

GitHub also offers the following extra security options.

##### Two-factor authentication

![Screenshot of the two-factor authentication screen.](https://learn.microsoft.com/en-gb/training/github/github-introduction-administration/media/2-factor-authentication.png)

Two-factor authentication (2FA), sometimes known as multifactor authentication (MFA), is an extra layer of security used when logging into websites or apps. With 2FA, users have to sign in with their username and password and provide another form of authentication that only they have access to.

For GitHub, the second form of authentication is a code generated by an application on a user's mobile device or sent as a text message (SMS). After a user enables 2FA, GitHub generates an authentication code anytime someone attempts to sign into their GitHub account. Users can only sign into their account if they know their password and have access to the authentication code on their phone.

Organization owners can require organization members, outside collaborators, and billing managers to enable 2FA for their personal accounts. This action makes it harder for malicious actors to access an organization's repositories and settings.

Enterprise owners can also enforce certain security policies for all organizations owned by an enterprise account.

##### SAML SSO

If you centrally manage your users' identities and applications with an IdP, you can configure SAML SSO to protect your organization's resources on GitHub.

This type of authentication gives organization and enterprise owners on GitHub a way to control and secure access to organization resources like repositories, issues, and pull requests. Organization owners can invite GitHub users to join the organization that uses SAML SSO, which allows those users to contribute to the organization and retain their existing identity and contributions on GitHub.

When users access resources within an organization that uses SAML SSO, GitHub will redirect them to the organization's SAML IdP for authentication. After they successfully authenticate with their account on the IdP, the IdP redirects to GitHub to access the organization's resources.

GitHub offers limited support for all identity providers that implement the SAML 2.0 standard with official support for several popular identity providers including:

- Active Directory Federation Services (AD FS).
- Microsoft Entra ID.
- Okta.
- OneLogin.
- PingOne.

##### LDAP

Lightweight directory access protocol (LDAP) is a popular application protocol for accessing and maintaining directory information services. LDAP lets you authenticate GitHub Enterprise Server against your existing accounts and centrally manage repository access. It's one of the most common protocols used to integrate third-party software with large company user directories.

GitHub Enterprise Server integrates with popular LDAP services like:

- Active Directory.
- Oracle Directory Server Enterprise Edition.
- OpenLDAP.
- Open Directory.

### How does GitHub organization and permissions work?

#### Repository permission levels

You can customize access to a given repository by assigning permissions. There are five repository-level permissions:

- **Read**: Recommended for non-code contributors who want to view or discuss your project. This level is good for anyone that needs to view the content within the repository but doesn't need to actually make contributions or changes.
- **Triage**: Recommended for contributors who need to proactively manage issues and pull requests without write access. This level could be good for some project managers who manage tracking issues but don't make any changes.
- **Write**: Recommended for contributors who actively push to your project. Write is the standard permission for most developers.
- **Maintain**: Recommended for project managers who need to manage the repository without access to sensitive or destructive actions.
- **Admin**: Recommended for people who need full access to the project, including sensitive and destructive actions like managing security or deleting a repository. These people are repository owners and administrators.

You can give organization members, outside collaborators, and teams different levels of access to repositories owned by an organization. Each permission level progressively increases access to a repository's content and settings. Choose the level that best fits each person or team's role in your project without giving more access to the project than necessary.

After you create a repository with the correct permissions, you can make it a template so that anyone who has access to the repository can generate a new repository that has the same directory structure and files as your default branch. To make a template:

1. On GitHub.com, go to the main page of the repository.
    
2. Under the repository name, select **Settings**. If you can't see the **Settings** tab, open the dropdown menu, and then select **Settings**.
    
    ![Screenshot showing where to locate the settings button in your GitHub repository.](https://learn.microsoft.com/en-gb/training/github/github-introduction-administration/media/repository-actions-settings.png)
    
3. Select **Template repository**.
    

#### Ways Users Receive Repository Access

##### Actions of a User Given a List of Their Repository Permissions

A user’s effective permissions in a repository are influenced by various factors, including:

- **Repository Role:** (e.g., Admin, Write, Read)
- **Team Membership:** (e.g., inherited permissions from a team)
- **Organization Membership:** (e.g., default organization permissions, SSO requirements)

When you combine these different permission sources, GitHub applies the highest level of access granted to the user. For example, if a user has Read access through a team but also has Write access directly assigned as a collaborator, they will effectively have Write permissions.

##### Repository Membership Options

When granting access to a repository, there are several ways a user can become a collaborator:

|Membership Type|Description|
|---|---|
|**Direct Collaborator**|Added explicitly to the repository with a specific role (Read, Triage, Write, Maintain, or Admin).  <br>Recommended for external contributors or small teams.|
|**Team Membership**|A user inherits repository access via their team membership.  <br>Team permissions are often set at the organization level for consistent, scalable management.|
|**Organization Default Permissions**|If the repository is part of an organization, there may be a default permission level for all organization members (e.g., None, Read).  <br>Owners can override these defaults for specific teams or users.|
|**Outside Collaborator**|A user who is not a member of the organization but has explicit access to a repository.  <br>Useful for contractors, freelancers, or open-source contributors needing limited access.|

#### Monitoring and Auditing Repository Access

Regularly auditing who has access to a repository ensures proper security and compliance. Here are some recommended steps and tools:

- **View Access in Repository Settings:**
    
    - Navigate to Settings > Manage access (for the repository).
    - Review the list of users and teams, along with their permission levels.
- **Organization Audit Log (GitHub Enterprise or Organization-level):**
    
    - Organization owners can view changes to membership, repository access, and permissions in the Audit log.
    - Filter events by repository name or access changes for a more focused view.
- **Enterprise Audit Log (GitHub Enterprise):**
    
    - If you manage multiple organizations, use the Enterprise account’s audit log to track changes across all organizations and repositories.
    - This is especially valuable for compliance reporting or large-scale security reviews.
- **Automated Scripting:**
    
    - Use the GitHub REST API or GraphQL API to programmatically list collaborators, teams, and permissions.
    - Integrate scripts with your CI/CD pipeline or security dashboards to continuously monitor and flag anomalies.

**Tip:** Set up branch protection rules and required reviews to add another layer of security and accountability for all code changes.

#### Team permission levels

A team in a GitHub organization is a group of users who collaborate on shared repositories. Teams help streamline access management and communication by applying consistent permissions across multiple repositories at once. Key benefits include:

- **Centralized Access Control:** Assign repository permissions (e.g., Read, Write) to the entire team instead of managing each user individually.
- **Structured Collaboration:** Organize members by department, project, or role for more efficient collaboration.
- **Visibility & Communication:** Each team can have its own discussion board, making it easier to share updates and coordinate efforts.

Teams provide an easy way to assign repository permissions to several related users at once. Members of a child team also inherit the permission settings of the parent team, providing an easy way to cascade permissions based on the natural structure of a company.

There are two levels of permissions at the team level:

|**Permission level**|**Description**|
|---|---|
|Member|Team members have the same set of abilities as organization members|
|Maintainer|Team maintainers can do everything team members can, plus:  <br>- Change the team's name, description, and visibility.  <br>- Request that the team change parent and child teams.  <br>- Set the team profile picture.  <br>- Edit and delete team discussions.  <br>- Add and remove organization members from the team.  <br>- Promote team members to also have the team maintainer permission.  <br>- Remove the team's access to repositories.  <br>- Manage code review assignment for the team.  <br>- Manage scheduled reminders for pull requests.|

An organization owner can also promote any member of the organization to be a maintainer for a team.

To audit access to a repository that you administer, you can view a combined list of teams and users with access to your repository in your settings:

![Screenshot of the manage access screen.](https://learn.microsoft.com/en-gb/training/github/github-introduction-administration/media/manage-access-overview.png)

GitHub offers several permission levels that can be assigned to teams. When you grant a team access to a repository, you can choose from the following permission models:

##### Permission Models

|Permission Level|Description|Best For|
|---|---|---|
|**Read**|Users can view and clone the repository. Can open and comment on issues and pull requests.|Individuals who need read-only or review access.|
|**Triage**|Users can manage issues and pull requests (e.g., label, assign, comment). Cannot push changes to the repository.|Project managers or contributors who need to triage and organize issues without contributing code.|
|**Write**|Users can push to branches (except protected branches). Can manage issues and pull requests.|Active contributors who need to commit code or update documentation.|
|**Maintain**|Users can manage repository settings, issues, and pull requests. Cannot delete or transfer the repository.|Project maintainers who handle routine repository management but don’t require full admin rights.|
|**Admin**|Users have full control over the repository, including setting permissions, deleting the repository, and managing all settings.|Those who need top-level administrative access.|

**Tip:** Always follow the Principle of Least Privilege—assign the lowest permission level necessary for each team to perform its tasks effectively. This approach reduces the risk of accidental or unauthorized changes.
### Managing enterprise access, permissions, and governance

#### Organization permission levels

GitHub organizations provide a centralized way for teams to collaborate on projects while maintaining controlled access to repositories and sensitive data. Organization permissions determine what members and teams can do within the organization, ensuring that each user has the appropriate level of access.

There are multiple levels of permissions at the organizational level:

|**Permission level**|**Description**|
|---|---|
|Owner|Organization owners can do everything that organization members can do, and they can add or remove other users to and from the organization. This role should be limited to no less than two people in your organization.|
|Member|Organization members can create and manage organization repositories and teams.|
|Moderator|Organization moderators can block and unblock nonmember contributors, set interaction limits, and hide comments in public repositories that the organization owns.|
|Billing manager|Organization billing managers can view and edit billing information.|
|Security managers|Organization security managers can manage security alerts and settings across your organization. They can also read permissions for all repositories in the organization.|
|Outside collaborator|Outside collaborators, such as a consultant or temporary employee, can access one or more organization repositories. They aren't explicit members of the organization.|

In addition to these levels, you can also set default permissions for all members of your organization:

![Screenshot of the member privileges screen with the base permissions dropdown displayed.](https://learn.microsoft.com/en-gb/training/github/github-introduction-administration/media/org-base-permissions.png)

For improved management and security, you might also consider giving default read permissions to all members of your organization and adjusting their access to repositories on a case-by-case basis. If you have a relatively small organization with a low number of users, a low number of repositories, or a combination of the two, this level of restriction might be unnecessary. If you trust everyone with pushing changes to any repository, you might prefer to give all members write permissions by default.

#### Enterprise permission levels

Recall from earlier that enterprise accounts are collections of organizations. By extension, each individual user account that is a member of an organization is also a member of the enterprise. You can control various settings related to authentication from this higher level.

There are three levels of permission at the enterprise level:

|**Permission level**|**Description**|
|---|---|
|Owner|Enterprise owners have complete control over the enterprise and can take every action, including:  <br>- Managing administrators.  <br>- Adding and removing organizations to and from the enterprise.  <br>- Managing enterprise settings.  <br>- Enforcing policies across organizations.  <br>- Managing billing settings.|
|Member|Enterprise members have the same set of abilities as organization members.|
|Billing manager|Enterprise billing managers can only view and edit your enterprise's billing information and add or remove other billing managers.|
|Guest collaborator|Can be granted access to repositories or organizations, but has limited access by default (Enterprise Managed Users only)|

In addition to these three levels, you can also set a policy of default repository permissions across all your organizations:

![Screenshot of the policies screen with the default permissions dropdown displayed.](https://learn.microsoft.com/en-gb/training/github/github-introduction-administration/media/enterprise-base-permissions.png)

For improved management and security, you can give default read permissions to all members of your enterprise and adjust their access to repositories on a case-by-case basis. In a smaller enterprise, such as one with a single, relatively small organization, you might prefer to trust all members with write permissions by default.

To further streamline enterprise-scale access control:

- **Nested Teams:** Enterprise accounts can use nested team structures to reflect departmental hierarchies. A parent team’s permissions cascade down to child teams, simplifying complex access management.
- **Automation & Auditing:** You can use GitHub’s API or GitHub Actions to automate team creation and permission assignments, and audit access via organization or enterprise audit logs.

#### Enterprise Permissions and Policies via Ruleset

This section covers how to manage enterprise permissions and policies through rulesets. We'll explore best practices for structuring organizations, setting default permissions, synchronizing teams via Active Directory (AD), automating multi-org scripting, and aligning policies with your company’s trust and control positions.

##### Weighing the pros and cons of deploying a single versus multiple organizations

When structuring your enterprise, one of the key decisions is whether to use a single organization or multiple organizations. Each approach has unique benefits and trade-offs.

###### Single Organization

|Pros|Cons|
|---|---|
|**Simplified Management:** Centralized control of permissions and policies.|**Limited Flexibility:** One-size-fits-all policies might not suit all teams.|
|**Consistency:** Uniform application of rules and streamlined collaboration.|**Security Risks:** A single breach could impact the entire organization.|
|**Resource Sharing:** Easier asset sharing across teams.|**Scalability Issues:** Managing permissions can become complex as the organization grows.|
|**Cost Efficiency:** Reduced overhead in administrative tooling and licensing.||

###### Multiple Organizations

|Pros|Cons|
|---|---|
|**Tailored Policies:** Customize permissions to fit the specific needs of each team.|**Increased Complexity:** More organizations mean more administrative overhead.|
|**Enhanced Isolation:** Limits the impact of a security breach to a single organization.|**Redundancy:** Potential duplication of settings and management efforts.|
|**Decentralized Administration:** Teams can manage their own policies and permissions.|**Inter-Org Collaboration:** May require extra tools or processes for cross-organization projects.|

##### Setting default read versus default write across organizations

Deciding on the default permission level is critical to balancing security and collaboration within your enterprise.

###### Default Read vs Default Write

|Default Read|Default Write|
|---|---|
|**Enhanced Security:** Minimizes the risk of unintended modifications.|**Improved Collaboration:** Empowers users to contribute and modify content directly.|
|**Control:** Easier to audit and monitor changes.|**Efficiency:** Reduces bottlenecks in content creation and updates.|
|**Best For:** Environments where the majority of users only need to view resources.|**Risks:** Increases the chance of accidental changes or misconfigurations if not carefully managed.|

**Recommendation:**  
Use a default read permission model and grant write access selectively, ensuring adherence to the principle of least privilege.

##### Team synchronization through Active Directory (AD)

Using Active Directory (AD) for team synchronization makes user management and access control easier and more efficient.

###### Why use AD sync?

- **Single source of truth:** Keeps user identities consistent across your organization.
- **Automated access management:** Streamlines onboarding, offboarding, and role updates.
- **Seamless role alignment:** Ensures AD groups match enterprise roles and permissions.

###### Things to consider before implementing

- **Role mapping:** Clearly define how AD groups align with your organization's roles.
- **Sync frequency:** Set a schedule that balances performance and security.
- **Compliance & auditing:** Log all changes to meet compliance requirements.

By planning ahead, you can ensure a smooth integration that keeps your organization secure and well-organized.

##### Maintainability: scripting for multiple organizations and access rights

As your enterprise scales, automating the management of permissions across multiple organizations is essential for maintainability.

###### Key Practices:

Automating the management of permissions across multiple organizations is crucial for maintaining efficiency and security as your enterprise grows. This section provides key practices for scripting and automation to ensure consistent and scalable permission management. By following these practices, you can streamline administrative tasks, reduce manual errors, and maintain a secure and well-organized environment.

- **Modularity:** Develop scripts in modular components to handle different organizations with minimal changes.
- **Reusability:** Create reusable functions or modules to perform common permission tasks.
- **Testing:** Thoroughly test scripts in a controlled environment before deployment.
- **Logging:** Implement detailed logging to track changes and facilitate troubleshooting.
- **Version Control:** Use version control systems (like Git) to manage script revisions and collaborate with team members.

## Authenticate and authorize user identities on GitHub
### Introduction

User authentication has traditionally been achieved using a User ID and password. A password is a single-factor form of authentication. The fundamental issue with single-factor authentication is that it's easier for any bad actor with knowledge of the sign-on information to impersonate the valid user. To prevent a breach of security for a user account, GitHub has authentication tools available to promote security best practices. You can even enforce a security policy for all GitHub users within the organization.

Controlling access to your company's data is foundational for a secure GitHub Enterprise. GitHub is committed to helping enterprises on their security journey with authentication methods to allow for more secure account access and a better user experience. In a GitHub Enterprise, most organizations want to require extra levels of authentication for better security. Enterprise System Administrators can enforce authentication and authorization security policies across an organization. These security features allow you to ensure that users are required to sign on securely to access the correct permissions in repositories. These features also include access and tools for auditing user access and activity, identity maintenance, and authentication compliance. As an administrator, you should work with your internal resources to identify what type of authentication and authorization is appropriate. 
### User identity and access management

Authentication is the gateway to your enterprise's software development ecosystem. Every user's interaction with GitHub begins with identity verification. While individual accounts can rely on usernames and passwords, strong enterprise security mandates **two-factor authentication (2FA)** or more advanced methods like **passkeys** and **biometric login**. Balancing usability with security is key—especially in a fast-paced development environment.

#### Modern Authentication in GitHub Enterprise

To ensure a secure and streamlined authentication experience, GitHub supports multiple modern methods that integrate with your identity management systems:

##### Passkeys and WebAuthn

- **Passkeys** are a passwordless login method, tied to a physical device, and resistant to phishing.
- **WebAuthn** supports biometric factors and hardware tokens like YubiKey.
- These methods significantly reduce credential-based attacks and improve login UX.

##### GitHub Mobile for 2FA

Users can authenticate with **GitHub Mobile**, which supports push notifications for quick, secure approval—enhancing 2FA without disrupting workflows.

##### OAuth and GitHub Apps

- **OAuth Apps** use GitHub's OAuth 2.0 flow to authenticate users and grant scoped access to external applications.
- **GitHub Apps** authenticate as individual installations with fine-grained permissions and are ideal for CI/CD and automation pipelines.

##### Enterprise Managed Users (EMU)

In **GitHub Enterprise Cloud**, EMUs ensure that authentication happens strictly through your **Identity Provider (IdP)**. This model:

- Restricts access to enterprise-managed accounts only.
- Enforces centralized control over identity, credentials, and session policies.

#### Organization Management with SAML SSO

One foundational capability for enterprise-grade authentication is **SAML Single Sign-On (SSO)**. SAML links your IdP with GitHub, enabling users to sign in across services using one set of credentials. GitHub uses the IdP to verify user identity before granting access to organization or enterprise resources.

When users log into GitHub, they can see the enterprises they belong to—but access to repository data requires SAML reauthentication via the IdP.

As an **Enterprise Admin**, your responsibilities include:

- Authorizing access based on role and need-to-know.
- Monitoring and auditing user activity.
- Scoping permissions and minimizing surface area for attacks.

![Screenshot of an example of admin repository permission list review.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/repository-permission-list-example.png)

To configure SAML SSO for your organization, integrate your IdP with GitHub. Supported providers include:

- Active Directory Federation Services (AD FS)
- Microsoft Entra ID
- Okta
- OneLogin
- PingOne
- Shibboleth

>**Note**: GitHub provides limited support for identity providers that implement the SAML 2.0 standard.

#### Enterprise Access and Authorization Controls

Access in GitHub is governed by a robust, multi-layered authorization model:

##### Fine-Grained Personal Access Tokens (PATs)

Unlike classic PATs, **fine-grained PATs**:

- Restrict access to specific repositories and scopes.
- Support automatic expiration for reduced risk exposure.
- Offer enhanced traceability and compliance controls.

##### Custom Repository Roles

Admins can define **custom roles** that extend beyond the default permission sets. This supports:

- Delegated access tailored to unique workflows.
- Least-privilege enforcement for sensitive repositories.

##### Security Policy Enforcement

You can enforce global security controls such as:

- Mandatory **2FA** for all users.
- **IP allowlists** to restrict access to approved networks.
- Blocking unverified OAuth apps unless explicitly approved.

##### Organizational and Enterprise-Level Controls

- **Organization-level** controls include default roles, team-based access, and the management of external collaborators.
- **Enterprise-level** governance includes:
    - Centralized SAML enforcement.
    - IdP-based login restrictions.
    - Global policy enforcement via **GitHub Enterprise Cloud**.

#### Repository Visibility and Internal Access

When organization members create repositories, they can choose among **public**, **private**, or **internal** visibility options:

- **Public**: Available to anyone on the internet.
- **Private**: Restricted to selected users.
- **Internal**: Visible to all members within the enterprise but hidden from external users.

This granularity ensures that source code, documentation, and other assets are only shared with appropriate stakeholders.
### User authentication

When it comes to user authentication, security should be the number one consideration that comes to mind. Strong security is essential. It seems like every month or so, a company reports a data breach. Credentials are stolen because of inefficient security processes, or simply because of a lack of up-to-date security features within the company. Establishing secure user authentication can be a difficult task if user adoption requires long and frustrating steps to authenticate.

GitHub Enterprise supports two recommended methods for secure user authentication:

- **SAML Single Sign-On(SSO)**
- **Two-Factor Authentication(2FA)**

#### SAML SSO Authentication

SAML(Security Assertion Markup Language) SSO integrates GitHub with your organization’s identity provider (IdP), allowing centralized access control, and improved compliance. When enabled, GitHub redirects users to the IdP for authentication before granting access to organization resources.

##### Enabling and Enforcing SAML SSO

You can configure SAML SSO at either the **organization** or **enterprise** level, depending on the scope of enforcement you require.

###### Organization-Level SAML SSO

- **Setup**: In your org settings under **Security**, input your IdP’s SAML SSO URL and public certificate. Test and save the configuration.
- **Enforcement**: Select **Require SAML SSO authentication** to remove noncompliant members automatically.
- **Use Case**: Ideal for phased rollouts or testing with limited impact.

>**Note**: GitHub removes only organization members who fail to authenticate. Enterprise members remain until they next access the resource.

###### Enterprise-Level SAML SSO

- **Setup**: In your enterprise account settings, enable SAML SSO similarly to org-level.
- **Enforcement**: Apply SSO across all organizations in your enterprise.
- **Benefits**: Ensures unified policies and reduces risk from fragmented configurations.
- **Note**: GitHub does **not** immediately remove noncompliant enterprise members. They are prompted to authenticate upon access.

##### Choosing the Right SSO Scope

|Criteria|Org-Level|Enterprise-Level|
|---|---|---|
|**Scope**|Individual organization|Entire enterprise|
|**User Removal**|Immediate upon enforcement|Deferred until next access|
|**Policy Consistency**|Varies by org|Unified across enterprise|
|**Setup Complexity**|Lower|Higher|
|**Use Case**|Pilot/test|Broad compliance|

##### Step-by-Step: Enabling and Enforcing SAML SSO

|Scope|Steps|
|---|---|
|**Organization**|1. Navigate to **Your organizations** → **Settings** → **Security**.  <br>2. Enable SAML with your IdP’s details.  <br>3. Test configuration and save.  <br>4. Select **Require SAML SSO**, then remove noncompliant users.|
|**Enterprise**|1. Navigate to **Your enterprises** → **Settings** → **Security**.  <br>2. Enable SAML with your IdP’s details.  <br>3. Test configuration and save.  <br>4. Enforce SSO across all orgs and review noncompliant users.|

![Screenshot of the setting to require SSO authentication for all members of an organization.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/require-saml-sso-authentication.png)

#### Two-Factor Authentication (2FA)

2FA adds a second verification step beyond username and password. You can require 2FA for organization members, outside collaborators, and billing managers.

>**Warning**: When you require the use of two-factor authentication for your organization, all accounts that don't use 2FA is removed from the organization and lose access to its repositories. Accounts that are affected include bot accounts.

For more detailed information about 2FA, see [Securing your account with two-factor authentication (2FA)](https://docs.github.com/authentication/securing-your-account-with-two-factor-authentication-2fa).

##### Enforcing 2FA

- Navigate to your org’s **Security** settings.
- Enable the checkbox labeled **Require two-factor authentication**.
- Communicate the requirement in advance to prevent loss of access.

![Screenshot of the checkbox requiring two-factor authentication for members in the organization.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/require-2fa-checkbox.png)

##### 2FA Methods in GitHub

|Method|Description|
|---|---|
|**Security Keys**|Most secure method. Physical USB or NFC devices that prevent phishing. Requires prior setup with TOTP(Time-based one-time passwords) or SMS(Short Message Service).|
|**TOTP Apps**|Recommended. Generates time-based one-time passwords, supports backup, and works offline.|
|**SMS**|Least secure. Should only be used where TOTP isn't viable. GitHub SMS support varies by region.|

###### Time-based one-time passwords

![Screenshot of the time-based one-time password code.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/two-factor-identification-totp-example.png)

###### GitHub SMS support

![Screenshot of the SMS code.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/two-factor-authentication-sms-six-digit-code-example.png)

>**Note**: Security keys store credentials locally and never expose secrets. GitHub recommends FIDO2/U2F keys.

##### Auditing 2FA Compliance

To review who has enabled 2FA:

1. Go to **Your organizations** → select org → **People** tab.
2. Select the **2FA** filter.

From here, you can identify noncompliant users and follow up outside of GitHub, typically via email.

![Screenshot of the account-security setting.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/two-factor-authentication-enabled-example.png)
### User authorization

After a user successfully authenticates through your identity provider (IdP) by using SAML single sign-on (SSO), the next critical step is authorization—granting tools like personal access tokens (PATs), SSH keys, or OAuth apps with the ability to access organization resources.

#### Automating User Authorization with SAML SSO and SCIM

Security assertion markup language (SAML) SSO enables enterprise and organization owners to control access to GitHub resources like repositories, issues, and pull requests. Integrating SCIM (System for Cross-domain Identity Management) enhances access control by automating user provisioning and deprovisioning.

![Screenshot of the SCIM setting.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/enable-scim-user-provisioning-example.png)

With SCIM, new employees added to your IdP are granted access to GitHub automatically, while departing users are removed, reducing manual steps and improving security.

>**Note**: Without SCIM, SAML SSO alone doesn't support automatic deprovisioning of organization members.

SCIM also revokes stale tokens after a session ends, reducing security risks. Without SCIM, revoking stale tokens must be done manually.

#### Managing SSH Keys and PATs with SAML SSO

SAML SSO and SCIM work together to reflect identity changes in GitHub. To support this cohesion:

- `NameID` and `userName` must match between the SAML IdP and SCIM client.
- Group changes in your IdP trigger SCIM updates in GitHub.

Users accessing APIs or Git must use an authorized PAT or SSH key. These methods are auditable and securely tied to SAML SSO.

![Screenshot of the SSH key.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/saml-sso-ssh-key-example.png)

To simplify onboarding, provision users using: `https://github.com/orgs/ORGANIZATION/sso/sign_up`. Display this link in your IdP dashboard.

When users first authenticate, GitHub links their account and SCIM data to your organization. Admins can later audit or revoke sessions and credentials to automate offboarding.

#### SCIM Integration with GitHub

SCIM streamlines identity management in GitHub Enterprise Cloud by supporting both native integrations and custom configurations.

##### Supported SCIM Providers

GitHub natively supports:

- Okta
- Microsoft Entra ID
- OneLogin
- Ping Identity
- Google Workspace

These integrations ensure reliable configuration and compatibility.

##### Custom SCIM Integrations

If your IdP isn't natively supported, use GitHub’s SCIM API to build custom integrations.

###### SCIM API Overview

The SCIM 2.0 API allows you to:

- Create, update, and delete users
- Manage groups

###### Example Request to Provision a User

```http
POST /scim/v2/Users
Content-Type: application/json

{
  "userName": "jdoe",
  "name": {
    "givenName": "John",
    "familyName": "Doe"
  },
  "emails": [
    {
      "value": "jdoe@example.com",
      "primary": true
    }
  ]
}
```

GitHub processes this request and adds the user to your organization.

##### Getting Started

###### For Supported Providers

1. Sign in to your IdP admin console.
2. Enable SCIM provisioning.
3. Provide GitHub’s SCIM base URL and bearer token.

![Screenshot of SCIM configuration steps in IdP's administrative console.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/scim-configuration-steps.png)

###### For Custom IdPs

1. Use GitHub's SCIM REST API.
2. Authenticate with a PAT.
3. Test the integration with sample requests.

##### Key Benefits of SCIM Integration

- **Provisioning:** Automatically create accounts.
- **Updates:** Synchronize roles and departments.
- **Deprovisioning:** Remove access promptly upon user exit.

#### SCIM vs. Manual User Management

|Aspect|SCIM-Based Management|Manual Management|
|---|---|---|
|**Automation**|Automates provisioning and deprovisioning|Manual intervention required|
|**Consistency**|Standardized user data across systems|Risk of inconsistencies|
|**Security**|Timely deactivation of access|Delayed or missed revocations|
|**Scalability**|Scales with large user bases|Cumbersome at scale|
|**Compliance**|Helps meet policy and audit requirements|Harder to track and report|

#### Connecting Your IdP to GitHub

You can use a supported identity provider or bring your own SAML 2.0 IdP.

##### Supported (Paved Path) IdPs

- Okta
- Microsoft Entra ID
- Google Workspace

Some advantages of using the supported IdPs are:

- Seamless integration
- GitHub-supported
- Lower setup effort

##### Bring Your Own IdP

Bring your own IdP requires SAML 2.0 support. It has the advantage of allowing for full flexibility.

##### Integration Steps

|Type|Steps|
|---|---|
|**Paved Path:**|1. Navigate to enterprise security settings.  <br>2. Select your IdP.  <br>3. Follow setup instructions.|
|**Custom IdP:**|1. Go to security settings.  <br>2. Choose custom IdP.  <br>3. Enter SAML metadata. 4. Validate the connection.|

#### Comparing IdP Integration Paths

|Feature|Paved Path|Bring Your Own IdP|
|---|---|---|
|Setup Process|✅ Guided setup|⚠️ Manual configuration|
|Flexibility|⚠️ Limited to listed IdPs|✅ Any SAML 2.0 IdP|
|Maintenance|✅ GitHub-managed|⚠️ Organization-managed|
|Customization|⚠️ Minimal|✅ Fully customizable|
|Support & Updates|✅ GitHub-supported|⚠️ Self-managed|

#### Managing Identities and Access

##### SAML SSO Configuration

1. Configure your SAML SSO URL.
2. Provide your public certificate.
3. Add IdP metadata.

##### Credential Management

PATs and SSH keys must be explicitly authorized and linked to IdP identities to access organization resources securely.

##### Auditing SAML Sessions

- View active sessions in settings.
- Revoke individual sessions as needed.

#### GitHub Membership Considerations

|Type|Consideration|
|---|---|
|GitHub Instance Membership|- Access to public repositories  <br>- Create personal projects  <br>- Public profile visibility|
|Organization Membership|- Role-based internal access  <br>- Profile visible to org admins  <br>- Might affect billing|
|Multiple Organization Memberships|- Different roles across orgs  <br>- Broader resource access  <br>- Complex permission and billing  <br>- Requires strict governance|
### Team synchronization

If your company uses Microsoft Entra ID or Okta as your identity provider (IdP), you can manage GitHub team membership through **team synchronization**. When enabled, team sync automatically reflects changes in IdP groups on GitHub—reducing the need for manual updates or custom scripts. This centralized approach simplifies onboarding, permissions management, and access revocation.

|Feature|Description|
|---|---|
|Sync Users|Keep GitHub `Teams` aligned with IdP (for example, Active Directory) group membership|
|Sync on New Team|Automatically populate teams at creation|
|Custom Team Mapping|Use `syncmap.yml` to define custom mappings between team slugs and group names|
|Dynamic Config|Use a `settings` file to derive sync settings from your directory structure|

#### Team Synchronization Use Cases

Team sync is ideal for enterprises looking to streamline membership management within GitHub organizations. Admins can map GitHub teams to IdP groups and manage memberships automatically. This is useful for:

- Onboarding new employees
- Adjusting access as users move between teams
- Removing users who leave the organization

> ⚠️ To use team sync, your IdP admin must enable **SAML SSO** and **SCIM**.

#### Enterprise Managed Users

If you're using **Enterprise Managed Users** in GitHub Enterprise Cloud, all members are provisioned through your IdP. Users don't self-manage GitHub accounts and can't access resources outside the enterprise.

With this model, you can:

- Manage organization/team membership directly through your IdP
- Ensure GitHub users are enterprise-scoped and isolated

For more, see [Getting started with GitHub Enterprise Cloud](https://docs.github.com/get-started/onboarding/getting-started-with-github-enterprise-cloud).

#### Team Synchronization vs. SCIM for GHES

In GitHub Enterprise Server (GHES), managing user access and team memberships can be achieved through various methods, including team synchronization and System for Cross-domain Identity Management (SCIM). Understanding these methods is essential for effective administration.

##### Team Sync in GHES

Team synchronization allows you to link GitHub teams with groups in your Identity Provider (IdP). This integration ensures that any changes in the IdP group—such as adding or removing members—are automatically reflected in the corresponding GitHub team. This approach streamlines team management by centralizing user access control within the IdP.

However, it's important to note that team synchronization isn't a user provisioning service and doesn't invite non-members to join organizations in most cases. Therefore, a user will only be successfully added to a team if they're already an organization member.

Consider the following scenario to understand how team synchronization works in practice:

- When Azure AD group "DevOps Engineers" maps to GitHub team "DevOps"
- When Alice is added to the IdP group → automatically added to the GitHub team
- When she leaves the group → automatically removed from the team

>**Note**: Team Sync in GHES doesn’t provision accounts. Users must already be GitHub organization members.

##### Team Sync Configuration

1. Enable Security Assertion Markup Language(SAML) Single Sign-On(SSO) and SCIM in your IdP.
2. Map GitHub teams to IdP groups via GitHub UI or API.
3. Changes in group membership sync automatically to GitHub.

Supported IdPs:

- **Microsoft Entra ID**: Requires permissions for profile reading and directory access.
- **Okta**: Requires SAML SSO, SCIM, tenant URL, and Single Sign-on for Web Systems(SSWS) token with read-only admin access.

##### Disable Team Sync

To disable:

1. Navigate to **Settings** > **Organization security**
2. Click **Disable team synchronization**

![Screenshot of the organization setting to disable team synchronization.](https://learn.microsoft.com/en-gb/training/github/authenticate-authorize-user-identities-github/media/disable-team-synchronization.png)

>**Note**: Disabling sync removes users from teams if they were added via IdP mapping.

##### SCIM in GHES

SCIM is an open standard protocol designed to automate the exchange of user identity information between identity domains and IT systems. In the context of GHES, SCIM enables administrators to provision, update, and deprovision user accounts directly through the GitHub API. This means you can create, update, and delete user accounts, and sync group information to map GitHub team memberships.

SCIM is useful for managing user lifecycles at scale, ensuring that user data remains consistent across systems.

Consider the following scenario to understand how SCIM works in practice:

- Okta SCIM integration provisions GitHub users automatically
- Bob is added to Okta → GitHub account is provisioned
- Bob changes roles → access and teams update
- Bob leaves → account is deprovisioned

**Key Benefit:** Full automation for account lifecycle management.

#### Team Sync vs. Group SCIM

GitHub supports two primary identity integration approaches:

- **Team Sync**: Focused on syncing group membership to GitHub teams
- **Group SCIM**: Focused on full lifecycle management of users and groups

##### Differences Between Team Sync and Group SCIM

|Feature|Team Sync|Group SCIM|
|---|---|---|
|Focus|Team-level mapping|User and group provisioning|
|Setup|Manual group-to-team mapping|Automated via IdP SCIM config|
|Automation Level|Syncs group membership only|Full lifecycle automation|
|Ideal Use Case|GitHub Teams management|Large orgs with high user turnover|
|Deprovisioning|Manual or IdP-group dependent|Fully automated|
|Identity Model|Classic|Managed Users|

#### Choosing the Right Approach

The choice between Team Sync and Group SCIM depends on your organization’s needs, size, and existing identity management infrastructure:

|Use Case|Recommended Solution|
|---|---|
|Manage repository access by teams|Team Sync|
|Automate user lifecycle|Group SCIM|
|Need full IdP-based governance|Group SCIM|
|GitHub Teams is core to workflow|Team Sync|

#### Usage Limits

When using team synchronization, observe these limits:

- Max members per team: **5,000**
- Max members per organization: **10,000**
- Max teams per organization: **1,500**

Exceeding these may result in performance issues or sync failures.
## Manage repository changes by using pull requests on GitHub
### Introduction

Change is inevitable, especially in software repositories. Project improvements often require the coordination of many people working together in parallel to produce the right output. Responsibly tracking and merging those changes is a complex and substantial challenge.

Fortunately, pull requests offer the right balance of control and convenience. Whether you're interested in making changes, reviewing changes, or understanding the effect of changes across the repository, pull requests are the way GitHub users collaborate on code.

### What are pull requests?

#### Branches

First, let’s define what branches are, why they’re important to developers, and how they’re related to pull requests.

Branches are isolated workspaces where you can develop your work without affecting others in the repository. They allow you to develop features, fix bugs, and safely experiment with new ideas in a contained area of your repository.

Developers working on independent branches is a common concept in modern software development. By having their own branch, a developer can make any changes, called _commits_, without worrying about how their commits affect other developers working on their own branches.

##### Merging branches

Although having each developer work on a separate branch is great for individual productivity, it opens a new challenge. At some point, each developer's branch needs to be _merged_ into a common branch, like `main`. As projects scale, there can be many merges that need to happen, and it becomes increasingly important to track and review each merge. Needing to keep track of multiple changes to a project is where pull requests come in.

#### What is a pull request?

A pull request is a way to document branch changes and communicate that the changes from the developer’s branch are ready to be _merged_ into the base (main) branch. Pull requests enable stakeholders to review and discuss the proposed changes to ensure that the code quality in the base branch is kept as high as possible.

In order for the two branches to be merged, they must be different from one another:

- The _compare_ branch is the developer’s own branch, which contains the specific changes they made.
- The _base_ branch, also referred to as the _main_ branch, is the branch that the changes need to be merged into.

The most common use of _compare_ is to compare branches, such as when you're starting a new pull request. You're always taken to the branch comparison view when starting a new pull request.

#### Create a pull request

Now let’s review how to create a pull request!

1. On `GitHub.com`, navigate to the main page of the repository.
    
2. In the **Branch** menu, select the branch that contains your commits.
    
    ![Screenshot of creating a new branch and naming it.](https://learn.microsoft.com/en-us/training/github/manage-changes-pull-requests-github/media/2-new-branch-name-text-box.png)
    
3. Above the list of files, in the yellow banner, select the **Compare & pull request** button to create a pull request for the associated branch.
    
    ![Screenshot of a yellow text box, highlighting the green compare and pull request button.](https://learn.microsoft.com/en-us/training/github/manage-changes-pull-requests-github/media/2-compare-and-pull-request.png)
    
4. In the **base branch** dropdown menu, select the branch you'd like to merge your changes into. Then select the **compare branch** dropdown menu to select the branch you made your changes in.
    
5. Enter a title and description for your pull request.
    
6. To create a pull request that’s ready for review, select the **Create Pull Request** button. To create a draft pull request, select the dropdown and select **Create Draft Pull Request**, then select **Draft Pull Request**.
    

#### Pull request statuses

Now let’s review the different statuses of a pull request.

- **Draft pull request** - When you create a pull request, you can choose to either create a pull request that’s ready for review or a _draft_ pull request. A pull request with a draft status can’t be merged, and code owners aren’t automatically requested to review draft pull requests.
    
- **Open pull request** - An open status means the pull request is active and not yet merged to the base branch. You can still make commits and discuss and review potential changes with collaborators.
    
- **Closed pull request** - You can choose to close a pull request without merging it into the base/main branch. This option can be handy if the changes proposed in the branch are no longer needed, or if another solution is proposed in another branch.
    
- **Merged pull request** - The merged pull request status means that the updates and commits from the compare branch were combined with the base branch. Anyone with push access to the repository can complete the merge.
    

#### Merge a pull request

1. Under your repository name, select **Pull requests**.
    
    ![Screenshot of the top navigation bar of a repo with the Pull request tab highlighted.](https://learn.microsoft.com/en-us/training/github/manage-changes-pull-requests-github/media/3-pull-request-tab.png)
    
2. In the **Pull requests** list, select the pull request you'd like to merge.
    
3. Scroll down to the bottom of the pull request. Depending on the merge options enabled for your repository, you can:
    
    - Merge all of the commits into the base branch by selecting the **Merge pull request** button. If the **Merge pull request** option isn’t shown, select the merge dropdown menu, choose the **Create a merge commit** option, and then select the **Create a merge commit** button.
        
        ![Screenshot of the dropdown menu of the green merge pull request button with the Create a merge commit selected.](https://learn.microsoft.com/en-us/training/github/manage-changes-pull-requests-github/media/3-merge-pull-request.png)
        
    - **Squash and merge** allows you to take all of your commits and combine them into one. This option can help you keep your repository history more readable and organized. Select the **Squash and merge** option, and then select the **Squash and merge** button.
        
    - The **Rebase and merge** option allows you to make commits without a merge commit. This option enables you to skip a merge by maintaining a linear project history. Select the merge dropdown menu, then choose the **Rebase and merge** option, and then select the **Rebase and merge** button.
        
4. If prompted, enter a commit message, or accept the default message.
    
5. If you have more than one email address associated with your account on `GitHub.com`, select the email address dropdown menu and select the email address to use as the Git author email address. Only verified email addresses appear in this dropdown menu. If you enabled email address privacy, then a no-reply GitHub email is the default commit author email address.
    
    ![Screenshot of a commit change with a description box and the drop-down menu of the email to select as the author of the commit.](https://learn.microsoft.com/en-us/training/github/manage-changes-pull-requests-github/media/3-select-author-of-merge.png)
    
6. Select **Confirm merge**, **Confirm squash and merge**, or **Confirm rebase and merge**.
    
7. Optionally, you can delete the compare branch to keep the list of branches in your repository tidy.


## Search and organize repository history by using GitHub

### Introduction

GitHub projects support virtually unlimited scale. The upside of this scale is that your projects can grow to include countless files, commits, issues, pull requests, and more. The downside is, well, the same.

Suppose you're a developer working on a rapidly growing project. As more contributors come on board, they're able to add features and fix bugs at an incredible rate. However, every one of those changes likely includes a lot of contextual information buried in issues, discussions, commits, and pull requests. While that information seems fresh in everyone's mind at the time, the risk of losing that context as time passes could cost you some significant productivity down the road. What happens when a bug is reported that traces back to work that hasn't been touched for more than a year? Fortunately, GitHub offers a few ways to help you quickly ramp up for any task.

### How to search and organize repository history by using GitHub

Here, we'll discuss how you can use filters, blame, and cross-linking to search and organize repository history.

Put yourself in the position of a developer who has just joined a large project. Someone just posted a new issue reporting a bug related to the web app's sidebar, and you've been assigned to fix it. You've already read through the report a few times and understand the problem being described, so now you need to figure out how to get started with the fix.

As a new team member, you're not yet familiar with the codebase. You also haven't been part of the planning discussions, code reviews, or anything else that would provide you with the context you need to start implementation. You'll first need to acquire that background knowledge to best determine the right fix.

#### Searching GitHub

Although you weren't around for the events that led to the sidebar's implementation, many of those events live on in the project's history. Searching the project's repository for "sidebar" will give you a starting point.

There are two search methods available on GitHub: the global search at the top of the page and the scoped search available on certain repository tabs. They support the same syntax and function in the same way, but with some key differences.

##### Global search

The global search lets you use [the complete search syntax](https://docs.github.com/enterprise-cloud@latest/search-github/searching-on-github) to search across all of GitHub.

![A screenshot of a search across GitHub.](https://learn.microsoft.com/en-us/training/github/search-organize-repository-history-github/media/2-global-search.png)

The search results are comprehensive and include everything from code to issues to the Marketplace (and even users). This is the best way to find mentions of key terms across multiple result types and repositories.

![A screenshot of global search results.](https://learn.microsoft.com/en-us/training/github/search-organize-repository-history-github/media/2-global-search-results.png)

>**Note**: The filter clause `is:pr` filters out issues returned from the issues/pull requests store. Some filter clauses, such as `is:pr`, are only supported by certain search providers and ignored by others. For example, the code-search provider doesn't support that clause, so it will ignore it and return the same code results either way.

In our scenario, using the global search scoped to the current repository is a good way to find code and commits that mention the term "sidebar". You'll also likely get hits for issues and pull requests, although they're not as easy to filter further in the global search results view.

To craft a complex global search, try the [advanced search](https://github.com/search/advanced).

##### Context search

Context searches are available on certain tabs, such as **Issues** and **Pull requests**. These searches are scoped into the current repository and only return results of that type. The benefit to this scoping is that it allows the user interface to expose known type-specific filters such as authors, labels, projects, and more.

![Screenshot of a context search within a repository.](https://learn.microsoft.com/en-us/training/github/search-organize-repository-history-github/media/2-context-search.png)

Using the context search is the preferred option when you're looking for something in the current repository. In our scenario, this is a good way to find search results mentioning "sidebar," which you could then easily refine using the filter dropdowns.

##### Using search filters

There are an infinite number of ways to search using [the complete search syntax](https://docs.github.com/enterprise-cloud@latest/search-github/searching-on-github). However, most searches only make use of a few common filters. While these are often available from context search dropdowns, it's sometimes more convenient to type them in directly.

Here are some example filter queries:

|Query|Explanation|
|---|---|
|`is:open is:issue assignee:@me`|Open issues assigned to the current user (`@me`)|
|`is:closed is:pr author:contoso`|Closed pull requests created by `@contoso`|
|`is:pr sidebar in:comments`|Pull requests where "sidebar" is mentioned in the comments|
|`is:open is:issue label:bug -linked:pr`|Open issues labeled as bugs that do not have a linked pull request|

Learn more about [Understanding the search syntax](https://docs.github.com/enterprise-cloud@latest/search-github/getting-started-with-searching-on-github/understanding-the-search-syntax)

#### What is git blame?

Despite its ominous name, `git blame` is a command that displays the commit history for a file. It makes it easy for you to see who made what changes and when. This makes it much easier to track down other people who have worked on a file in order to seek out their input or participation.

>**Note**: Some Git systems alias `git praise` onto `git blame` to avoid the implication of judgment.

##### Blame in GitHub

GitHub extends the basic `git blame` functionality with a more robust user interface.

![A screenshot of GitHub blame.](https://learn.microsoft.com/en-us/training/github/search-organize-repository-history-github/media/2-github-blame.png)

In our scenario, there are a few ways you might get to this view. You might've found some sidebar code from the global search and selected the **Blame** option to see who worked on it last, or maybe you found a pull request and tracked that back to the last commit that seems related to the bug description. However you got here, the blame view is an effective way to locate a subject matter expert for the task at hand.

#### Cross-linking issues, commits, and more

Part of what makes GitHub great for collaborative software projects is its support for linking disparate pieces of information together. Some of this happens automatically, such as when you create a pull request from a series of commits on a branch. Other times, you can use the interface to manually link pull requests or projects to issues using the dropdown options.

##### Autolinked references

To make it even easier to cross-link different items throughout your project, GitHub offers a shorthand syntax. For example, if you leave a comment like `Duplicate of #8`, GitHub will recognize that #8 is an issue and create the appropriate link for you.

![Screenshot of an autolinked issue.](https://learn.microsoft.com/en-us/training/github/search-organize-repository-history-github/media/2-autolinked-issue.png)

GitHub also links commits for you if you paste in the first seven or more characters of its ID.

![Screenshot of an autolinked commit.](https://learn.microsoft.com/en-us/training/github/search-organize-repository-history-github/media/2-autolinked-commit.png)

In our scenario, these links could prove very valuable for ramping up if someone thought ahead to leave the context. For example, the sidebar's current state might have had some known issues related to a JavaScript dependency. If the issue with that dependency was discussed in another issue that didn't explicitly mention "sidebar," then it would be difficult to find. However, if someone had thought ahead to link the issue in the discussion, then it could save you a lot of time now. Keep that in mind the next time you're documenting issues and pull requests.

Learn more about [Autolinked references and URLs](https://docs.github.com/get-started/writing-on-github/working-with-advanced-formatting/autolinked-references-and-urls).

##### Looping in users with @mention

Besides linking issues and commits, it's often helpful to associate other people with discussions. The easiest way to do this is by using an `@mention`. This kind of mention notifies the mentioned user so that they can participate in the discussion. It's also a good way to identify people associated with issues long after they have been closed.

![Screenshot of an @ mention.](https://learn.microsoft.com/en-us/training/github/search-organize-repository-history-github/media/2-user-mention.png)
## Using GitHub Copilot with Python
### Introduction

GitHub Copilot is an AI coding partner that provides autocomplete suggestions while you code. You get suggestions from Copilot by typing code or describing it in natural language.

Copilot analyses your file and related files, offering suggestions in your text editor. It uses OpenAI Codex, a new AI system developed by OpenAI, to help derive context from written code and comments, and then suggests new lines or entire functions.

GitHub Codespaces is a hosted developer environment operating in the cloud that can be run with Visual Studio Code. You can customize the development experience for any development project on GitHub, preinstalling dependencies, libraries, and even Visual Studio Code extensions and settings.
### What is GitHub Copilot?

Often, when you write code, you need to consult official documentation or other web pages to remember syntax or how to solve a problem. You can also spend hours trying to resolve a problem when the code isn't working. Additionally, you also spend time writing tests and documentation. All these tasks are time consuming. To be more efficient, you could use code snippets or rely on tooling in your integrated development environment (IDE). But is there a better way?

#### How does it work?

GitHub Copilot is an AI assistant that you use from within your IDE that’s capable of generating code and much more. GitHub Copilot uses _prompts_. A prompt is natural language text that you type. Copilot uses the text to provide suggestions based on what you type.

A prompt can look like the following example:

```python
# Create a web API using FastAPI with a route to products.
```

Copilot then uses the prompt to generate a response that you can choose to accept or reject. A response to the prompt might look like the following code:

```python
from fastapi import FastAPI
app = FastAPI()

@app.get("/products")
def read_products():
    return []
```

#### How it recognizes prompts

Copilot can tell that something is a prompt or an instruction if you:

- Type it as a comment in a code file with a file ending like .py or .js.
- Type text in a markdown file and wait a few seconds for Copilot to return a response.

#### Accepting suggestions

What you get back from Copilot is a _suggestion_, or text that shows itself as gray code, if you use black as your text color. To accept the suggestion, you need to press the Tab key.

Copilot might suggest more than one thing. In this case, you can cycle between suggestions by using Ctrl + Enter, and select the most appropriate one.

### Use GitHub Copilot with Python

#### Developing with GitHub Copilot

Often when we build out projects, we need to continuously ensure our code is fresh and updated. Additionally, we might need to fix any bugs that come up or add new features to improve functionality and usability. Let's explore some ways to make updates with GitHub Copilot and GitHub Copilot Chat, an interactive chat interface that lets you ask and receive answers to code-related questions.

##### Prompt engineering

GitHub Copilot can suggest code as you enter it, but you can also create useful suggestions by building prompts. A prompt, which is our input, is a collection of instructions or guidelines that help generate code. A prompt is useful to generate specific responses from Copilot. The prompt might be a comment or input when using GitHub Copilot Chat that steers Copilot to generate code on your behalf or writing code that Copilot autocompletes.

The quality of output from Copilot depends on how well you craft your prompt. Designing an effective prompt is crucial to ensuring you achieve your desired outcome.

For example, consider the following prompt:

```python
# Create an API endpoint
```

The prompt is ambiguous and vague, so the result from GitHub Copilot might not be what you need. It could, for example, suggest code that uses a framework that you don't know, or an endpoint that requires data that you don't recognize.

Now consider this prompt:

```python
# Create an API endpoint using the FastAPI framework that accepts a JSON payload in a POST request
```

The prompt is specific, clear, and allows GitHub Copilot to understand the goal and scope of the task. You can provide context and examples to Copilot using comments or code, but you can also use the chat option of GitHub Copilot Chat to enhance your prompt. Having a good prompt ensures that the model generates a high-quality output.

##### Best practices using GitHub Copilot

Copilot supercharges your productivity but requires some good practices to ensure quality. Some best practices when using Copilot are:

Keep your prompts simple then add more elaborate components as you keep going. For example:

```
create an HTML form with a text field and button
```

Next, elaborate more on the prompt to get more specific suggestions:

```
Add an event listen to the button to send a POST request to /generate endpoint and display response in a div with id "result"
```

Cycle between suggestions. You can do this using `Ctrl+Enter` (or `Cmd+Enter` on a Mac). You get various suggestions from Copilot, and you can pick the best output. Optionally, when using GitHub Copilot Chat, you can use the chat input to add your prompt and interact with the output.

If you're not getting the results you want, then you can reword the prompt or start writing code for Copilot to autocomplete.

>**Note**: GitHub Copilot uses open files in your text editor as additional context. This is helpful because it provides useful information in addition to the prompt or code you may be writing. If you need GitHub Copilot to provide suggestions based on other files you can open those or use `@workspace` with your prompt when using GitHub Copilot Chat.
