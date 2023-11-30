## Setup project with git
There are two ways to connect GitHub repository and local computer/sever:
1. Connect an existing repository on GitHub to a local computer/sever.
2. Connect an existing project on local computer/sever to a GitHub repository.

Both ways required the SSH URL specification.

### 0. Get the SSH URL specification
0. Ask for GitHub repo to be setup.
1. Go to an existing repository on [GitHub](https://github.com/)
2. Copy the SSH URL specification
    - SSH URL specification should have the format: `git@github.com:<username>/<repository_name>.git`
    - if it is an empty repository, simply click `SSH` and then copy the SSH URL.
    - if it is an existing repository, click `Code` (the green button) and then `SSH`, and copy the SSH URL.

### 1. Connect an existing repository on GitHub to the local computer/sever.
1. Copy the SSH URL specification (i.e, `git@github.com:<username>/<repository_name>.git`), refer to section "0. Get the SSH URL specification"
3. In terminal, go to the directory in which you want your project to locate.
4. Run `git clone <SSH_URL>`. (ex. `git clone git@github.com:bob123/test_repo.git`)
5. Enter passphrase for key in the password prompt.
6. Done.

### 2. Connect an existing project on local computer/sever to GitHub.
1. Copy the SSH URL specification (i.e, `git@github.com:<username>/<repository_name>.git`), refer to section "0. Get the SSH URL specification"
2. In terminal, go to your existing project directory.
3. Run `git init`. *note that this should be the root directory of the existing project.*
4. Run `git add <filename>` to select file to be add to the git repo.
5. Run `git commit -m <message>` to create a commit and add comments on the commit.
6. Run `git remote add origin <SSH_URL>`.
    - ex. `git remote add origin git@github.com:bob123/test_repo.git`
7. Run `git push --set-upstream origin HEAD:main`. This will push the added files to github as well as changing the HEAD pointer from master to main.
8. Enter passphrase for key in the password prompt.
9. Done.


## Push/Pull between GitHub repository and local/sever repository

### From GitHub repository to local/sever repository
You will be "pulling" content from the GitHub repository to local/sever repository.
1. Run `git pull` in the local/sever repository. *Note that this local/sever repository should be connected to a GitHub repository already*

### From local/sever repository to GitHub repository
You will be "pushing" content from the local/sever repository to the GitHub repository.
1. Run `git add <file>` to "select" the file that you would like to add to the GitHub repository.
2. Run `git commit -m "<message>"` to create a commit and add comments on the commit.
3. Run `git push` to send the commits and updates GitHub.
4. Done.
