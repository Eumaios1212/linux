origin      == Homeric-Freedom Org repo
eumaios1212 == eumaios1212 personal repo

1. git fetch origin
2. git checkout -b pr/something origin/dev --no-track
3. Do work
5. git add filename filename filename
6. git commit -m "doc: added docu"
7. Repeat 4-6
8. git push eumaios1212 pr/something 
  - Pr isnt merged for a while and has conflicts with origin/dev
10. git fetch origin
11. git rebase origin/master
12. git push -f eumaios1212 pr/something
13. Have to squash etc
14. git rebase -i HEAD~3
15. git push -f eumaios1212 pr/something
