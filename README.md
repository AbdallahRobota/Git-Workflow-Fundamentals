# Git Workflow Fundamentals by Abdallah AL-Banna

This cheat sheet provides an overview of Git workflows for initializing a repository, working with commits, branches, and managing a remote repository on GitHub.

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
   *(Use `--global` to apply globally or omit `--global` for repository-specific configuration.)*

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

## 4. Viewing and Resetting Commits

1. **View Commit History**:
   ```bash
   git log --oneline
   ```

2. **Undo Changes in the Working Directory**: Revert uncommitted changes:
   ```bash
   git checkout -- <file>
   ```


3. **Force Push After Reset**:
   ```bash
   git push origin main --force
   ```

---

## 5. Pulling Changes from the Remote

To ensure your local repository is up-to-date:
```bash
git pull origin main
```

---

## 6. Resolving Merge Conflicts

If there are conflicts during a merge:
1. Git will pause and show a conflict message.
2. Open the conflicting files and manually resolve the conflicts.
   - Look for sections like:
     ```
     <<<<<<< HEAD
     Your changes here
     =======
     Incoming changes here
     >>>>>>> branch-name
     ```
3. After resolving:
   ```bash
   git add <file>
   git commit -m "Resolve merge conflict"
   ```

---

## 7. Cloning an Existing Repository

1. **Clone a Repository**:
   ```bash
   git clone <repository-url>
   ```

2. **Navigate into the Project Folder**:
   ```bash
   cd <repository-name>
   ```

---

## 8. Undoing: `git revert` and `git reset`

   1. **`git revert`**

         ```bash
         git revert <commit-hash>
         ```

      ### **Examples**:
      1. **Revert a Single Commit**:
         ```bash
         git revert a1b2c3d4
         ```
         - Reverts the changes in commit `a1b2c3d4` and creates a new commit that undoes those changes.

      2. **Revert Multiple Commits**:
         ```bash
         git revert a1b2c3d4..e5f6g7h8
         ```
         - Reverts a range of commits from `a1b2c3d4` to `e5f6g7h8`.

      3. **Revert a Merge Commit**:
         ```bash
         git revert -m 1 <merge-commit-hash>
         ```
         - Reverts a merge commit, keeping the changes from the first parent.

         ### **Use Cases**:
         - Undoing mistakes in a shared repository.
         - Reverting a specific commit without modifying the project history.

---

2. **`git reset`**

      ### **Purpose**:  
      Moves the `HEAD` and changes the commit history. It **can modify the staging area and working directory**.

      ### **Types of Reset**:
      1. **Soft Reset (`git reset --soft`)**  
         Moves `HEAD` to the specified commit, keeping changes in the **staging area**.

         **Syntax**:
         ```bash
         git reset --soft <commit-hash>
         ```
         **Example**:
         ```bash
         git reset --soft HEAD~1
         ```
         - Moves `HEAD` one commit back, but the changes remain staged for committing.

      2. **Mixed Reset (`git reset --mixed`)**  
         Moves `HEAD` to the specified commit, **unstages changes** (removes changes from the staging area but keeps them in the working directory).

         **Syntax**:
         ```bash
         git reset --mixed <commit-hash>
         ```
         **Example**:
         ```bash
         git reset HEAD~1
         ```
         - Moves `HEAD` one commit back, unstages changes, but leaves them in the working directory.

         **Note**: `git reset` without any flags defaults to a mixed reset.

      3. **Hard Reset (`git reset --hard`)**  
         Moves `HEAD` to the specified commit, and **discards all changes** in both the staging area and working directory.

         **Syntax**:
         ```bash
         git reset --hard <commit-hash>
         ```
         **Example**:
         ```bash
         git reset --hard HEAD~1
         ```
         - Moves `HEAD` one commit back and completely discards any local changes.

      ### **Examples**:

      1. **Soft Reset**:
         ```bash
         git reset --soft HEAD~1
         ```
         - Reverts to the previous commit, but keeps the changes staged.

      2. **Mixed Reset**:
         ```bash
         git reset HEAD file1.txt
         ```
         - Unstages `file1.txt`, but keeps the changes in the working directory.

      3. **Hard Reset**:
         ```bash
         git reset --hard a1b2c3d4
         ```
         - Completely discards all changes and resets to the state of commit `a1b2c3d4`.

---

   ## **Key Differences Between `git revert` and `git reset`**

   | Feature                         | `git revert`                             | `git reset`                                                |
   | ------------------------------- | ---------------------------------------- | ---------------------------------------------------------- |
   | **Effect on History**           | Creates a new commit to undo changes.    | Rewrites commit history.                                   |
   | **Commit History Altered**      | No. History is preserved.                | Yes. History is changed.                                   |
   | **Safe for Shared Repos**       | Yes. It doesn’t rewrite history.         | No. Can rewrite history, causing issues for collaborators. |
   | **Changes in Staging Area**     | No changes to the staging area.          | Can unstage or stage files, depending on the reset type.   |
   | **Effect on Working Directory** | No. Working directory remains unchanged. | May modify the working directory (depends on reset type).  |

   ---

   ## **When to Use `git revert`**:
   - Undoing a commit in a **shared repository**.
   - Creating a new commit that undoes the changes made in a previous commit.

   ## **When to Use `git reset`**:
   - Modifying local commit history (e.g., squashing commits, fixing errors).
   - Removing files from the staging area (unstaging).
   - Discarding local changes completely with a hard reset.

   ---

   ### **Additional Notes**:
   - **`git reset --hard`** is destructive: it **loses all uncommitted changes** in the working directory and staging area.
   - **`git reset`** is useful for modifying local commit history and is best used for local, personal repositories.
   - **`git revert`** is safer for undoing changes in a shared environment, as it **does not rewrite history**.


## 9. Common Git Commands

| **Command**                      | **Description**                            |
| -------------------------------- | ------------------------------------------ |
| `git init`                       | Initialize a new Git repository.           |
| `git add .`                      | Stage all changes for the next commit.     |
| `git commit -m "message"`        | Commit changes with a descriptive message. |
| `git status`                     | View the status of your working directory. |
| `git log --oneline`              | View a simplified commit history.          |
| `git branch`                     | List all branches in the repository.       |
| `git checkout -b <branch-name>`  | Create and switch to a new branch.         |
| `git merge <branch-name>`        | Merge a branch into the current branch.    |
| `git push origin <branch-name>`  | Push changes to the remote branch.         |
| `git pull origin <branch-name>`  | Pull updates from the remote branch.       |
| `git reset --hard <commit-hash>` | Reset the repository to a specific commit. |
| `git push origin --force`        | Force push changes to the remote branch.   |
