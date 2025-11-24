
Actualización del Github

Paso 1  Ubicarme en  Documents/OSCP2026

Paso 2  Actaulizar los cambios realizados  con el comando 
git add .

con el comando   git status  podemos ver el estado actual de la incorporación de lo agregado ejemplo:

```
┌──(btk㉿kali)-[~/Documents/OSCP2026]
└─$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   .obsidian/workspace.json
        new file:   COMANDOS.md
        new file:   GITHUB.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   GITHUB.md

```

Paso 3 Realizar el commit al repositorio oficial con el comando
git commit -m "Mensaje de actualización de commit"


```
─$ git commit -m "Mensaje de actualización de commit"
[main bf2445b] Mensaje de actualización de commit
 3 files changed, 53 insertions(+), 12 deletions(-)
 create mode 100644 COMANDOS.md
 create mode 100644 GITHUB.md
                                                                                                                 
┌──(btk㉿kali)-[~/Documents/OSCP2026]
└─$ 

```


Paso 4  actualizacion de cambios para verlos reflejados en Github  se aplica el comando git push origin main  en donde debemos de logearnos con nuestro user y token

```
┌──(btk㉿kali)-[~/Documents/OSCP2026]
└─$ git push origin main 
Username for 'https://github.com': arturobadilloidm-sudo
Password for 'https://arturobadilloidm-sudo@github.com': 
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 22 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 922 bytes | 922.00 KiB/s, done.
Total 6 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/arturobadilloidm-sudo/OSCP2026.git
   27b3992..bf2445b  main -> main
                                                                                                                 
┌──(btk㉿kali)-[~/Documents/OSCP2026]


```



