# Git

## Workflow

### Pushing Changes

1. Create Repository on GitHub

2. in command line, go to directory where you want repo to be then run code:

   ```
   echo "# TestRepo1" >> README.md
   git init
   git add README.md
   git commit -m "first commit"
   git branch -M main
   git remote add origin https://github.com/pjmlearner/TestRepo1.git
   git push -u origin main
   ```

3. Initialize -  `git init`

4. Status - `git status` 

5. Staging - `git add [filename]`

6. Commit - `git commit -m "[message]"`

7. Push Changes - `git push [git repo url address]`

### Pull new files from Repo

1. Pull -`git pull [git repo url address]`

test1