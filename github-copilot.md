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

#### Finding License Usage for a Specific Organization**

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

###### GitHub Enterprise Server (GHES) Dashboard

Next, you'll dive into how to gain access to view track these licenses .

1. Log in to the **GitHub Enterprise Server Admin Console**.
2. Go to **Settings > License Usage**.
3. View:
    - **Total allocated licenses**
    - **Active users**
    - **Available seats**
    - **Historical license usage trends**

**REST API Alternative***

For **programmatic access**, use the REST API:

```bash
curl -H "Authorization: token YOUR-TOKEN" \
"https://api.github.com/enterprises/YOUR-ENTERPRISE/license"
```

##### Method 4. Finding License Usage Across Multiple GitHub Instances

For **large enterprises** with multiple GitHub Enterprise **Server instances**, admins must track **license consumption** across deployments.

###### GitHub Enterprise Metrics API

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

# Metered Usage Reports

Completed100 XP

- 3 minutes

In this unit, you'll learn how to monitor and manage billing for GitHub’s metered products, including Actions minutes, storage, licenses, and advanced features like Copilot and GHAS.

GitHub provides detailed billing and consumption reports to track the usage of **metered products**. These reports help administrators monitor costs, allocate resources efficiently, and ensure compliance with organizational policies.

## GitHub Actions Minutes

GitHub Actions is a CI/CD automation tool where workflows run on virtual machines. The minutes consumed in these workflows are metered based on repository type, runner type, and usage.

### Tracking Consumption

- Navigate to **Settings → Billing** in your GitHub organization or account.
- Under the **GitHub Actions** section, you can see the number of minutes used.
- Usage is broken down by repository, runner type (Linux, macOS, Windows), and remaining quota.

### Billing Details

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

### Optimization Strategies

- Use **self-hosted runners** for high-volume workflows to reduce costs.
- Optimize workflow scripts by caching dependencies and reducing redundant jobs.
- Limit workflows to **only trigger when necessary** (e.g., push to `main` branch only).

## Storage for GitHub Packages

GitHub Packages allows storing artifacts, container images, and dependencies. Storage is metered based on the volume of stored data and data transfer usage.

### Tracking Consumption

- Navigate to **Settings → Billing → GitHub Packages** to view storage usage.
- Breakdown includes **storage (GB) and data transfer (GB)** used per repository.

### Billing Details

- **Free Allocation:**
    - **Public repositories:** Free storage and bandwidth.
    - **Private repositories:**
        - Storage up to 2GB
        - Data transfer up to 1GB per month

For details on storage limits and usage beyond the free allocation, see [GitHub’s pricing page](https://github.com/pricing).

### Optimization Strategies

- Regularly **delete unused packages** or enable retention policies.
- Store frequently accessed images in a **centralized registry** to reduce duplication.
- Use **compressed formats** to reduce storage consumption.

## GitHub Enterprise (GHE) Licenses

GitHub Enterprise provides advanced features for organizations, and the number of **active users** determines license consumption.

### Tracking Consumption

- Go to **Enterprise Settings → Billing** to view **license usage reports**.
- Monitor active users vs. allocated licenses.

### Billing Details

- **Pricing Model:**
    - Each user with access to private repositories consumes **one license**.
    - Organizations pay per user annually or monthly.
- **Inactive Users:**
    - If an admin **removes** a user, the license remains **assigned** for the billing period but can be reallocated.

### Optimization Strategies

- Audit **inactive users** and revoke access to free up licenses.
- Use **SSO and SCIM provisioning** to automate user management.

## GitHub Advanced Security (GHAS) Licenses

GitHub Advanced Security (GHAS) offers **code scanning, secret scanning, and dependency review** for enhanced security.

### Tracking Consumption

- View reports in **Settings → Billing → GHAS Usage** to see active committers.
- The report shows **unique committers per billing period**.

### Billing Details

- **Pricing Model:**
    - Charged per **unique committer** per month.
    - If a committer contributes to multiple repositories, they **only count once**.
- **Free Tier:** Not available (only for public repositories).

### Optimization Strategies

- **Restrict GHAS** to repositories that **truly need advanced security**.
- Use **branch protections** to limit unnecessary scans on feature branches.

---

## GitHub Copilot**

GitHub Copilot provides **AI-driven code completion** and suggestions, billed per user.

### Tracking Consumption

- Admins can track **Copilot usage** under **Billing → Copilot** in organization settings.
- The report shows **active users** and monthly billing estimates.

### Billing Details

- **Access Model:**
    - Available for individuals and businesses with different subscription options.
- **Free Access:**
    - Free for students and verified open-source maintainers.
    - Free for **select enterprise customers** (trial-based).

For current Copilot plans and subscription details, see [GitHub Copilot pricing](https://github.com/features/copilot#pricing).

### Optimization Strategies

- Regularly **review and deactivate Copilot** for users who don’t need it.
- Encourage developers to **disable Copilot** in projects where AI-generated code is unnecessary.

## Large File Storage (LFS)

GitHub LFS is used for storing large binary files separately from Git repositories.

### Tracking Consumption

- View LFS usage in **Billing → LFS Usage**.
- Report includes **storage (GB) and bandwidth usage (GB)**.

### Billing Details

- **Free Tier:**
    - 1GB of storage per repository
    - 1GB of bandwidth per month

For more information on Git Large File Storage (LFS) usage and limits, see [GitHub's LFS documentation](https://docs.github.com/en/github/managing-large-files/about-git-large-file-storage#about-storage-and-bandwidth-usage).

### Optimization Strategies

- **Use external storage services** (e.g., AWS S3, Azure Blob Storage) for large files.
- **Delete unused large files** to optimize storage.
- **Enable Git LFS file pruning** to remove unreferenced objects.

==============



## Introduction to prompt engineering with GitHub Copilot
### Introduction

GitHub Copilot, powered by OpenAI, is changing the game in software development. GitHub Copilot can grasp the intricate details of your project through its training of data containing both natural language and billions of lines of source code from publicly available sources, including code in public GitHub repositories. This allows GitHub Copilot to provide you with more context-aware suggestions.

But to get the most out of GitHub Copilot, you need to know about prompt engineering. Prompt engineering is how you tell GitHub Copilot what you need. The quality of the code it gives back depends on how clear and accurate your prompts are.
### Prompt engineering foundations and best practices

#### What is prompt engineering?

Prompt engineering is the process of crafting clear instructions to guide AI systems, like GitHub Copilot, to generate context-appropriate code tailored to your project's specific needs. This ensures the code is syntactically, functionally, and contextually correct.

Now that you know what prompt engineering is, let's learn about some of its principles.

#### Principles of prompt engineering

Before we explore specific strategies, let's first understand the basic principles of prompt engineering, summed up in the **4 Ss** below. These core rules are the basis for creating effective prompts.

- **Single**: Always focus your prompt on a single, well-defined task or question. This clarity is crucial for eliciting accurate and useful responses from Copilot.
- **Specific**: Ensure that your instructions are explicit and detailed. Specificity leads to more applicable and precise code suggestions.
- **Short**: While being specific, keep prompts concise and to the point. This balance ensures clarity without overloading Copilot or complicating the interaction.
- **Surround**: Utilize descriptive filenames and keep related files open. This provides Copilot with rich context, leading to more tailored code suggestions.

These core principles lay the foundation for crafting efficient and effective prompts. Keeping the 4 Ss in mind, let's dive deeper into advanced best practices that ensure each interaction with GitHub Copilot is optimized.

#### Best practices in prompt engineering

The following advanced practices, based on the 4 Ss, refine and enhance your engagement with Copilot, ensuring that the generated code isn't only accurate but perfectly aligned with your project's specific needs and contexts.

##### Provide enough clarity

Building on the 'Single' and 'Specific' principles, always aim for explicitness in your prompts. For instance, a prompt like "Write a Python function to filter and return even numbers from a given list" is both single-focused and specific.

![Screenshot of a Copilot chat with a Python prompt.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/2-python-prompt.png)

##### Provide enough context with details

Enrich Copilot's understanding with context, following the 'Surround' principle. The more contextual information provided, the more fitting the generated code suggestions are. For example, by adding some comments at the top of your code to give more details to what you want, you can give more context to Copilot to understand your prompt, and provide better code suggestions.

![Screenshot of comments added to code for better Copilot suggestions.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/2-add-comments-example.gif)

In the example above, we used steps to give more detail while keeping it short. This practice follows the 'Short' principle, balancing detail with conciseness to ensure clarity and precision in communication.

>**Note**: Copilot also uses parallel open tabs in your code editor to get more context on the requirements of your code.

##### Provide examples for learning

Using examples can clarify your requirements and expectations, illustrating abstract concepts and making the prompts more tangible for Copilot.

![Screenshot of an example used to clarify prompts for Copilot.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/2-clarify-prompts-example.gif)

##### Assert and iterate

One of the keys to unlocking GitHub Copilot's full potential is the practice of iteration. Your first prompt might not always yield the perfect code, and that's perfectly okay. If the first output isn't quite what you're looking for, treat it as a step in a dialogue. Erase the suggested code, enrich your initial comment with added details and examples, and prompt Copilot again.

Now that you learned best practices to improve your prompting skills, let's take a closer look at how you can provide examples Copilot can learn from.

#### How Copilot learns from your prompts

GitHub Copilot operates based on AI models trained on vast amounts of data. To enhance its understanding of specific code contexts, engineers often provide it with examples. This practice, commonly found in machine learning, led to different training approaches such as:

##### Zero-shot learning

Here, GitHub Copilot generates code without any specific examples, relying solely on its foundational training. For instance, suppose you want to create a function to convert temperatures between Celsius and Fahrenheit. You can start by only writing a comment describing what you want, and Copilot might be able to generate the code for you, based on its previous training, without any other examples.

![Screenshot of Copilot creating a temperature conversion code from a comment.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/2-create-temp-conversion-from-comment.png)

##### One-shot learning

With this approach, a single example is given, aiding the model in generating a more context-aware response. Building upon the previous zero-shot example, you might provide an example of a temperature conversion function and then ask Copilot to create another similar function. Here's how it could look:

![Screenshot of Copilot using an example to create similar temperature conversion code.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/2-create-temp-conversion-from-example.png)

##### Few-shot learning

In this method, Copilot is presented with several examples, which strike a balance between zero-shot unpredictability and the precision of fine-tuning. Let's say you want to generate code that sends you a greeting depending on the time of the day. Here's a few-shot version of that prompt:

![Screenshot of Copilot generating greeting code based on multiple examples.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/2-generate-greeting-code-from-examples.png)

### GitHub Copilot user prompt process flow

#### Inbound flow:

![Illustration of GitHub Copilot inbound flow.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/3-github-copilot-inbound-flow.png)

Let's walk through all the steps Copilot takes to process a user's prompt into a code suggestion.

##### 1. Secure prompt transmission and context gathering

The process begins with the secure transmission of the user prompt over HTTPS. This ensures that your natural language comment is sent to GitHub Copilot's servers securely and confidentially, protecting sensitive information.

GitHub Copilot securely receives the user prompt, which could be a Copilot chat or a natural language comment provided by you within your code.

Simultaneously, Copilot collects context details:

- Code before and after the cursor position, which helps it understand the immediate context of the prompt.
- Filename and type of the file being edited, allowing it to tailor code suggestions to the specific file type.
- Information about adjacent open tabs, ensuring that the generated code aligns with other code segments in the same project.
- Information on project structure and file paths
- Information on programming languages and frameworks
- Pre-processing using Fill-in-the-Middle (FIM) technique to consider both the preceding and following code context, effectively expanding the model's understanding allowing Copilot to generate more accurate and relevant code suggestions by leveraging a broader context.

These steps translate the user's high-level request into a concrete coding task.

##### 2. Proxy filter

Once the context is gathered and the prompt is built, it passes securely to a proxy server hosted in a GitHub-owned Microsoft Azure tenant. The proxy filters traffic, blocking attempts to hack the prompt or manipulate the system into revealing details about how the model generates code suggestions.

##### 3. Toxicity filtering

Copilot incorporates content filtering mechanisms before proceeding with intent extraction and code generation, to ensure that the generated code and responses don't include or promote:

- **Hate speech and inappropriate content**: Copilot employs algorithms to detect and prevent the intake of hate speech, offensive language, or inappropriate content that could be harmful or offensive.
- **Personal data**: Copilot actively filters out any personal data, such as names, addresses, or identification numbers, to protect user privacy and data security.

##### 4. Code generation with LLM

Finally, the filtered and analyzed prompt is passed to LLM Models, which generate appropriate code suggestions. These suggestions are based on Copilot’s understanding of the prompt and the surrounding context, ensuring that the generated code is relevant, functional, and aligned with project-specific requirements.

#### Outbound Flow:

![Illustration of GitHub Copilot outbound flow.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/3-github-copilot-outbound-flow.png)

##### 5. Post-processing and response validation

Once the model produces its responses, the toxicity filter removes any harmful or offensive generated content. The proxy server then applies a final layer of checks to ensure code quality, security, and ethical standards. These checks include:

- **Code quality**: Responses are checked for common bugs or vulnerabilities, such as cross-site scripting (XSS) or SQL injection, ensuring that the generated code is robust and secure.
- **Matching public code (optional)**: Optionally, administrators can enable a filter that prevents Copilot from returning suggestions over ~150 characters if they closely resemble existing public code on GitHub. This prevents coincidental matches from being suggested as original content. If any part of the response fails these checks, it is either truncated or discarded.

##### 6. Suggestion delivery and feedback loop initiation

Only responses that pass all filters are delivered to the user. Copilot then initiates a feedback loop based on your actions to achieve the following:

- Grow its knowledge from accepted suggestions.
- Learn and improve through modifications and rejections of its suggestions.

##### 7. Repeat for subsequent prompts

The process is repeated as you provide more prompts, with Copilot continuously handling user requests, understanding their intent, and generating code in response. Over time, Copilot applies the cumulative feedback and interaction data, including context details, to improve its understanding of user intent and refine its code generation capabilities.
### GitHub Copilot data

#### Data handling for GitHub Copilot code suggestions

GitHub Copilot in the code editor does not retain any prompts like code or other context used for the purposes of providing suggestions to train the foundational models. It discards the prompts once a suggestion is returned.

GitHub Copilot Individual subscribers can opt-out of sharing their prompts with GitHub which will otherwise be used to finetune GitHub’s foundational model.

#### Data handling for GitHub Copilot chat

GitHub Copilot Chat operates as an interactive platform, allowing developers to engage in conversational interactions with the AI assistant to receive coding assistance. Here are the steps that it carries out which might be distinct from other features like code completion:

- **Formatting**: Copilot meticulously formats the generated response for optimal presentation within the chat interface. It highlights code snippets to improve readability and may include options for direct integration into your code. Copilot showcases the formatted response in the Copilot Chat window within the IDE, allowing you to easily review and interact with the provided information.
- **User engagement**: You can actively engage with the response by asking follow-up questions, requesting clarifications, or providing additional input. The chat interface maintains a conversation history to facilitate contextual understanding in subsequent interactions.
- **Data retention**: For Copilot Chat used outside the code editor, GitHub typically retains prompts, suggestions, and supporting context for 28 days. Specific retention policies for Copilot Chat within the code editor may vary.

The same goes for CLI, Mobile, and GitHub Copilot Chat on GitHub.com.

#### Prompt types supported by GitHub Copilot Chat

GitHub Copilot Chat processes a wide range of coding-related prompts, demonstrating its versatility as a conversational coding assistant. Here are some common input types:

- **Direct Questions**: You can ask specific questions about coding concepts, libraries, or troubleshooting issues. For example, "How do I implement a quick sort algorithm in Python?" or "Why is my React component not rendering?"
- **Code-Related Requests**: You can request code generation, modification, or explanation. Examples include "Write a function to calculate factorial," "Fix this error in my code," or "Explain this code snippet."
- **Open-Ended Queries**: You can explore coding concepts or seek general guidance by asking open-ended questions like "What are the best practices for writing clean code?" or "How can I improve the performance of my Python application?"
- **Contextual Prompts**: You can provide code snippets or describe specific coding scenarios to seek tailored assistance. For instance, "Here's a part of my code, can you suggest improvements?" or "I'm building a web application, can you help me with the authentication flow?"

Copilot Chat's ability to process diverse input types enhances its utility as a comprehensive coding companion.

#### Limited context windows

![Illustration of GitHub Copilot context window.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/4-copilot-data-limited-context-window.png)

While GitHub Copilot Chat excels at understanding and responding to prompts, it's essential to acknowledge the limitation of context windows. This refers to the amount of surrounding code and text the model can process simultaneously to generate suggestions. GitHub Copilot's context window typically ranges from approximately 200-500 lines of code or up to a few thousand tokens. This limitation can vary depending on the specific implementation and version of Copilot being used.

Copilot Chat currently operates with a context window of 4k tokens, providing a broader scope for understanding and responding to user queries compared to the standard Copilot.

Despite these advancements, you should be mindful of context window limitations when crafting prompts. Breaking down complex problems into smaller, more focused queries or providing relevant code snippets can significantly enhance the model's ability to provide accurate and helpful responses.
### GitHub Copilot Large Language Models (LLMs)

GitHub Copilot is powered by Large Language Models (LLMs) to assist you in writing code seamlessly. In this unit, we focus on understanding the integration and impact of LLMs in GitHub Copilot. Let's review the following topics:

- What are LLMs?
- The role of LLMs in GitHub Copilot and prompting
- Fine-tuning LLMs
- LoRA fine-tuning

#### What are LLMs?

Large Language Models (LLMs) are artificial intelligence models designed and trained to understand, generate, and manipulate human language. These models are ingrained with the capability to handle a broad range of tasks involving text, thanks to the extensive amount of text data they're trained on. Here are some core aspects to understand about LLMs:

##### Volume of training data

LLMs are exposed to vast amounts of text from diverse sources. This exposure equips them with a broad understanding of language, context, and intricacies involved in various forms of communication.

##### Contextual understanding

They excel in generating contextually relevant and coherent text. Their ability to understand context allows them to provide meaningful contributions, be it completing sentences, paragraphs, or even generating whole documents that are contextually apt.

##### Machine learning and AI integration

LLMs are grounded in machine learning and artificial intelligence principles. They're neural networks with millions, or even billions, of parameters that are fine-tuned during the training process to understand and predict text effectively.

##### Versatility

These models aren't limited to a specific type of text or language. They can be tailored and fine-tuned to perform specialized tasks, making them highly versatile and applicable across various domains and languages.

#### Role of LLMs in GitHub Copilot and prompting

GitHub Copilot utilizes LLMs to provide context-aware code suggestions. The LLM considers not just the current file but also other open files and tabs in the IDE to generate accurate and relevant code completions. This dynamic approach ensures tailored suggestions, improving your productivity.

#### Fine-tuning LLMs

Fine-tuning is a critical process that allows us to tailor pretrained large language models (LLMs) for specific tasks or domains. It involves training the model on a smaller, task-specific dataset, known as the target dataset, while using the knowledge and parameters gained from a large pretrained dataset, referred to as the source model.

![Diagram that shows how fine-tuning is used in Large Language Models.](https://learn.microsoft.com/en-us/training/github/introduction-prompt-engineering-with-github-copilot/media/4-fine-tune-in-large-language-models-diagram.png)

Fine-tuning is essential to adapt LLMs for specific tasks, enhancing their performance. However, GitHub took it a step further by using the LoRA fine tuning method, which we discuss next.

##### LoRA fine-tuning

Traditional full fine-tuning means to train all parts of a neural network, which can be slow and heavily reliant on resources. But LoRA (Low-Rank Adaptation) fine-tuning is a clever alternative. It's used to make large pretrained language models (LLMs) work better for specific tasks without redoing all the training.

Here's how LoRA works:

- LoRA adds smaller trainable parts to each layer of the pretrained model, instead of changing everything.
- The original model remains the same, which saves time and resources.

What's great about LoRA:

- It beats other adaptation methods like adapters and prefix-tuning.
- It's like getting great results with fewer moving parts.

In simple terms, LoRA fine-tuning is about working smarter, not harder, to make LLMs better for your specific coding requirements when using Copilot.

## Using advanced GitHub Copilot features
### Introduction

GitHub Copilot is an AI coding partner that provides autocomplete suggestions while you code. Get suggestions by typing code or interactively using natural language.

Copilot analyses your file and related files, offering suggestions in your text editor. It uses context from written code and comments, and then suggests new lines or entire functions.

GitHub Codespaces is a hosted developer environment operating in the cloud that can be run with Visual Studio Code. You can customize the development experience for any development project on GitHub, preinstalling dependencies, libraries, and even Visual Studio Code extensions and settings.

#### Scenario: Working with an existing project

As a developer, you want to be more productive typing code faster both for net new projects and existing ones. For this task, you want to use advanced features from an AI assistant that helps improve your developer workflows in code writing, documentation, testing, and more.
### Advanced GitHub Copilot features

Often, when you work with code, you need to review the project's documentation in addition to libraries and framework documentation. In order to write code or documentation, you must have a good understanding of the codebase. Tasks like fixing bugs and writing tests can be time intensive, but at the same time necessary for most projects. Fortunately, GitHub Copilot has several advanced features that can make these tasks easier and more efficient.

#### The basics

When GitHub Copilot is enabled, it provides you with suggestions. These suggestions are called ghost text. You can either ignore the ghost text, or accept it by pressing the **Tab** key. The suggestions don't require a prompt because by default GitHub Copilot uses the files you have open as context. However, you can provide a prompt using a comment, the chat window, or the inline chat within your code.

#### Chatting with GitHub Copilot

GitHub Copilot allows you to have an interactive discussion using the chat feature. In Visual Studio Code, you can click the chat icon on the left sidebar, which opens the chat interface in a dedicated pane.

In this pane, you can ask questions about the code you're currently working on or other software-related questions.

#### Using inline chat

Besides the dedicated chat pane, you can use the inline chat. It allows you to interact with GitHub Copilot without leaving your code.

Access the inline chat by using **Ctrl+i** on Windows or **Command+i** on a Mac. One of the benefits of using the inline chat is that you don't have to switch context by going to a different pane. The suggestions and interactions happen closer to the code.

#### Slash commands

Within the chat pane or when using the inline chat, you can use slash commands. These commands allow GitHub Copilot to use a specific intent for quickly solving common development tasks.

If you type a forward slash in the chat pane or inline chat, you should see a drop-down menu with all the slash commands available. For example, the `/tests` slash command helps you write tests, while the `/docs` command is intended for writing documentation.

Using specific slash commands to create a question is a good way to get better responses without having to write longer prompts.

#### Agents

Visual Studio Code has a feature called _agents_ that allows you to interact with GitHub Copilot. These agents allow you to ask questions using a specific context. For example the `@terminal` agent helps you chat with GitHub Copilot to interact with the terminal.

Another agent is `@workspace`, which is aware of your entire workspace. It allows you to ask questions about the entire project. To use an agent, prefix your question with the agent, for example: `@workspace how can I package this project?`.
### Applied GitHub Copilot techniques

#### Advanced tasks with GitHub Copilot

It's common to work with an existing project as an engineer. When fixing code or implementing features, we need to write documentation and tests and work with terminal commands. Let's go through some ways you can accomplish this using GitHub Copilot.

##### Implicit prompts

Although you can be specific in prompts for getting GitHub Copilot guidance, you can take advantage of features that implicitly provide a precrafted prompt to get a good answer.

For example, if you're working on a Python project, and you have a file open with the following code that has a bug in it:

```python
with open("file.txt", "r") as file:
    # Read the file and print the content
    contents = file.read
```

After selecting the code and using **Ctrl+i** on Windows or **Command+i** on a Mac, you can ask GitHub Copilot to help you fix the code using the inline chat and the `/fix` slash command.

If you only type `/fix`, you might get a response from GitHub Copilot similar to this suggestion: _"To fix the code, I would add parentheses after file.read to call the read method and fix the typo in the method name."_

Slash commands can be used to both in the inline chat and the chat interface. In addition to the `/fix` command, here are some of the most useful slash commands you can use in Copilot chat:

- `/doc`: Adds comments to the specified or selected code.
- `/explain`: Gets explanations about the code.
- `/generate`: Generates code to answer the specified question.
- `/help`: Gets help on how to use Copilot chat.
- `/optimize`: Analyzes and improves the runtime of the selected code.
- `/tests`: Creates unit tests for the selected code.

Using slash commands allows for easier interaction with GitHub Copilot and helps you get better responses without having to write longer prompts.

Combining features like slash commands with inline chat allows you to choose the way that works best for you and the code you're working on.

##### Selective context

GitHub Copilot can be customized to provide suggestions based on the context you're working on. For example, you can ask GitHub Copilot to provide suggestions based on the entire workspace or the terminal output.

GitHub Copilot can give you an accurate suggestion for your project without requiring you to open many files. Imagine you need to package your project using a _Dockerfile_. A _Dockerfile_ is a special file that needs to have specific instructions to package your project. You can use the `@workspace` agent to ask GitHub Copilot how to help you out. For example, open GitHub Copilot Chat and type the following command:=

```
@workspace I need to create a Dockerfile for this project, can you generate one that will help me package it?
```

You'll get a response back that explains the steps to create a _Dockerfile_ for your project, along with some explanation on what the steps of the file are going to do.

As always, if the suggestions aren't exactly what you are looking for, you can reword the prompt and be more specific. For example, you could ask GitHub Copilot to use a specific step when creating the _Dockerfile_:

```
@workspace help me create a Dockerfile to package this project but make sure you are using a Virtual Environment for Python.
```

In addition to the `@workspace` agent, you can use other agents like `@terminal`, `@file`, and `@directory` to get context-specific suggestions:

- `@terminal`: Provides suggestions based on the terminal output.
    - Example: @terminal How do I fix the error message I'm seeing?
- `@file`: Focuses on the content of a specific file.
    - Example: @file Can you help me refactor this function in main.py?
- `@directory`: Considers the contents of a specific directory.
    - Example: @directory How can I optimize the scripts in the utils directory?

If you're stuck or not getting the results you want, then you can reword the prompt or start writing code for Copilot to autocomplete.

>**Note**: Although you can be specific with `@workspace`, by default GitHub Copilot uses open files in your text editor as additional context.

## GitHub Copilot Across Environments: IDE, Chat, and Command Line Techniques
### Introduction

GitHub Copilot is an advanced AI-powered coding assistant that can dramatically enhance developer efficiency. GitHub Copilot saves time for developers, enabling them to concentrate on higher-level problem-solving and innovation by removing menial tasks off their plate and providing relevant code completion and generating entire blocks of code.

GitHub Copilot offers flexible interaction options tailored to your workflow. Whether through code completion, chat, or commands, Copilot meets you where you are, enhancing your development experience and productivity. Understanding these interaction modes is key to unlocking the full potential of GitHub Copilot and optimizing your coding workflow.
### Code completion with GitHub Copilot

GitHub Copilot code completion features live directly within your IDE, where you write and review your code. GitHub Copilot integrates seamlessly with editors like Visual Studio Code or JetBrains, offering features such as autosuggestions, a multiple suggestions pane, and support for various coding styles. You primarily interact with GitHub Copilot through these IDE tools, and understanding how and where to use them helps you optimize its powerful code generation abilities.

#### GitHub Copilot supported languages

GitHub Copilot provides robust support for a wide range of programming languages and frameworks, with strong capabilities in:

- Python
- JavaScript
- Java
- TypeScript
- Ruby
- Go
- C#
- C++

While these languages receive exceptional support, GitHub Copilot can assist with many other languages and frameworks as well.

>**Tip**: GitHub Copilot offers a free tier with **2,000 code autocompletes and 50 chat messages per month**. To get started, open Visual Studio Code, click on the GitHub Copilot icon, and then click "Sign in to Use GitHub Copilot for Free". Log in to your GitHub account in the window that will open in the browser. [Learn more](https://gh.io/copilot). Educators, Students and select open-source maintainers can receive Copilot Pro for free, learn how at: [https://aka.ms/Copilot4Students](https://aka.ms/Copilot4Students).

#### Auto suggestions

Copilot offers code suggestions as you type: sometimes completing the current line, sometimes suggesting a whole new block of code. You can accept all, part, or ignore the suggestion. This ability to provide real-time, context-aware suggestions saves valuable development time by reducing the need to search for syntax, troubleshoot logic, or repeatedly write common patterns.

![Screenshot of auto completion ghost text.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/auto-completion-ghost-text.png)

#### Multiple suggestions pane

When you're working on a code block and GitHub Copilot offers a suggestion, you see a grayed-out code snippet. To explore more options, hover over the suggestion to reveal the GitHub Copilot control panel.

![Screenshot of multiple suggestion auto completion ghost text.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/multiple-suggestion-auto-completion-ghost-text.png)

Click the forward or backward arrow buttons in the control panel to see the next or previous suggestions. You can also use keyboard shortcuts:

- macOS: Option (⌥) or Alt+] (next), Option (⌥) or Alt+[ (previous)
- Windows or Linux: Alt+] (next), Alt+[ (previous)

![Screenrecord of suggestions pane.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/suggestions-pane.gif)

While GitHub Copilot is superb at suggesting code for you, it also demonstrates its ability to adapt through the following ways:

- **Method Implementation**: When you start typing a method name, Copilot can suggest the entire implementation, following your established coding style.
- **Naming Conventions**: It picks up on your preferred naming conventions for variables, functions, and classes.
- **Formatting**: Copilot adapts to your indentation style, bracket placement, and other formatting preferences.
- **Comment Style**: It can mimic your comment style, whether you prefer inline comments, block comments, or doc strings.
- **Design Patterns**: When your project consistently uses certain design patterns, Copilot suggests code that aligns with these patterns.

#### Using coding comments for suggestions

A key aspect of this capability is how it incorporates coding comments to enhance its suggestions. This section explores the various ways GitHub Copilot utilizes comments to improve its code completion and generation capabilities.

##### Understanding comment context

When integrated into your existing codebase, GitHub Copilot uses various aspects of your code to provide more relevant suggestions, including code comments. Developers often use comments to clarify code intent and enhance collaboration, and Copilot, as your AI coding assistant, makes use of these comments in much the same way. By understanding the intent behind the comments, Copilot can provide more accurate and context-aware code suggestions through two key processes:

- **Natural Language Processing**: Copilot uses advanced natural language processing (NLP) techniques to interpret the meaning and intent behind comments in the code.
- **Contextual Analysis**: It analyzes comments in relation to the surrounding code, understanding their relevance and purpose within the broader context of the file or project.

#### Types of comments utilized

Copilot can work with various types of comments to inform its suggestions:

- **Inline comments**: Short explanations next to specific lines of code.
- **Block comments**: Longer explanations that might describe a function or class.
- **Docstrings**: Formal documentation strings in languages like Python.
- **TODO comments**: Notes about future implementations or improvements.
- **API Documentation**: Comments that describe the usage and parameters of functions or methods.

#### Comment-driven code generation

Copilot uses comments in several ways to generate and suggest code:

- **Function implementation**: When a function is described in comments, Copilot can suggest an entire implementation based on that description.
    
    ![Screenshot of multiple line code completion ghost text.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/multiple-line-code-completion-ghost-text.png)
    
- **Code completion**: Copilot uses comments to provide more accurate code completions, understanding the developer's intent.
    
    ![Screenshot of whole function  auto completion ghost text.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/whole-function-auto-completion-ghost-text.png)
    
    In this example, we have a comment describing a function to reverse a string. Based on this comment, Copilot is likely to suggest an implementation using Python's slice notation with a step of -1, which efficiently reverses the string.
    
- **Variable naming**: Comments can influence Copilot's suggestions for variable names, making them more descriptive and context-appropriate.
    
    ![Screenshot of variable name auto completion ghost text.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/variable-name-auto-completion-ghost-text.png)
    
    Here, we have a comment describing a list of the user's favorite books. Copilot would likely suggest descriptive variable names that match the context. In this case, it suggested "favorite_books" as the variable name, which clearly describes the content of the list.
    
- **Algorithm selection**: When comments describe a specific algorithm or approach, Copilot can suggest code that aligns with that method.
    
    ![Screenshot of algorithm auto completion ghost text.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/algorithm-auto-completion-ghost-text.png)
    
    In the example above, we provide comments that outline the steps of the bubble sort algorithm. Based on these comments, Copilot would likely suggest an implementation that closely follows the steps described.
### GitHub Copilot Chat

GitHub Copilot Chat is an advanced feature of the GitHub Copilot ecosystem, designed to provide developers with an interactive, conversational AI assistant directly within their development environment.It allows developers to have natural language conversations about their code, ask questions, and receive intelligent responses and suggestions in real-time. 

To access Copilot in your IDE, click the chat icon on the left navbar.

[![Screenshot of Chat.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat.png#lightbox)

GitHub Copilot Chat is particularly beneficial in certain scenarios:

- **Complex code generation** When you need to implement complex algorithms, data structures, or generate boilerplate code for specific design patterns, Copilot Chat can help streamline the process. It can assist in creating intricate regular expressions, constructing detailed SQL queries, or developing advanced data structures like a Bubble sort in Python.
    
    [![Screenshot of chat code generation.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-code-generation.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-code-generation.png#lightbox)
    
- **Debugging assistance** If you encounter errors in your code, Copilot Chat can be valuable in analyzing error messages and suggesting potential fixes. It can help identify logical errors and provide step-by-step explanations of problematic sections of code. One way to achieve this is by using Copilot inline-chat by highlighting the piece of code containing the error, right clicking and selecting Copilot, then inline-chat.
    
    [![Screenshot of selection code chat debugging.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/selection-code-chat-debugging.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/selection-code-chat-debugging.png#lightbox)
    
    For example, you might ask, "I'm getting a `NullReferenceException` in this method. Can you help me debug it?"
    
    ![Screenshot of generating code chat debugging.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/generating-code-chat-debugging.png)
    
- **Code explanations** Copilot Chat can also be used to better understand complex code snippets. It can break down code into simpler terms, explain the purpose and functionality of unfamiliar code, and offer insights into best practices and potential optimizations. For example, you could ask: - "Can you explain how this async/await code works in Python?"
    
    [![Screenshot of chat code explanations.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-code-explanations.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-code-explanations.png#lightbox)
    

#### How to improve GitHub Copilot Chat responses

You can significantly improve the quality and relevance of GitHub Copilot Chat's responses with certain key features. Let's dive into them.

##### Scope referencing

To enhance the accuracy and relevance of the responses provided by GitHub Copilot Chat, it’s important to properly scope your questions using references. Here’s how you can do that:

- **File references:** You can specify a particular file in your question by adding a `#file:` before the file name.
    
    [![Screenshot of chat scope file referencing pick.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-scope-file-referencing-pick.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-scope-file-referencing-pick.png#lightbox)
    
    For example, if you’re working with a file named `controller.js`, you can use the #file command to select it and reference it directly in your question as `#file:controller.js`. This tells Copilot Chat to focus on the contents of that file when generating a response.
    
    [![Screenshot of chat scope file referencing.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-scope-file-referencing.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-scope-file-referencing.png#lightbox)
    
- **Environment References:** You can reference the entire solution or workspace by using `@workspace`. This allows Copilot Chat to consider the broader context of the projects and configurations that are currently open in your Visual Studio IDE. For instance, asking "@workspace where is the calculate function?" will prompt Copilot to consider the entire solution to find the most relevant information.
    
    [![Screenshot of chat scope workspace referencing.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-scope-workspace-referencing.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/chat-scope-workspace-referencing.png#lightbox)
    

##### Slash commands

Slash commands in GitHub Copilot Chat allow you to quickly specify the intent of your query. This can significantly improve the quality of the responses you receive by making your requests more focused. Here are some commonly used slash commands:

- **/doc:** Adds comments to the specified or selected code. For example, you can type `/doc` followed by the code you want to document, and Copilot will generate appropriate comments.
    
    [![Screenshot of /doc slash commands.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/doc-slash-commands.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/doc-slash-commands.png#lightbox)
    
- **/explain:** Provides explanations for selected code. This is particularly useful when you need to understand what a particular piece of code does. For example, `/explain the #file:controller.js` will give you a detailed explanation of that file.
    
    [![Screenshot of /explain slash commands.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/explain-slash-commands.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/explain-slash-commands.png#lightbox)
    
- **/fix:** Proposes fixes for problems in the selected code. If you're facing issues, you can highlight the problematic section and use `/fix` to receive suggestions for resolving the issue.
    
    [![Screenshot of /fix slash commands.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/fix-slash-commands.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/fix-slash-commands.png#lightbox)
    
- **/generate:** Helps in generating new code based on your requirements. For example, `/generate code to find the root of a number in client.js` will create a function to perform the task.
    
    [![Screenshot of /generate slash commands.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/generate-slash-commands.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/generate-slash-commands.png#lightbox)
    
- **/optimize:** Analyzes and suggests improvements to the running time or efficiency of the selected code. For instance, `/optimize the` calculate `method in controller.js` will focus on enhancing the performance of that specific method.
    
    [![Screenshot of /optimize slash commands.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/optimize-slash-commands.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/optimize-slash-commands.png#lightbox)
    
- **/tests:** Automatically creates unit tests for the selected code. You can simply highlight the code and use `/tests using Mocha` to generate tests.
    
    [![Screenshot of /tests slash commands.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/tests-slash-commands.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/tests-slash-commands.png#lightbox)
    

##### Copilot agents

GitHub Copilot agents are custom tools that you can build and integrate with GitHub Copilot Chat to provide additional functionalities tailored to your specific needs. In addition to slash commands, you can use specific agents within Copilot Chat in your IDE to handle different tasks:

- **@workspace:** This agent allows you to extend the context of whatever questions you ask Copilot to the whole project. It is very useful for getting code generated that would fit in your project right away, using information from your whole project. It can also be utilized for getting answers about your whole codebase.
    
    [![Screenshot of `@workspace` agent command.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/workspace-agent-command.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/workspace-agent-command.png#lightbox)
    
    You can also use the “@workspace /new” smart action which allows you to generate a completely new project from scratch based on your requirements. For example, “@workspace /new generate new html file pages and javascript for advanced calculations“
    
    [![Screenshot of  `@workspace \new` agent command.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/workspace-new-agent-command.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/workspace-new-agent-command.png#lightbox)
    
    Click on “Create Workspace” to proceed with code generation and just like that you have your new project with the code you requested.
    
    [![Screenshot of new generated workspace project.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/new-generated-workspace-project.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/new-generated-workspace-project.png#lightbox)
    
- **@terminal:** This agent is useful for command-line related questions. For example, you could ask it to find the largest file in a directory or explain the last command you ran.
    
    [![Screenshot of `@terminal` agent command.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/terminal-agent-command.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/terminal-agent-command.png#lightbox)
    
- **@vscode:** Use this agent to ask questions related to Visual Studio Code, such as how to debug or change settings within the IDE.
    
    [![Screenshot of `@vscode` agent command.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/vscode-agent-command.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/vscode-agent-command.png#lightbox)
    
    By effectively utilizing these tools and techniques, you can significantly improve the quality of responses you receive from GitHub Copilot Chat, making your coding experience more efficient and productive.
    

##### Sharing feedback on GitHub Copilot Chat

Most IDEs with Copilot Chat integration have built-in feedback mechanisms. For example, in VS Code, you can find feedback options at the beginning of GitHub Copilot Chat's suggestions. Hover over a suggestion, and you should see thumbs up and thumbs down buttons.

![Screenshot of thumbs up helpful buttons.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/thumbs-up-helpful-buttons.png)

Click on the thumbs up to rate a suggestion as helpful.

![Screenshot of thumbs down unhelpful.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/thumbs-down-unhelpful.png)

Click on thumbs down to rate an unhelpful one.

### GitHub Copilot for the Command Line

GitHub Copilot isn't just a tool for writing code in your favorite IDE; it’s also a powerful assistant that can help streamline your command-line workflows. By integrating with the GitHub CLI, Copilot can provide explanations for unfamiliar commands, suggest commands based on your needs, and even execute them on your behalf. Whether you're new to the command line or a seasoned user, Copilot can enhance your productivity by offering intelligent suggestions and simplifying complex tasks.

#### Common commands

Once you have Copilot set up in the CLI, here are some frequently used commands for interacting with it:

- **Getting command explanations**:
    
    - If you're unsure about what a specific command does, you can ask Copilot to explain it. For instance:
        
        ```shell
        gh copilot explain "sudo apt-get"
        ```
        
        ![Screenshot of copilot explain in cli.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/copilot-explain-in-cli.png)
        
        This command provides you with a detailed explanation of the provided command.
        
- **Getting command suggestions**:
    
    - Need help with constructing a command? You can ask Copilot to suggest a command based on what you want to accomplish:
        
        ```shell
        gh copilot suggest "Undo the last commit"
        ```
        
        ![Screenshot of copilot suggest in cli.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/copilot-suggest-in-cli.png)
        
        Copilot starts an interactive session to clarify your request and suggest the best command.
        
- **Executing suggested commands**: After receiving a suggestion, you can choose the `Execute command` option. This copies the command to your clipboard. You can also allow Copilot to execute commands on your behalf only if you configure the `ghcs` alias:
    
    ```
    ghcs suggest "What command to see running docker containers"
    ```
    
    [![Screenshot of executing suggested command copilot suggest in cli.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/executing-suggested-command-copilot-suggest-in-cli.png)](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/executing-suggested-command-copilot-suggest-in-cli.png#lightbox)
    
- **Revise suggested command**: To give GitHub Copilot CLI to rework or revise a command to make it better or more suited to your expectations, use the "Revise command" option along with your feedback.
    
    ![Screenshot of revising suggested command copilot suggest in cli.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/revising-suggested-command-copilot-suggest-in-cli.png)
    

#### Configuration options

To make the most out of Copilot in the CLI, you may want to configure certain settings:

- **Alias Configuration**: If you want Copilot to execute commands on your behalf directly, you need to set up the `ghcs` alias. Using an alias allows you to bypass copying and pasting commands manually, and instead Copilot does it for you.
    
    To configure the `ghcs` alias, run the following commands:
    
    For bash:
    
    ```bash
    echo 'eval "$(gh copilot alias -- bash)"' >> ~/.bashrc
    ```
    
    For PowerShell:
    
    ```powershell
    $GH_COPILOT_PROFILE = Join-Path -Path $(Split-Path -Path $PROFILE -Parent) -ChildPath "gh-copilot.ps1"
    gh copilot alias -- pwsh | Out-File ( New-Item -Path $GH_COPILOT_PROFILE -Force )
      echo ". `"$GH_COPILOT_PROFILE`"" >> $PROFILE
    ```
    
    For Mac terminal or Zsh:
    
    ```Zsh
    echo 'eval "$(gh copilot alias -- zsh)"' >> ~/.zshrc
    ```
    
- **Feedback mechanism**: Copilot encourages user feedback to improve its suggestions. You can rate the quality of a suggestion by selecting the `Rate response` option after Copilot provides you with a command.
    
    ![Screenshot of rating suggested command copilot suggest in cli.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/rating-suggested-command-copilot-suggest-in-cli.png)
    
- **Organizational settings**: If you're using Copilot within an organization your access to certain features may be governed by your organization's policies. Administrators can enable or disable Copilot's capabilities within the CLI.
    
    For further customization and detailed configuration so you can optimize Copilot's functionality for your specific needs, refer to the [GitHub documentation](https://docs.github.com/en/copilot).
    
- **Data handling**: GitHub Copilot CLI doesn't retain your prompts, but it keeps your usage analytics. You can configure whether you want GitHub Copilot to keep and use your usage data to improve the product. Enter the command `gh copilot config` , select "Optional Usage Analytics", then select "No" if you want to opt out.
    
    ![Screenshot of configure usage data setting in cli.](https://learn.microsoft.com/en-us/training/github/github-copilot-across-environments/media/configure-usage-data-setting-in-cli.png)

## Management and customization considerations with GitHub Copilot
### Introduction
At GitHub, we're committed to advancing safe, secure, and trustworthy AI. We believe in the power of AI to enhance efficiency and innovation across the software development life cycle to increase developer happiness. GitHub continues to ensure that AI advancements are accessible and beneficial to all.

### Explore GitHub Copilot plans and their associated management and customization features
GitHub enables developers and organizations to maximize their potential by prioritizing security, privacy, compliance, and transparency as we develop, iterate, and innovate GitHub Copilot.

Every developer and organization has specific needs. That's why GitHub Copilot has several pricing plans.
#### Management policy features

|Feature|Free* & Pro|Business|Enterprise|
|---|---|---|---|
|Public code filter|✅|✅|✅|
|User management|❌|✅|✅|
|Data excluded from training by default|❌|✅|✅|
|Enterprise-grade security|❌|✅|✅|
|IP indemnity|❌|✅|✅|
|Content exclusions|❌|✅|✅|
|SAML SSO authentication|❌|✅|✅|
|Require GitHub Enterprise Cloud|❌|❌|✅|
|Usage metrics|❌|✅|✅|

*GitHub Copilot Free has usage limitations

#### Customization features

|Feature|Free* & Pro|Business|Enterprise|
|---|---|---|---|
|Tailor chat conversations to your private codebase|❌|❌|✅|
|Unlimited integrations with Copilot Extensions (public beta)|✅|✅|✅|
|Build a private extension for internal tooling (public beta)|✅|✅|✅|
|Attach knowledge bases to chat for organizational context|❌|❌|✅|

*GitHub Copilot Free has usage limitations

When you're selecting a GitHub Copilot pricing plan, you and your organization should consider these key factors:

- **Data privacy and security**: The plans offer varying levels of data privacy and security measures. For instance, GitHub Copilot Business and Enterprise are the only plans that provide more robust privacy controls. These controls include the ability to exclude specific files from GitHub Copilot analysis, access detailed audit logs, and provide IP indemnity.
- **Policy management**: The ability to manage Copilot policies at an organizational level is crucial. Business and Enterprise plans allow for comprehensive policy management, to help ensure that sensitive data is handled according to the organization's privacy policies.
- **Data collection and retention**: Understanding how data is collected and retained is essential for compliance with data privacy regulations. Individual subscribers can choose whether GitHub collects and retains their prompts and Copilot suggestions.
- **IP indemnity and data privacy**: For businesses and enterprises, IP indemnity and data privacy are critical to avoiding legal, security, and customer issues. Evaluating the need for these features can help determine the most suitable pricing plan for your business.

 >**Tip**: GitHub Copilot offers a free tier with **2,000 code autocompletes and 50 chat messages per month**. To get started, open Visual Studio Code, click on the GitHub Copilot icon, and then click "Sign in to Use GitHub Copilot for Free". Log in to your GitHub account in the window that will open in the browser. [Learn more](https://gh.io/copilot). Educators, Students and select open-source maintainers can receive Copilot Pro for free, learn how at: [https://aka.ms/Copilot4Students](https://aka.ms/Copilot4Students).
 
### Explore contractual protections in GitHub Copilot and disabling matching public code

![Screenshot of a futuristic, neon-colored depiction of GitHub Copilot represented as a stylized robotic helmet.](https://learn.microsoft.com/en-us/training/github/github-copilot-management-and-customizations/media/git-hub-copilots-contractual-protections.png)

"Screenshot of a futuristic, neon-colored depiction of GitHub Copilot represented as a stylized robotic helmet. Copilot is portrayed alongside abstract graphics of orbs and atomic-like structures. The text of GitHub Copilot's contractual protections is in bold white at the bottom."

To help ensure that your organization remains compliant with legal requirements, you should understand how contractual protections and GitHub Copilot features can help safeguard your code and data.

#### Contractual protections

To help ensure that your organization remains compliant with legal requirements, GitHub Copilot offers:

- **IP indemnity**: The GitHub Copilot Business and Enterprise plans include IP indemnity, which provides legal protection against intellectual property claims related to the use of Copilot suggestions. With IP indemnity, if any suggestion from GitHub Copilot is challenged as infringing on third-party IP rights, GitHub assumes legal responsibility. For GitHub to assume legal responsibility, the **Matching public code** setting must be blocked.
- **Data Protection Agreement (DPA)**: GitHub offers a DPA that outlines the measures taken to protect your data and ensure compliance with data privacy regulations. These agreements provide transparency and assurance that your data is handled securely and responsibly.
- **GitHub Copilot Trust Center**: The GitHub Copilot Trust Center provides detailed information about how GitHub Copilot works, including security, privacy, compliance, and intellectual property safeguards. This resource helps organizations feel confident using GitHub Copilot while adhering to best practices and legal requirements.

#### Filtering out matching public code

GitHub Copilot can help minimize potential code overlap by identifying and filtering out code suggestions that match publicly available code. This feature is essential for maintaining the originality and security of your codebase. It can reduce the risk of incorporating nonsecure or noncompliant code into your projects.

To block suggestions that match public code:

1. On the upper-right corner of any page on GitHub, select your profile photo, and then select **Your enterprises** or **Your organizations**.
    
2. Next to the enterprise or organization, select **Settings**.
    
3. On the left sidebar, select **Copilot**.
    
4. Under **Suggestions**, select **Matching public code** on the dropdown menu, and then select **Block**.
    
5. To confirm your new settings, select **Save**.

### Manage content exclusions

The content exclusion feature in GitHub Copilot helps protect sensitive information by preventing the use of specific files, directories, or repositories to inform code-completion suggestions.
#### Configurations for content exclusion

To implement content exclusion strategies, repository administrators and organization owners can use the following configurations.

##### Configure content exclusions for repositories

1. On GitHub, go to the main page of the repository.
    
2. Under the repository name, select **Settings**.
    
3. In the sidebar, in the **Code & automation** section, select **Copilot**.
    
4. In the **Repositories and paths to exclude** section, specify the files or directories to exclude from Copilot suggestions.
    

##### Configure content exclusions for organizations

1. In the upper-right corner of GitHub, select your profile photo, and then select **Your organizations**.
    
2. Next to the organization, select **Settings**.
    
3. On the left sidebar, select **Copilot** > **Content exclusion**.
    
4. Enter the details of files or repositories to exclude from Copilot suggestions.
    

#### Impact of content exclusion on code suggestions

You can use content exclusions to configure GitHub Copilot to ignore certain files. When you exclude content from GitHub Copilot:

- Code completion is no longer available in the affected files.
- The content in affected files won't inform code completion suggestions in other files.
- The content in affected files won't inform GitHub Copilot Chat responses.

Content exclusions can significantly affect the quality and relevance of code suggestions that GitHub Copilot generates. When you exclude certain files or directories, GitHub Copilot won't use the content in those files to inform its suggestions. This action can lead to more secure and compliant code suggestions, but it might also reduce the overall context available to GitHub Copilot. This reduction could potentially affect the accuracy and usefulness of the suggestions.

For example, excluding a critical configuration file might prevent Copilot from suggesting relevant code snippets that depend on the configurations defined in that file. It's essential to carefully analyze which files should be excluded to balance security and functionality.

You can specify content exclusions only in the settings for an organization or repository. Content exclusion settings that are defined in an organization or repository within an enterprise apply to all members who are licensed as part of a GitHub Copilot Business or GitHub Copilot Enterprise subscription.

#### Limitations of content exclusions

Although content exclusions are a valuable tool for managing privacy and security, they might not be fully effective in some scenarios. For instance:

- **IDE limitations**: In some integrated development environments (IDEs), content exclusions might not apply when you're using certain features, such as Copilot Chat. For example, in Visual Studio Code and Visual Studio, content exclusions are not applied when you use the `@github` chat participant in your question.
- **Semantic information**: Copilot might still use semantic information from an excluded file if the IDE provides the information in a nonexcluded file. This includes type information and hover-over definitions for symbols or function calls used in code.
- **Policy scope**: Content exclusion settings apply only to members of the organization in which you configure the content exclusion. Anyone else who can access the specified files can still see code completion suggestions and Copilot Chat responses referencing the specified files.

Understanding these limitations is crucial for effectively managing content exclusions and ensuring that sensitive information is adequately protected.

### Troubleshoot common problems with GitHub Copilot

#### Code suggestions are missing

One of the most common problems that users encounter with GitHub Copilot is the absence of code suggestions. If Copilot isn't providing code suggestions in your editor, try these troubleshooting actions:

- **Check your internet connection**: Ensure that you have a stable internet connection, because GitHub Copilot requires an active connection to function properly.
- **Update the Copilot extension**: Make sure you're using the latest version of the GitHub Copilot extension. Older versions might not communicate effectively with the Copilot servers.
- **Verify IDE compatibility**: Confirm that your IDE is compatible with GitHub Copilot. Some IDEs might require specific configurations or updates to work with Copilot.
- **Review content exclusions**: If certain files are excluded from a Copilot analysis, suggestions might not appear for those files. Check the content exclusion settings to ensure they're configured correctly.

By taking these actions, you can often resolve problems related to missing code suggestions and ensure that Copilot functions as expected.

#### Content exclusions aren't working as expected

Content exclusions are designed to prevent GitHub Copilot from using specific files or directories. However, content exclusions might not work as expected in some scenarios. Here are some common problems and their resolutions:

- **Delayed application of exclusions**: After you add or change content exclusions, the changes can take up to 30 minutes to take effect in IDEs where the settings are already loaded. To apply changes immediately, reload the content exclusion settings in your IDE.
    
- **Inadequate scope of exclusions**:
    
    - Content exclusion settings apply only to members of the organization in which you configured the exclusion. Ensure that all relevant team members have the appropriate settings applied.
        
    - Check the GitHub Copilot icon on the status bar. If a GitHub Copilot content exclusion applies to the file, the GitHub Copilot icon has a diagonal line through it. Hover over the icon to see whether an organization or the parent repository disabled GitHub Copilot for the file.
        
- **IDE-specific limitations**: In some IDEs, content exclusions might not apply when you're using certain features, such as GitHub Copilot Chat. Be aware of these limitations and adjust your workflow accordingly.
    

By understanding and addressing these problems, you can ensure that content exclusions are applied effectively and help protect sensitive information.

#### Code suggestions are unsatisfactory

If the suggestions that GitHub Copilot is generating are unsatisfactory, you can use these techniques to prompt Copilot to provide better results:

- **Provide clear context**: Ensure that your code provides clear context for GitHub Copilot to generate relevant suggestions. This task includes writing descriptive comments and using meaningful variable names.
- **Use Copilot commands**: In some IDEs, you can use specific commands to prompt Copilot to generate suggestions. For example, in Visual Studio Code, you can use the Ctrl+Enter shortcut to trigger GitHub Copilot.
- **Adjust prompt length**: Sometimes, providing a longer or more detailed prompt can help Copilot generate better suggestions. Experiment with different prompt lengths to see what works best.

By using these techniques, you can improve the quality of GitHub Copilot suggestions and enhance your coding experience.