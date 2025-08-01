# HOW TO USE THIS SUBMODULE 

## 📄📄 Cloning our Sub module Repo
### ✅ Option 1: Clone with submodules in one command (Recommended)
```bash 
git clone --recurse-submodules https://github.com/VMahluza/quickcoach.git
```
This will:
> Clone your main repository.
> Automatically initialize and clone the `frontend` and `backend` submodules.

### ✅ Option 2: Clone and manually initialize submodules
If you've already cloned the main repo without --recurse-submodules:
```bash 
git clone https://github.com/VMahluza/quickcoach.git
```
Then run: 
```bash 
cd quickcoach
git submodule update --init --recursive
```
## 🛠️ Making Changes to this submodule
Let's say you made changes to the backend
> 1. Navigate into the submodule
```bash
cd backend
```
> 2. Check your current branch
```bash
git status
git branch
```
> 3. Add, commit, and push your changes
```bash
git add .
git commit -m "Your change message"
git push origin
```

#### 📍 Now update the main repo to reference the new submodule commit
After pushing your submodule changes:

> Go back to your main repo root:
```bash cd ..```
> Git will detect the submodule has a new commit:

```bash git status```
> Commit the submodule reference update:
```bash
git add backend  # or frontend
git commit -m "Updated backend submodule to latest commit"
git push origin main
```
> This tells Git: "Hey, the main repo now points to a newer commit of the backend/frontend."

#### ✅ Summary Workflow
Step	What you do
1	cd backend or cd frontend
2	Make changes, commit & push to the submodule
3	cd .. back to main repo
4	git add backend
5	Commit and push the submodule update in main repo

## 📌 Important Notes
> Each submodule has its own Git history.
You must push from inside the submodule for changes to be saved remotely.
Updating the submodule pointer in the main repo ensures collaborators get the correct version.

## 🔄 Pulling Updates Made by Someone Else (Submodules)
### ✅ Option 1: Full update (main repo + submodules)
> If your colleague pushed both:
Changes inside backend/ or frontend
AND updated the main repo to point to the latest submodule commits
Then run this:
```bash
git pull --recurse-submodules
git submodule update --init --recursive
```
> This fetches the main repo and syncs submodules to the commit your colleague set.

### ✅ Option 2: Update submodules directly
If you only want to get the latest commits from the submodules (in case your colleague pushed, but didn’t update the main repo):
For frontend:
```bash
cd frontend
git checkout main  # or the branch they pushed to
git pull
cd ..
```
For backend:
```bash
cd backend
git checkout main
git pull
cd ..
```
### 🧠 How it works
> * ```git submodule update``` syncs to the commit specified in the main repo.

> * ```git pull``` (inside a submodule) gets the latest code from the submodule’s own branch.

> * If the main repo was updated by your teammate to point to newer commits, you can just do a top-level pull with ```--recurse-submodules```.

### 💡 Tip
> If you're working with branches in submodules (not pinned commits), you can set this up to always track latest like this:

```bash
git config -f .gitmodules submodule.backend.update remote
git config -f .gitmodules submodule.frontend.update remote
git submodule update --remote
```

## COMMON ISSUES - 🧯 Submodules not up-to-date after cloning
> After cloning, submodules are locked to a specific commit. So unless the main repo was updated to reference newer submodule commits, your submodules will appear outdated.

### ✅ Solutions
#### Update main repo to track submodule HEADs (optional for future)
> Tell Git to track remote HEAD for submodules
```bash
git config -f .gitmodules submodule.backend.update remote
git config -f .gitmodules submodule.frontend.update remote
```
> Now update to the latest commits in both submodules
```bash
git submodule update --remote
```
> Then commit the updated submodule references in the main repo:

```bash
git add backend frontend
git commit -m "Updated submodules to latest commits"
git push origin main
```
> From now on, git submodule update --remote will pull latest from default branches of submodules.

