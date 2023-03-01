---
title: Git
tags:
  - Git
---

Git is a popular **version control system(VCS) ** that is used to track changes to files and directories over time. It has become the de facto standard for version control and is widely used in software development, especially for open-source projects. It is supported by many hosting services, such as GitHub, GitLab, and Bitbucket, which provide additional features such as code reviews, issue tracking, and [continuous integration (CI)](/blog/cicd/cicd).

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

---

:material-clock-edit-outline: Edit on **Feb 24th, 2023**
:material-clock-plus-outline: Created on **Apr 8th, 2020**