# Test

Recuperer une copie local : ds un terminal : $ git clone "URL"
URL = http://github.com/login/Test.git
ou git@github.com : login/Test.git

NB : positionner la variable d'environnement : 

Commandes Git : 

	Voir dans quel etat on se trouve : 
		$ git status

	-> Modifier ou ajouter des fichiers :
		refaire un git status
	
	Voir les differences : 
		$ git diff

	Enregistrer les modifications (faire un commit): 
		-ajouter les changements à enregistrer dans l'index : 
			$ git add fichier1 fichier2  ... 
		NB : $ git satus (pour verifier)
		     $ git diff (ne devrait rien afficher)
		     $ git diff --cached (regarde entre lindex et le dépot)
		-Faire de commit (enregistrer les changements) :
			$ git commit

		NB : $ git statut (pas de changement normalement)


Raccourcis : 

	$ git commit -s :  fait autmatiquement le "add" pour les fichiers deja connus de git
	$ git commit -- fichier : le fichier est ajouté pour le commit
	$ git commit -m "message" : Ecris le message directement



Revoir les commits : 

	$ gitk (interface graphique)
	$ git log (affiche dans le terminal)
	$ git log -p (affiche les modifications en plus)
	$ git log --stat --summary (n'affiche pas toutes les modifs mais juste ce qui a ete modif et le nombre de lignes modifiées, cest une version simplifiée)
	$ git log --oneline (résumé des commit sur une ligne)	

Envoyer /recevoir les modifs  vers/depuis un serveur : 

	Envoyer : $ git push

	Recevoir : $ git pull (recupere ET integre les changements)

	$ git fetch (récupere simplement les changements)


A quoi peuvent ressembler de "vrais" commits :
	En general : -changement unitaire (une fonctionnalité, un bug...)
				 -message explicatif

	Exemples : https://git.kernel.org

				ex : git.git --> log

	Ajout de Fichiers : Ajout --> $ git add fichiers... 
	      	 	    Suppression --> $ git rm fichiers...
			    Renommer/deplacer : $ git mv source destination
NB : en pratique, ça revient à une suppression et un ajout. 
     		 On peut constater avec : $ git log --summary
		    	 	   	  $ git log --summary -M
					
				
Mettre du travail de coté :

     $ git stash     (Met les modifs de coté sous forme de pile)
     $ git stash pop [id] (depile et applique les dernieres modifs sauvegardées par git stash)
     $ git stash drop [id](dépile et supprime les dernieres modifs)
     $ git stash show  [id](dernieres modifications)
     $ git stash list (donne la liste d'id de chaque modifs) ------- man git stash (docu)
       

Fichier .gitignore : 
	Creer un fichier ****.gitignore (à enregistrer dans le depot) et mettre ce que l'on ne veut pas dedans par ex :
	*~
	*.bak
	*.o
	*.class
	Essai.java


Les branches : 
    Le merge est la reassociation entre une branche du projet et la branche du master.
    Creation de branche : $ git branch [experimental]
    liste des branches : $ git branch
    changer de branche : $ git checkout [experimental]
    merge : $ git merge experimental ---> Si conflit, merge s'arrête et les points problématiques sont indiqués.
    Pour les voir : $ git diff (On peut resoudre les problemes grâce à ça, puis commit -a)
    Suppression branche : $ git branch -d experimental
    Pour forcer : $ git branch -D branche_foireuse 

Etiqueter une version :
	$ git tag NOM [commit]      ex : git tag v1.0   ---> le [commit] peut etre la reference au commit ou quelque chose qui nous explique quel commit viser (ex : HEAD^)

Lister les tags existant : 
	$ git tag
Ressortir un commit tagé : 
	$ git checkout NOM


Identifier l'origine des changements : 
	$ git blame fichier


Identifier le commit à l'origine d'un probleme : 
	$ git bisect          ex : $ git bisect start
				   $ git bisect bad (derniere version par défaut si pas referenciée)
				   $ git bisect good v1.52

				   $ git bisect good (ou bad selon les tests) 


Pour faire des commits propres (courts, unitaires...) :
	- Selectionner ce que l'on ajoute pour un commit
		$ git add -p [fichier] (pose la question pour chaque modif)

	- Annuler un commit (en laissant une trace) : 
		$ git revert identifiant

	- Completer le dernier commit : ---> ATTENTION ! avant de partager avc git push par ex. et ne pas oublier de faire git add avant !
		$ git commit --amend
 

Annuler des changements / les derniers commits (totalement) :

	ATTENTION ! --> à éviter si les commits ont déjà été partagés

	$ git reset [mode] [identifiant commit] --> reinitialise le dépot au commit donné (en effaçant tous ce qui a été fait apres ce commit)

	mode :  --soft      reinitialise le dépot seulement (pas le répertoire de travail)
		--mixed     reinitialise le dépot et l'index (par défault)
		--hard      reinitialise tout y compris le repertoire de travail

	identifiant commit : par défault HEAD (= dernier commit)

ex : $ git reset HEAD^^ ---> supprime les deux derniers commits

     $ git reset --hard ----> reinitialise le repertoire de travail au dernier commit
	

Avant de faire un push, on aimerait revenir sur les derniers commits (pour les completer, en supprimer, en changer l'ordre, fusionner...) :

	$ git rebase -i origin/master	----> -i = mode interactif  // origin/master = origine des commits que l'on veut modifier
		--> un editeur est lancé avec la liste des commits qui vont être appliqués

 >>>> si probleme (conflit par ex), le rebase s'arrete pour qu'on puisse le corriger
	une fois corrigé : $ git rebase --continue  --->pour poursuivre
		ou alors : $ git rebase --skip      pour ignorer le commit qui pose probleme 
		ou : 	   $ git rebase --about     pour annuler l'opération rebase
    	 

Lors d'un travail à plusieurs,on souhaite ajouter notre travail apres de nombreux commits au travail realisé par mes collegues qui eux aussi ont fait des commits entre temps : 
		$ git pull --rebase


Creer un dépot git local :
	$ git init (Dans un répertoire donné)

Recuperer (faire une copie) un dépot : 
	$ git clone /chemin/vers/depot/ (depuis la source dans le repertoire ou l'on est)
	$ git clone ssh://login@machine/chemin/vers/depot/

	$ git pull  ---> recuperer les dernieres modifs
			--> eviter les push !
			
Travailler à plusieurs : 
	-> man gittutorial
	"USING GIT FOR COLLABORATION"
		--> bien fixer les droits d'acces :
			->fichers : lecture (r)
			->repertoire : lecture + execution (r + x)
			->repertoires parents : exécution


