### Git Workflow for Hummingbot Project  
**origin** == Homeric-Freedom Org repo  
**eumaios1212** == eumaios1212 personal repo

1. `git fetch origin` (from any branch in local hummingbot repo)
    - `git fetch <remote>`  
    - downloads refs (references) from a remote repository into your local repo
    - refs are pointers to commits (HEAD), branches,remotes and tags.
2. `git checkout -b pr/something origin/dev --no-track`
    - Creates a new branch (`-b`) named `pr/something` based on `origin/dev` without tracking it (`--no-track`)
3. Do work
4. `git add filename filename filename`
    - Stages the specified files for commit
5. `git commit -m "doc: added docu"`
    - Commits the staged changes with a message
    - If multiple `-m` options are given, their values are concatenated as separate paragraphs (for 
      Conventional Commits formatting).
6. Repeat 4-6
7. `git push eumaios1212 pr/something`
    - Creates a new branch `pr/something` in the `eumaios1212` remote repository and pushes the changes to it
8. `pr/something` isn't merged for a while and may conflict with `origin/dev`
9. `git fetch origin`
    - Fetches the latest changes (if any) from the `origin` remote repository
    - HOW TO KNOW IF THERE ARE CHANGES 
      AFTER `git fetch origin`, so steps 10 and 11 can be skipped?
10. `git rebase origin/dev`
    - Rebases the current `pr/something` branch onto `origin/dev`, applying changes on top of the latest changes on
      `origin/dev`
11. `git push -f eumaios1212 pr/something`  
    - Force pushes the rebased branch to the `pr/something` branch in the `eumaios1212` remote repository
    - The force push (`-f`) overwrites the history of the branch with the rebased commits
    - This is necessary because rebasing rewrites commit history, and a regular push would be rejected
      if the remote branch has diverged from the local branch.
12. X number of Commits need to be squashed
13. `git rebase -i HEAD~X`
14. `git push -f eumaios1212 pr/something`
    - Force pushes the squashed commits to the `pr/something` branch in the `eumaios1212` remote repository
    - The force push (`-f`) overwrites the history of the branch with the squashed commits