# Git

### Search for a file in history
  
        git log --all --full-history -- "**/thefile.*"

### Purge big files or secrets from history

https://docs.gitlab.com/ee/user/project/repository/reducing_the_repo_size_using_git.html#purge-files-from-repository-history

Check for files in history

      git log --follow -p -- file/path 
