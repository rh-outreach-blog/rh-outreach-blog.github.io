---
layout: page
title: Exercise 2
permalink: /git-guide-2/
---

This guide will allow you to put the learning from lessons 4 - 6 into practice. It will walk you through the process of:

* Opening a new branch and making changes there
* Stashing these changes to safely switch branches
* Rebasing your branch to tidy your commit history

This exercise operates on the expectation that you have completed exercise 1, if not, please do so and return to this guide.

---
## Stashing changes

1. Within your IDE, open the project directory and enter the following in your integrated terminal:
    ``` bash
    git checkout -b exercise-2 # this will create and switch to a new branch for this exercise
    ```

2. Let's make a change to this branch. Add the text "This is a test" to the README file via your IDE or simplt enter:
    ``` bash 
    echo -e "\n    This is a test" >> README.md
    ```

3. Save your change then enter:
    ``` bash
    git add . # this will add all of the changed files within the current directory to staging
    ```

4. Next we'll commit this change by entering:
    ``` bash
    git commit -m "This is the first change"
    ```

5. Verify the presence of this commit by entering:
    ``` bash
    git log
    ```

6. Let's make a second change:
    ``` bash
    echo -e "\n    This is the second test" >> README.md
    ```

7. Hit save but do **NOT** add this change to staging.

8. Now we will attempt to move back to our main branch:
    ``` bash
    git checkout main
    ```
    This should result in an error:
    ``` bash
        error: Your local changes to the following files would be overwritten by checkout:
            README.md
    Please commit your changes or stash them before you switch branches.
    Aborting
    ```
9. Let's stash the uncommited changes before switching to main:
    ``` bash
    git stash
    ```
    Then:
    ``` bash
    git checkout main
    ```
10. You should observe that the changes made in your branch are not reflected in main. Let's switch back to our test branch:
    ``` bash
    git checkout exercise-2
    ```

11. Now we can continue on our stashed changes by entering:
    ``` bash
    git stash apply
    ```

12. Let's commit the changes:
    ``` bash
    git commit -m "This is the second change"
    ```

---
## Rebasing

1. Let's examine our current git log:
    ``` bash
    git log
    ```
It should resemble the following image:

    ![git log](/images/git-log.png)

2. Let's imagine we'd made several more changes for a review for example. Ideally, we would like to preserve a neat commit history when working on branches. Let's attempt to rebase to facilitate this.

3. In the log, we can observe that it's the two most recent commits we want to adjust. Enter the following:
    ``` bash
    git rebase -i HEAD~2 # -i is the flag for "interactive" and "HEAD~2" specifies the 2 most recent commits on the HEAD
    ```

4.  This will open an interactive nano window within your terminal. It should resemble the below screenshot:

    ![rebase](/images/rebase.png)

    The instructions within should be self explanatory but in this case we want to squash the second commit into the first one.

5. Change the word **"pick"** next to the second commit to **"squash"**. You can also use single letters as outlined within the nano file. Use **ctrl+x** to save and then confirm to perform the rebase.

6. You will then be presented with an additional nano view where you can see both commit messages. In this view, remove the second commit message and corresponding comment.

7. Change the remaining commit message to: **"This is the combined commit"** and save.

8. To verify the rebase run:
    ``` bash
    git log
    ```

9. The output should be similar to the below screenshot:

    ![post rebase](/images/post-rebase.png)
        
    We've now successfully combined both commit and changed the message to reflect this.

10. Finally, let's push these changes to a remote branch:
    ``` bash
    git push origin exercise-2 --force-with-lease # we don't need this here but normally would if the remote branch had commits
    ```






