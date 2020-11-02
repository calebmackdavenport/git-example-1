
# Git Submodule Example

This is an example of two projects sharing code.  
The other project is available [here](https://github.com/smebdi/git-example-2).

These projects currently share the following submodule repositories:  
[submodule1](https://github.com/smebdi/git-submodule-example)  
[submodule4](https://github.com/smebdi/git-submodule-example-4)

## Adding a new submodule
To add a submodule to an existing project, it's as easy as  
`git submodule add https://github.com/smebdi/git-submodule-example-4 ./store/submodule4`

This will point the project at the top level commit hash and leave the submodule in a detached head state.  
You can leave it like this if you intend to be a listener and not make changes.

Or checkout a branch of the submodule such as `origin/main`, and it will function as a nested repository pointed at that branch. 

**What you see below follows a branch based workflow, not a commit based workflow.**  
**There are many ways to work with submodules - this is my preferred method.**

## Making changes within a submodule
Root level changes are easily visible, as always, by using `git status` or any version control viewer. Below is an example of VSCode's source control tab where I have:
- Unstaged changes to a submodule
- Unstaged changes to the root project
- An unstaged change in root which will reflect the updated commit within the submodule  
![](https://i.gyazo.com/955931b86a45950224a14ebfc9f442e0.png)

The `submodule` that has been updated will look like the following:
![](https://i.gyazo.com/0a370813d373e6a59adc9e303e81e1cb.png)

Before committing, in your root repository, you'll find a `-dirty` flag in the `submoduleNameHere.diff` to notate that changes have been made and the commit does not directly match the submodule from the repository. If you discard those changes without committing, git should automatically remove the flag.

Once you commit and push your changes to the submodule, `submoduleNameHere.diff` will update with the new commit hash like so:  
![](https://i.gyazo.com/5118dcb5d4c9ada75ce84792e627fc36.png)

That commit would show any changes made within the root repo as well as a snapshot of the changes within the submodule.  
![](https://i.gyazo.com/d5b0c92e3991ac85a0dc53d71c0766b6.png)

Assuming both submodules are pointed at the same branch, those changes are visible to any other repositories sharing the same submodule either via a source control manager or `git status`.  
![](https://i.gyazo.com/5c418acdd4a453f098b46767f7c14514.png)

Simply `git pull` within the submodule to retrieve the latest commit. Pointing at the new commit will update the `submoduleNameHere.diff` in the root repository, just like before. Simply commit this change to reflect the updated submodule commit target.  
![](https://i.gyazo.com/af2360a45a5aa60481799d15d841b118.png)

If multiple users are working on the same root branch and one user updates a submodule, those changes are easily visible:  
![](https://i.gyazo.com/30d7d82072e3a955d29c750a60600c4d.png)  
Again, simply `git pull` within the submodule first then and within the root repository.
