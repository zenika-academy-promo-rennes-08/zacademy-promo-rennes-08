# Jour 3 - GIT - 15/02/2023

## Infos utiles

- Gestion de versions (versioning)
- Autres outils de versioning: SVN
- Learn Git Branching: https://learngitbranching.js.org/?locale=fr_FR

## Commandes GIT

- `git checkout <branch> ou <hashCommit> ou <nomTag>` : place le pointeur HEAD sur une branche (qui elle même pointe sur son dernier commit) ou sur un commit directement
- `git branch <nomBranche> <hashCommit>` : crée une branche sur la référence du commit spécifié
- `git branch -f main <HEAD^2~2...> ou <hashCommit>` : placer la branche à un endroit précis par rapport au HEAD ou sur un commit. Le ~ va servir à se référer aux niveaux au-dessus alors que le ^ permet de se référer aux parents. Pour un commit qui a 2 parents, pour se référer au second parent, on utilise ^2
- `git reset` (local): suppression totale
- `git revert` (distant): création d'un nouveau commit qui annule le dernier
- `git rebase` : copie tous les commits d'une branche en dessous d'une autre
- `git cherry-pick <commits>` : copie tous les commits souhaités (de différentes branches) dans une autre branche
- `git rebase -i` : pour modifier l'ordre des commits, voire en supprimer, doit être utilisée en se placant sur la branche souhaitée
- `git tag <nomTag> <hashCommit>` : affecte un tag à un commit
- `git describe <refCommit> ou <nomBranche>` : décrit la différence entre le commit et le tag le plus récent. Le résultat renvoyé est `<tag>_<numCommits>_g<hash>`, où où tag est le tag le plus proche dans l'historique, numCommits le nombre de commits depuis le tag, et <hash> le hash/identifiant du commit décrit.
- `git pull; git push` : permet de mettre à jour le dépôt local avec le distant, et de merger la branche local avec le branche du dépôt local en créant un nouveau commit de merge puis push après
- `git pull --rebase; git push` : permet de mettre à jour le dépôt local avec le distant, et de rebase ma branche local avec le branche du dépôt local puis push après

- `git checkout -b <nomBrancheLocale> <nomBrancheDistante>` : crée une nouvelle branche qui va suivre la branche distante indiquée
- `git branch -u <nomBrancheDistante> <nomBrancheLocale>` : paramétrer une branche locale déjà existante pour suivre une branche distante
- `git push <remote> <place>` (git push origin main) : peu importe la branche courante, on demande de publier tous les commits de la branche main locale vers la branche main distante
- `git push origin <source>:<destination>` (git push origin foo^:main) : publier les modifications de la source vers la branche distante désignée par la destination. Si la destination n'existe pas, git va la créer dans le repo distant
- `git push origin :<destination>` (git push origin :foo) : en ne précisant pas une source, on détruit la destination, dans l'exemple on détruit la branche distante foo
- `git fetch <remote> <place>` (git fetch origin main) : peu importe la branche courante, on demande de récupérer les commits de la branche distante main vers la branche locale origin/main (attention pas main!)
- `git fetch origin <source>:<destination>` (git fetch origin main:foo) : récupère les commits de la source (branche distante) vers la destination (branche locale). Cela est opposé à l'ordre dans git push. Par contre, en utilisant cette syntaxe, ce n'est pas que la branche distante en local origin/foo qui est modifiée mais également la branche foo. Si la destination n'existe pas, il crée la branche
- `git fetch origin :<destination>` (git fetch origin :foo) : en ne précisant aucune source, on crée une nouvelle branche local, dans notre exemple une branche foo. A rappeler que l'utilisation du refSpec <source>:<destination> est inversée entre push et fetch
- `git pull origin foo` : équivalent à  git fetch origin foo; git merge o/foo
- `git pull origin bar~1:bugFix` : équivalent à git fetch origin bar~1:bugFix; git merge bugFix
  
- `git log --oneline` : affiche les commits de la représentation de la branche en local (un par ligne)
  
