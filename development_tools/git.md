# Getting Started with Git

Make sure you have Git installed on your system (e.g., by running `sudo apt install git -y` on Linux) and that you have a working account with a Git host (GitLab or GitHub) before following the instructions below.

## Clone a Repository

If you've accepted an invitation to a private Git repository or have access to the address of a public one, you can clone the remote repository to your local machine (consider creating a projects folder first for better organization).

To communicate with the remote repository from your local machine, you can either use the **SSH (Secure Shell)** protocol by generating key pairs, or generate a **personal access token (PAT)** as a password replacement when using the **HTTPS** protocol.

Access tokens allow finer control over repository access (e.g., read-only, write-only, etc.).

### When Using a Personal Access Token (PAT)

***(See the general SSH setup section if you're configuring SSH keys instead.)***

Git will prompt for authentication. Use your GitHub/GitLab username as the username, and use the PAT instead of your password.

To generate a PAT on GitHub:

Go to `Settings > Developer settings > Personal Access Tokens > Tokens (classic) > Generate new token`

**Clone the repository using HTTPS (not SSH):**

- `git clone https://github.com/your-user/your-repo.git`


Cloning must be done using the HTTPS URL when using a PAT — not the SSH one.

Git will ask for your credentials:

- **Username**: your GitHub/GitLab username

- **Password**: your generated Personal Access Token


To store your credentials for future Git operations and avoid repeated prompts, run:

- `git config --global credential.helper store`


If you've done this, Git will store your username and PAT for all future operations.

If needed, you can view the stored token (if saved this way) using:

`cat ~/.git-credentials`


***Note: Personal Access Tokens are tied to your account, not a specific repository.***

After cloning, the repository should appear in your current working directory. You can open it in VS Code with:

- `cd repo_name`
- `code .`


If `code .` doesn't work immediately, type exit to close the current terminal, open a new one, and try again (Terminal > New Terminal in VS Code).


## Configure Your Identity for Commits

Open a suitable terminal (CMD, PowerShell, or your IDE terminal) and set up your Git identity:

- `git config --global user.name "Your Name"`
- `git config --global user.email "your_email@example.com"`


The `--global` flag sets your identity for all repositories on the system under your user account (saved in ~/.gitconfig).

If you need different identities for different repositories (e.g., work vs. personal email), you can override the global settings locally:

- `cd your-repo`
- `git config user.name "Work Name"`
- `git config user.email "work_email@example.com"`


You can verify which settings are active using:

- `git config --list --show-origin`


### Essential Git Commands

In order to set up and maintain a proper project structure with 
Git, have a look at the following "cheat sheets" and documentations:

- [Long Cheat Sheet by geeksforgeeks](https://www.geeksforgeeks.org/git/git-cheat-sheet/) 
- [Short Cheat Sheet by GitLab](https://about.gitlab.com/images/press/git-cheat-sheet.pdf) 
- [Stackoverflow Post on Deleting Branches](https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-locally-and-remotely/23961231#23961231) 
- [Stackoverflow Post on Commits and Merging](https://stackoverflow.com/questions/63745370/git-shows-there-is-no-difference-but-files-are-different-and-upon-merging-those)
- [Basics of Working with Remotes](https://git-scm.com/book/de/v2/Git-Grundlagen-Mit-Remotes-arbeiten)
- [Preview a Merge in Git](https://stackoverflow.com/questions/5817579/how-can-i-preview-a-merge-in-git)
- [Fetch vs. Pull](https://about.gitlab.com/blog/git-pull-vs-git-fetch-whats-the-difference/)

  **Concise Summary**:

  *Safer Option*:

  `git fetch origin`

  `git checkout local_branch`

  `git diff origin/local_branch` # check for differences between local version and remote-tracking branch before merge

  `git merge origin/local_branch`

  *Quick Option*:

  `git checkout local_branch`

  `git pull origin local_branch` # combines fetch from remote origin with merge to local_branch > risk of possible conflicts
