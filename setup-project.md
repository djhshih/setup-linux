## Setup project with git
Before setting up your project with git, determine which of the following options fit your situation:
1. Connect an existing repository on github to the local computer/sever.
2. Connect an existing project on local computer/sever to github.
and refer to the corresponding section.

Regardless of which options, you will need to the SSH URL specification.

### 0. Get the SSH URL specification
1. Go to your existing repository on [github](https://github.com/)
2. SSH URL specification have the format: `git@github.com:<username>/<repository_name>.git`
3. Copy the SSH URL specification
    - if it is an empty repository, simply click `SSH` and then copy the SSH URL.
- if it is an existing repository, click `Code` (the green button) and then `SSH`, and copy the SSH URL.

### 1. Connect an existing repository on github to the local computer/sever.
1. Copy the SSH URL specification (i.e, `git@github.com:<username>/<repository_name>.git`), refer to section "0. Get the SSH URL specification"
3. Now that you have copied the SSH URL, in terminal, go to the directory in which you want your project to locate.
4. Run `git clone <SSH_URL>`. (ex. `git clone git@github.com:bob123/test_repo.git`)
5. Enter passphrase for key in the password prompt.
6. Done.

### 2. Connect an existing project on local computer/sever to github.
1. Copy the SSH URL specification (i.e, `git@github.com:<username>/<repository_name>.git`), refer to section "0. Get the SSH URL specification"
2. In terminal, locate to your existing project directory. *should be the root folder of the existing project.*
3. Run `git init`.
4. Run `git add <filename>` to select files to be add to the git repo.
5. Run `git commit -m <message>` to add a message correspond to the files you added.
6. Run `git remote add origin <SSH_URL>`.
    - ex. `git remote add origingit@github.com:bob123/test_repo.git`
7. Run `git push --set-upstream origin HEAD:main`. This will push the added files to github as well as changing the HEAD pointer from master to main.
8. Enter passphrase for key in the password prompt.
9. Done.

Ask for GitHub repo to be setup.

Remote:
git clone


Workflow
local: git push
remote: git pull

