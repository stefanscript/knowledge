# Git

### Search for a file in history
  
        git log --all --full-history -- "**/thefile.*"

### Purge big files or credentila from history

https://docs.gitlab.com/ee/user/project/repository/reducing_the_repo_size_using_git.html#repository-cleanup

Check for files in history

      git log --follow -p -- file/path 
