lets assume origin == upstream
1. git fetch origin
2. git checkout -b pr/something origin/dev
3. Do work
4. git add filename filename filename
5. git commit -m "doc: added docu"
6. Repeat 4-6
7. git push your_remote pr/something
8. git push eumaios1212 pr/something 
9. Pr isnt merged for a while and has conflicts
10. git fetch origin
11. git rebase origin/master
12. git push -f nahuhh pr/something
13. Have to squash etc
14. git rebase -i HEAD~3
15. git push -f nahuhh pr/something
