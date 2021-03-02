# git_lesson


1. Создать отдельный репозиторий на github.
2. Создать локально три текстовых файла.
3. Поместить в стейдж, закомитить, запушить.
4. Создать две новые ветки.
5. Внести изменения в ветку 1 и 2 
6. Смерджить между собой вновь созданные ветки.
7. Смерджить ветку с веткой мастер
8. Отменить предыдущий комит
9. Все изменения запушить в гит репозиторий.

=======================================================

## 1. Создать отдельный репозиторий на github.
```
root@db-master:~/git_lesson# git config --global user.name "Pavel"
root@db-master:~/git_lesson# git config --global user.email "likemaydev@gmail.com"
root@db-master:~/git_lesson# git clone https://github.com/likemaydev/git_lesson.git
```


## 2. Создать локально три текстовых файла.
```
root@db-master:~/git_lesson# touch test_file1
root@db-master:~/git_lesson# touch test_file2
root@db-master:~/git_lesson# touch test_file3
```


## 3. Поместить в стейдж, закомитить, запушить.
```
root@db-master:~/git_lesson# git add *
root@db-master:~/git_lesson# git status
root@db-master:~/git_lesson# git commit -m "Add files to repo"
root@db-master:~/git_lesson# git push
...
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/likemaydev/git_lesson.git
   4d2a417..6e9b7a9  main -> main
```


## 4. Создать две новые ветки.
```
root@db-master:~/git_lesson# git branch newbr1
root@db-master:~/git_lesson# git branch newbr2
root@db-master:~/git_lesson# git branch
* main
  newbr1
  newbr2
```

## 5. Внести изменения в ветку 1 и 2 
```
root@db-master:~/git_lesson# git checkout newbr1
root@db-master:~/git_lesson# echo "Edit test_file2 in newbr1" > test_file2
root@db-master:~/git_lesson# git add *
root@db-master:~/git_lesson# git commit -m "Edit test_file2 in newbr1"

root@db-master:~/git_lesson# git checkout newbr2
root@db-master:~/git_lesson# echo "Edit test_file3 in newbr2" > test_file3
root@db-master:~/git_lesson# git add *
root@db-master:~/git_lesson# git commit -m "Edit test_file3 in newbr2"

root@db-master:~/git_lesson# git log -n 2 --graph --all
* commit 8a5e0d504907d8da2aef089010a642dab2303780 (HEAD -> newbr2)
| Author: Pavel <likemaydev@gmail.com>
| Date:   Tue Mar 2 10:32:12 2021 +0000
|
|     Edit test_file3 in newbr2
|
| * commit 20ff02391c0bcd59e270c75827d99890c1550d4c (newbr1)
|/  Author: Pavel <likemaydev@gmail.com>
|   Date:   Tue Mar 2 10:30:45 2021 +0000
|
|       Edit test_file2 in newbr1
```

## 6. Смерджить между собой вновь созданные ветки.
```
root@db-master:~/git_lesson# git merge newbr1 -m "Merge newbr1 > newbr2"
Merge made by the 'recursive' strategy.
 test_file2 | 1 +
 1 file changed, 1 insertion(+)

root@db-master:~/git_lesson# git log -n 2 --graph --all
*   commit d93049d51dc0f7339ee5ad5b9e0be88306d11980 (HEAD -> newbr2)
|\  Merge: 8a5e0d5 20ff023
| | Author: Pavel <likemaydev@gmail.com>
| | Date:   Tue Mar 2 10:34:18 2021 +0000
| |
| |     Merge newbr1 > newbr2
| |
| * commit 20ff02391c0bcd59e270c75827d99890c1550d4c (newbr1)
| | Author: Pavel <likemaydev@gmail.com>
| | Date:   Tue Mar 2 10:30:45 2021 +0000
| |
| |     Edit test_file2 in newbr1
```

## 7. Смерджить ветку с веткой мастер
```
root@db-master:~/git_lesson# git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

root@db-master:~/git_lesson# git branch
* main
  newbr1
  newbr2

root@db-master:~/git_lesson# git merge newbr2 -m "Merge newbr2 > main"
Updating 6e9b7a9..d93049d
Fast-forward (no commit created; -m option ignored)
 test_file2 | 1 +
 test_file3 | 1 +
 2 files changed, 2 insertions(+)

root@db-master:~/git_lesson# git log -n 2 --graph --all
*   commit d93049d51dc0f7339ee5ad5b9e0be88306d11980 (HEAD -> main, newbr2)
|\  Merge: 8a5e0d5 20ff023
| | Author: Pavel <likemaydev@gmail.com>
| | Date:   Tue Mar 2 10:34:18 2021 +0000
| |
| |     Merge newbr1 > newbr2
| |
| * commit 20ff02391c0bcd59e270c75827d99890c1550d4c (newbr1)
| | Author: Pavel <likemaydev@gmail.com>
| | Date:   Tue Mar 2 10:30:45 2021 +0000
| |
| |     Edit test_file2 in newbr1
```

## 8. Отменить предыдущий комит
```
root@db-master:~/git_lesson# git reset --hard HEAD~1
HEAD is now at 8a5e0d5 Edit test_file3 in newbr2

root@db-master:~/git_lesson# git log -n 2 --graph --all
*   commit d93049d51dc0f7339ee5ad5b9e0be88306d11980 (newbr2)
|\  Merge: 8a5e0d5 20ff023
| | Author: Pavel <likemaydev@gmail.com>
| | Date:   Tue Mar 2 10:34:18 2021 +0000
| |
| |     Merge newbr1 > newbr2
| |
| * commit 20ff02391c0bcd59e270c75827d99890c1550d4c (newbr1)
| | Author: Pavel <likemaydev@gmail.com>
| | Date:   Tue Mar 2 10:30:45 2021 +0000
| |
| |     Edit test_file2 in newbr1
```

## 9. Все изменения запушить в гит репозиторий.
```
root@db-master:~/git_lesson# git push
...
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/likemaydev/git_lesson.git
   6e9b7a9..8a5e0d5  main -> main
```
