---
title: Git
tags:
  - Git
---

Git is a popular **version control system(VCS)** that is used to track changes to files and directories over time. It has become the de facto standard for version control and is widely used in software development, especially for open-source projects. It is supported by many hosting services, such as GitHub, GitLab, and Bitbucket, which provide additional features such as code reviews, issue tracking, and [continuous integration (CI)](/blog/cicd/cicd).

???+ info "Benefit of Git"

    - Fast Speed: 
      Git uses SHA compression, which makes it very fast.

    - Merge Conflicts: 
      Git can handle merge conflicts, which mean that **it's OK for multiple people to work on the same file at the same time.**

    - Cheap Branches: 
      Git offers a lot of flexibility and opportunity for collaboration with branches. **By using branches, developers can make changes in a safe sandbox.**

    - Ease of roll back: 
      his means that if you do make a mistake, even on an important branch like main, it's OK. **You can easily revert that change, or roll back the branch pointer to the commit where everything was fine.**

??? question "Why Git is good for text files, but not so good for images?"

    Git stores changes in SHA hashes, which work by compressing text files. That makes Git a very good version control system (VCS) for software programming, but not so good for binary files like images or videos.

## Git Init

```sh
git init
```

It turns any directory into a Git repository. Git creates a hidden directory called `.git`. That directory stores all of the objects and refs that Git uses and creates as a part of your project's history. This hidden `.git` directory is what separates a regular directory from a Git repository.


## Git Clone

```sh
git clone https://github.com/Kreal321/blog.git
```

The git clone command is used to create a copy of a remote Git repository on your local machine.


??? note "How to fix The remote end hung up unexpectedly while git cloning"

    Raising the postBuffer size by:

    ```sh
    git config --global http.postBuffer 524288000
    ```
    
    If it does not work, you can raise again:

    ```sh
    git config --global http.postBuffer 1048576000
    ```

    > Maximum size in bytes of the buffer used by smart HTTP transports when POSTing data to the remote system.
    > For requests larger than this buffer size, HTTP/1.1 and Transfer-Encoding: chunked is used to avoid creating a massive pack file locally. Default is 1 MiB, which is sufficient for most requests.

## Git Log

Only show the first line of the commit message

```sh
git log --oneline
```

Show author date and commit date information

```sh
git log --pretty=fuller
```

??? question "Author date and commit date are different?"

    Author date is the date when the author made the commit, and commit date is the date when the commit was committed to the repository.

    To change commit commit date and author date during git commit, you can use the following command:

    ```sh
    GIT_COMMITTER_DATE="DATE" git commit -m "init commit" --date="DATE"
    ```


## Useful Links
- [Installing Git Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Git Guide from GitHub](https://github.com/git-guides)
