Git Visualization Tutorial: Manipulating the Local Repo
=======================================================
-------------


As you all may know, GitHub is a very powerful version control tool.  However, it seems that most students only know the bare minimum functions for making through the CS curriculum.  GitHub provides a variety of other tools that make the version control process as fluid and convenient as possible.

This tutorial will focus on manipulating the local repository as most students understand how to use `git push` and `git pull`.  The additional remote functions such as `git fetch` or miscellaneous arguments for pulling or pushing are not as important to learn.


## (Re)Learning The Basics
-------------
 
### Commit
As the majority of the readers may know, committing to a repository is essentially taking a snapshot of the current state of the directory and recording it in the repository.  Imagine you have just cloned a repository which will be depicted as the `R0` circle below.

<img src="https://github.com/mliao95/MShistory/blob/master/Images/1.JPG" align="left" height="70" width="119" ><br><br>
<br>
<br>

When we have made changes to files in the directory and want to update our local repository, we type `git commit <filename>` to commit one file or `git commit -a` to commit all tracked files.  After committing to the repo, we create another circle, `R1`, which contains all the changes we made from `R0`.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/2.JPG" align="left" height="160" width="120" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>




The new node represents the most updated node in the repository, and our `master` branch is moves from `R0` to `R1`.

### Branching

Branching might be one of the most useful yet underused tool in the GitHub arsenal.  Branches are essentially just a series of pointers with the `master` branch being the default pointer.  Let's create a new branch called `newBranch` by typing `git branch newBranch`.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/3.JPG" align="left" height="160" width="130" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>

As you can see, a new branch is created at our pointer which is represented as the `*`.  However, our pointer is still on `master`.  Let's see what happens when we make changes and type `git commit`.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/4.JPG" align="left" height="210" width="150" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

As you can see, our pointer is on `master` which is now moved to `R2`, but our new branch, `newBranch` is still on `R1`.  This happens because we are still pointing to `master`.  Let's move our pointer to `newBranch` with `git checkout newBranch`.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/5.JPG" align="left" height="210" width="150" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Now if we make some changes, it will be from the `R1` version, not the `R2` version.  Let's make some changes and type `git commit`.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/6.JPG" align="left" height="250" width="250" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

So now our pointer is on `newBranch` which is on `R3` and our `master` branch is on `R2`.  Although both `R3` and `R2` branch off of `R1`, the changes done in each are independent of one another.  To combine the two branches, we need to merge them.

### Merging

Merging branches will allow us to combine the changes made in `R2` and `R3`.  This is the scenario where we might have to fix merge conflicts.  When we type `git merge <branch_name>`, we combine all of the changes made in the target branch with the node our current pointer is on.  We then move our pointer to the new node, and the target branch stays at its current node.  Let's checkout to `master` and merge all the changes we made in `newBranch` with `git checkout master` followed by `git merge newBranch`. 


<img src="https://github.com/mliao95/MShistory/blob/master/Images/7.JPG" align="left" height="310" width="250" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Now after fixing any potential merge conflicts, all changes in the `newBranch` are now added onto the `master` branch at the node `R4`!  This can be done in other ways such as rebasing.

## Related Tools
-------------


### Rebase

Rebasing essentially has the same application as merging with one small difference: it creates copies of the changes in the target branch and adds them to your current pointer.  Let's rewind the repo back a step to see what happens when we rebase instead of merge.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/8.JPG" align="left" height="250" width="250" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

So currently, we are checked out on `newBranch` and we want to rebase the changes onto the master line.  Let's type in `git rebase master`.



<img src="https://github.com/mliao95/MShistory/blob/master/Images/9.JPG" align="left" height="280" width="190" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Now `newBranch` is moved right ahead of `master` at `R3'`.  Note that `R3'` has the exact same changes as `R3` but just plopped on top of `R2`.  If we want to update `master` to the newest version, we can rebase `master` on top of `newBranch` with `git checkout master` then `git rebase newBranch`.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/10.JPG" align="left" height="280" width="190" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Since `newBranch`, which is on `R4`, is directly stemming from `master`'s node, `R3`, rebasing `master` onto `newBranch` just moves the pointer up.  Although the differences between merging and rebasing are minor, rebasing allows for a clean linear commit history.  As you probably noticed, there is no branch on `R3`, so it must be inaccessible, right?  Wrong.  We can access it by detatching our pointer from the branch.

### HEAD pointer

For clarification, the `HEAD` is our main pointer which was represented by the `*` next to the branch names.  In most cases, we want this attatched to a given branch such as `master`, but in certain scenarios it is helpful to detatch the `HEAD` to point to certain commits.  Let's take the rebasing scenario and utilize our `HEAD` to access the isolated `R3`.  Here is the current scenario:

<img src="https://github.com/mliao95/MShistory/blob/master/Images/11.JPG" align="left" height="280" width="190" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
Ok, now lets detatch our head to access `R3` by typing `git checkout R3`.  


<img src="https://github.com/mliao95/MShistory/blob/master/Images/12.JPG" align="left" height="280" width="190" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Please note that the node names such as `R3` is a simplified version of the commit hash which is usually something like `253738856baaed7822f22e0bad105719aef51084`.  Luckily, you only need to supply enough characters such that Git understands which hash you are referencing.  In a real example, typing `git checkout 253738` would generally work.  One thing to keep in mind is that checking out to a branch is different from checking out to a node the branch is on.  Let's say `master` is on `R4`.  `git checkout master` will move the `HEAD` to point to the master branch whereas `git checkout R4` will detatch the `HEAD` to `R4`.  Checking out to a branch is essentially pointing to a pointer.

## Fixing Mistakes
-------------
### Reset

Let's say the newest commit completely ruined the whole project.  How do we go back to an old version of the repository?  A good method is to use `git reset`.  Here is a new scenario:

<img src="https://github.com/mliao95/MShistory/blob/master/Images/13.JPG" align="left" height="210" width="150" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Our `master` branch is on `R2` which contains all the unwanted changes.  We want to roll back out repo back to `R1`.  If we want to say "Move the master branch back one commit" we can type `git reset HEAD~1` which moves the checked out branch to the node previous to the `HEAD` node.  Similarly, `git reset master~1`, `git reset master^` or `git reset R1` will do the same function.  All commands will result in this state:


<img src="https://github.com/mliao95/MShistory/blob/master/Images/14.JPG" align="left" height="210" width="150" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Resetting only works if you are checked out on a branch, so if your `HEAD` is detached, it will not work.  Similar to merging, there are two ways to perform relatively the same function.  In this case, we can revert our changes rather than resetting them.

### Revert

Reverting operates similarly to rebasing.  Instead of moving our pointers back to a previous version, reverting will add a new commit that reverses the changes.  Let's go back to the initial scenario where `R2` contains unwanted changes.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/15.JPG" align="left" height="210" width="150" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Let's use the command `git revert R2` to undo the changes done in `R2`.  The new repo state looks like this:


<img src="https://github.com/mliao95/MShistory/blob/master/Images/16.JPG" align="left" height="280" width="150" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Note that there is a new commit, `R2'` that contains the complementary changes of `R2`.  Ideally, `R2'` is now at the same state as `R1`.  This can be done with any node.  If we wanted, we could undo the changes in `R1` with `git revert R1` which would result in this:

<img src="https://github.com/mliao95/MShistory/blob/master/Images/17.JPG" align="left" height="280" width="150" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

In this case, `R1'` would be in the same state as `R0`.

## Bonus: Neat Tricks
-------------
### Cherry Picking

Cherry picking is a great tool to use to selectively choose which commits to rebase.  For instance, let's say `newBranch` contains three functions for our software, but we later learn that one of the functions is no longer needed.  Each commit in `newBranch` is one of those three functions.

<img src="https://github.com/mliao95/MShistory/blob/master/Images/18.JPG" align="left" height="310" width= "250" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

We want to add the functions created in node `R2` and `R4` to the `master` branch, but we want to leave out the things in `R3`.  Cherry picking allows us to do just that.  By typing in `git cherry-pick R2 R4`, we rebase those commits right onto the `master` branch.  The end result will look like this:


<img src="https://github.com/mliao95/MShistory/blob/master/Images/19.JPG" align="left" height="310" width= "250" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

### Referencing Commits

This last section is less about different ways to tell Git which commit you are trying to reference.  As said before, many of the commit references in this tutorial are over simplified as I just used names such as `R0` or `R2`, and finding the commit hash and referencing the commit through that is time consuming.  Here are a couple of referencing tricks to make this easier.  Take this repo scenario below.


<img src="https://github.com/mliao95/MShistory/blob/master/Images/20.JPG" align="left" height="310" width= "250" ><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

If we want to reference the node one above a certain pointer, we can use the `^` symbol.  For instance, `newBranch^` would return `R5`.  Similarly, `newBranch^^` would return `R4`.

If we want to reference the commit five commits ago, we can use `~5` to do that function.
Instead of typing something like `master^^^^^`, we can simply just use `master~5`.








