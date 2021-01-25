# pythontrail
TicTacToe Game 

However, moving forward, a few things will change about this process, namely the branches we push to, and the commands we enter. As far as the commands go, we're going to add two more into the mix, `git log` and `git diff`. You may have used or seen these commands before, but at a glance, `git log` gives you a summary of the past commits relative to the branch you're currently on, and `git diff` shows you what changes you have made since the previous commit. Our new process should look something like this:

```
git log
git status
git diff
git add .
git commit -m 'a helpful message'
git push origin master
```

## Branching Workflow

Today, we're going to make an application to store who the best IA for our cohort is. However, because of the fact that this is a hotly debated topic, we're going to make two branches with differing opinions and create a merge conflict.

The commands should look something like this:

```sh
# first we'll clone down a remote repo
git clone https://git.generalassemb.ly/sei-nyc-bees/advanced-git

# we'll create a file and make some changes in it
touch best-ia.js

# we'll add and commit our changes
git add .
git commit -m 'create best-ia file'

# we'll create our first branch
git checkout -b feature/tara

# we'll return to master
git checkout master

# and then create our second branch
git checkout -b feature/corey

# we'll return to feature/tara to make our first change
git checkout feature/tara

# we'll make a change in this file, and then add and commit our work
git add .
git commit -m 'added tara as best IA'
git push origin feature/tara

# we'll return to feature/tara to make our first change
git checkout feature/corey

# we'll make a change in this file, and then add and commit our work
git add .
git commit -m 'added corey as best IA'
git push origin feature/corey
```

## Merging Workflow

Now that we've created our branches, it's time to merge them in.

```sh
# let's return to master to merge our branches in
git checkout master

# let's first merge in tara's branch, this should go off without a hitch
git merge feature/tara

# next, let's merge corey's branch
git merge feature/corey

# we now have a merge conflict! let's put the two bestIAS into a new array and solve it within the file. once we finish this, let's add and commit our work so far
git add .
git commit -m 'solve merge'
git push origin master
```

## Lab

Now let's do the same thing in groups of three.

Steps:
1. Pick one person to be the Git Maintainer. 
1. Your Maintainer will create a repository and add the other group members as collaborators.
1. Within Github, add a branch called develop and set it to be the default branch. 
    - On GitHub Enterprise, navigate to the main page of the repository.
    - Under your repository name, click Settings.
    - In the left menu, click Branches.
    - In the default branch sidebar, choose the new default branch.
1. Everyone: clone down the repository. 
1. Maintainer: create a file called `best-student.js` with the following content:

    ```js
    console.log('Here is the best student!');
    ```
1. The Maintainer will then add, commit, and push the changes to `origin develop`.
1. After this, each member will run `git pull origin develop` to get the change Maintainer has just made.
1. Upon pulling the develop branch, each group member will create a feature branch with their name, such as `feature/bruno`. As a general note, *do not name a branch with your name in your projects*. This exercise is an exception, as the feature we're integrating is creating a variable to represent the best student, with your name as the value.
1. After creating the new branch, each member should add a variable called `bestStudent` with their name as the value.
    ```js
    const bestStudent = 'soleil';
    ```
1. After adding this line, navigate back to the terminal, and add and commit your work, and push to your remote.
    ```sh
    git add .
    git commit -m 'your commit message here'
    # if your name is soleil for example, this command would be:
    # git push origin feature/soleil
    git push origin feature/your-name-here
    ```
1. Once all group members have pushed to the remote, the Maintainer should pull down all these branches, using the `git pull` command with the name of the remote (`origin`) and the branch name, i.e. `git pull origin feature/bruno`.
1. Once the branches have been pulled down, the Maintainer should checkout back to the master branch (`git checkout master`), and begin merging the branches one by one (`git merge feature/name-of-branch`).
10. Once a merge conflict arises, replace the `bestStudent` variable with an array containing each member whose name you merge in.
    ```js
    console.log('Here is the best student!');

    const bestStudents = ['corey', 'tara', 'jordan'];
    ```
1. After each merge, make sure to add and commit your work to merge the changes in.
1. Once the Maintainer has finished merging all the branches, push up the updated master branch to your remote.
1. Celebrate with a bottle of champagne to share amongst your group, for you have triumphed over Git! Let's take a look at the changes we've made by running a fancy version of git log: `git log --all --decorate --oneline --graph`. We can call this git log adog for mnemonics' sake. This will give us a full tree view of our commits that we've done, relative to our current branch.
