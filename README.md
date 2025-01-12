
# Git Workflow Fundamentals by Abdallah AL-Banna

This cheat sheet provides an overview of Git workflows for initializing a repository, working with commits, branches, pull requests, and managing a remote repository on GitHub. It also covers tagging, reverting, and resetting commits effectively.

---

## 1. Initial Setup

1. **Initialize Git in a Project Folder**:
   ```bash
   git init
   ```

2. **Create a `.gitignore` File**: Exclude unnecessary files (specific to your project type). For example:
   ```gitignore
   # Ignore Visual Studio temporary files
   .vs/
   bin/
   obj/
   ```

3. **Set Up Git User Identity**:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

4. **Create an Initial Commit**:
   ```bash
   git add .
   git commit -m "Initial commit: Add project files"
   ```

5. **Create a Remote Repository on GitHub**:
   - Go to [GitHub](https://github.com) and create a new repository.
   - Copy the repository URL.

6. **Link the Local Repository to GitHub**:
   ```bash
   git remote add origin <repository-url>
   ```

7. **Rename the Branch to `main` (if needed)**:
   ```bash
   git branch -M main
   ```

8. **Push the Initial Commit**:
   ```bash
   git push -u origin main
   ```

---

## 2. Working on the Main Branch

1. **Modify Files**: Make changes to your project files.

2. **Stage Changes**:
   ```bash
   git add .
   ```

3. **Commit Changes**:
   ```bash
   git commit -m "Describe what you changed"
   ```

4. **Push Changes to GitHub**:
   ```bash
   git push origin main
   ```

---

## 3. Working with Feature Branches

1. **Create and Switch to a New Branch**:
   ```bash
   git checkout -b <branch-name>
   ```

2. **Make Changes in the Feature Branch**: Modify files, stage, and commit:
   ```bash
   git add .
   git commit -m "Describe feature or changes"
   ```

3. **Push the Feature Branch to GitHub**:
   ```bash
   git push -u origin <branch-name>
   ```

4. **Merge the Feature Branch into Main**:
   - Switch back to the main branch:
     ```bash
     git checkout main
     ```
   - Merge the feature branch:
     ```bash
     git merge <branch-name>
     ```
   - Push the updated main branch:
     ```bash
     git push origin main
     ```

5. **Delete the Feature Branch (Optional)**:
   Locally:
   ```bash
   git branch -d <branch-name>
   ```
   Remotely:
   ```bash
   git push origin --delete <branch-name>
   ```

---

## 4. Pull Requests

1. Push your feature branch to the remote repository:
   ```bash
   git push -u origin <branch-name>
   ```

2. Navigate to your repository on GitHub.

3. Click on **Pull Requests** in the repository menu.

4. Click **New Pull Request** and select your feature branch to merge into the main branch.

5. Review the changes and submit the pull request.

---

## 5. Tagging Commits

Tags are useful for marking specific points in your project, such as version releases.

1. **Create a Lightweight Tag**:
   ```bash
   git tag <tag-name>
   ```

2. **Create an Annotated Tag**:
   ```bash
   git tag -a <tag-name> -m "Tag message"
   ```

3. **Push Tags to the Remote Repository**:
   ```bash
   git push origin <tag-name>
   ```

4. **List Tags**:
   ```bash
   git tag
   ```

5. **Delete a Tag**:
   Locally:
   ```bash
   git tag -d <tag-name>
   ```
   Remotely:
   ```bash
   git push origin --delete <tag-name>
   ```

---

## 6. Resolving Merge Conflicts

If there are conflicts during a merge:
1. Git will pause and show a conflict message.
2. Open the conflicting files and manually resolve the conflicts:
   ```text
   <<<<<<< HEAD
   Your changes
   =======
   Incoming changes
   >>>>>>> branch-name
   ```
3. After resolving:
   ```bash
   git add <file>
   git commit -m "Resolve merge conflict"
   ```

---

## 7. Cloning an Existing Repository

1. Clone a repository:
   ```bash
   git clone <repository-url>
   ```

2. Navigate into the project folder:
   ```bash
   cd <repository-name>
   ```

---

## 8. Undoing Changes: `git revert` vs. `git reset`

### **`git revert`** (Safe for Shared Repositories)
- Creates a new commit that undoes a specific commit.
   ```bash
   git revert <commit-hash>
   ```

### **`git reset`** (Rewrites History)
- Modifies commit history. Use cautiously in shared repositories.
   - Soft reset (keep changes staged):
     ```bash
     git reset --soft <commit-hash>
     ```
   - Mixed reset (unstage changes):
     ```bash
     git reset --mixed <commit-hash>
     ```
   - Hard reset (discard changes):
     ```bash
     git reset --hard <commit-hash>
     ```

---

## 9. Common Git Commands

| Command                            | Description                                   |
| ---------------------------------- | --------------------------------------------- |
| `git init`                         | Initialize a new Git repository.              |
| `git add .`                        | Stage all changes for the next commit.        |
| `git commit -m "message"`          | Commit changes with a message.               |
| `git status`                       | View the status of your working directory.    |
| `git log --oneline`                | View a simplified commit history.             |
| `git checkout -b <branch-name>`    | Create and switch to a new branch.            |
| `git merge <branch-name>`          | Merge a branch into the current branch.       |
| `git push origin <branch-name>`    | Push changes to the remote branch.            |
| `git pull origin <branch-name>`    | Pull updates from the remote branch.          |
| `git tag -a <tag-name>`            | Create an annotated tag.                      |
| `git revert <commit-hash>`         | Revert a specific commit safely.              |
| `git reset --hard <commit-hash>`   | Reset the repository to a specific commit.    |
| `git push origin --force`          | Force push changes to the remote repository.  |
| `git push origin --delete <tag>`   | Delete a tag from the remote repository.      |
