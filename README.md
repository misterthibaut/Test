# Test

Recuperer une copie local : ds un terminal : git clone "URL"
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

	git commit -s :  fait autmatiquement le "add" pour les fichiers deja connus de git
	git commit -- fichier : le fichier est ajouté pour le commit
	git commit -m "message" : Ecris le message directement



Revoir les commits : 

	$ gitk (interface graphique)
	$ git log (affiche dans le terminal)
	$ git log -p (affiche les modifications en plus)
	$ git log --stat --summary (n'affiche pas toutes les modifs mais juste ce qui a ete modif et le nombre de lignes modifiées, cest une version simplifiée)
	$ git log --oneline (résumé des commit sur une ligne)	

Envoyer /recevoir les modifs  vers/depuis un serveur : 

	Envoyer : $ git push

	Recevoir : $ git pull

	$ git fetch (recupere ET integre les changements)
	


          
