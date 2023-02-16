# Jour 4 - GIT - 16/02/2023

## Console interactive du git rebase -i

`git rebase -i <nomDeBranche> ou <reCommit> ou <HEAD...>` (`<nomDeBranche> ou <reCommit> ou <HEAD...>` désigne l'endroit à partir du quel, on veut accéder aux commits): va ouvrir la console interactive
  
### Commandes

- Touche `insert` du clavier : pour modifier le fichier (affiche normalement --INSERT-- sur le terminal)
- Touche `Echap`: pour sortir de l'INSERT
- `:wq` pour enregister puis quitter
- Supprimer la ligne pour omit un comit
- `:q!` permet de sortir du terminal interactif sans modif

## Modifier un commit déjà push

### Solution 1: passer par un `git commit --amend`
  
1. `git rebase -i <refCommit>` : on accéde à l'insertion(avec touche insert) et on place le commit qu'on veut modifier en dernier
2. Modifier le fichier en local, puis un `git add` puis un `git commit --amend`: le `git commit --amend` va écraser le dernier commit sur la branche locale (pas la distante)
3. `git rebase -i <refCommit>` : on accéde à l'insertion (avec la touche `insert`) et on replace le commit modifié à sa place initiale
4. `git push --force`: pour mettre à jour la branche locale avec la branche distante
  
### - Solution2: passer par un squash avec `git rebase -i`
  
1. Modifier le fichier en local, puis un `git add` puis un `git commit` classique
2. `git rebase -i <refCommit>` : on accéde à l'insertion (avec touche `insert`) et on place le nouveau commit sous le commit qu'on souhaitait modifier
3. Remplacer dans le nouveau commit (déplacé) `pick` par `squash`: cela va fusionner le commit en squash avec le commit parent (celui qui est au dessus)
4. Enregistrer et sortir de la console interactif avec `:wq`
5. `git push --force`: pour mettre à jour la branche locale avec la branche distante
  
#### Pour récupérer les modifications appliquées par quelqu'un d'autres:
1. `git pull` (en se plaçant sur la branche concernée): ca va mettre à jour les documents en local et va créer un merge de branche
2. Si conflit de merge (modification sur une même ligne), il faut accepter les modifications entrantes
3. `git reset --hard <brancheDistante>` (`git reset --hard origin/yassir-julien`): pour supprimer le commit du merge et ainsi mettre à jour la branche locale par rapport à la branche distante
4. `git log --oneline`: pour vérifier si tout s'est bien passé et l'ordre des commits
  
