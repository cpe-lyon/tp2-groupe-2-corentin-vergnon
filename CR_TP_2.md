## Exercice 1. Variables d’environnement

1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur?

Ils trouvent les commandes tapées par l'utilisateur dans le dossier **/usr/bin/**.



2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel?

C'est la variable d'environnement $HOME.

Commande : cd $HOME



3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.

- PWD : répertoire courant
- OLDPWD : le répertoire ou on était avant
- LANG : définit la langue et l'encodage que les logiciels utilisent pour communiquer avec l'utilisateur.
- SHELL : définit l'emplacement du shell
- _ : 



4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.

Commande : **MY_VAR="TestVariable"**
On vérifie qu'elle existe en utilisant **echo $MY_VAR**.
Le shell affiche bien "TestVariable".



5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.

La commande **bash** permet de lancer un nouveau bash. 
La variable locale MY_VAR n'existe pas dans ce deuxième bash, puisqu'elle est locale au premier bash.
En utilisant la commande **exit**, on revient au bash initial et on retrouve notre variable locale.



6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.

On utilise la commande **export MY_VAR="TestVariableEnv"**
On utilise ensuite **bash** pour créer un nouveau bash.
Cette fois-ci, avec **echo $MY_VAR**, la variable d'environnement est toujours présente.

Cela s'explique par le fait qu'une variable d'environnement est une variable globale et non locale.



7. Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace. Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.

Commande : **export NOMS="VERGNON"**
**echo $NOMS**
L'affectation a bien fonctionné.



8. Ecrivez une commande qui aﬀiche ”Bonjour à vous deux, binôme1 binôme2!” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS.

Commande : **echo Bonjour à toi, $NOMS**



9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset ?

En utilisant la commande **unset**, on libère l'espace mémoire.
Si le contenu de la variable est vide, elle a toujours un emplacement mémoire qui lui est dédié.



10. Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)

Commande : **echo '$HOME' = $HOME**



## Exercice 2 : Contrôle de mot de passe


```
#!/bin/bash
PASSWORD='corentin_vergnon'
read -s -p "Saisissez le mot de passe : " temp_pwd
if [ $PASSWORD = $temp_pwd ]; then 
	echo 'Mot de passe correct'
else
	echo 'Mot de passe incorrect'
fi
```



## Exercice 3 : Expressions rationnelles

```
#!/bin/bash

function is_number
{
	re='^[+-]?[0-9]+([.][0-9]+)?$'
	if ! [[ $1 =~ $re ]] ; then
		return 1
	else
		return 0
	fi
}

if is_number $1; then
	echo "C'est un nombre.";
else 
	echo "Ce n'est pas un nombre.";
fi
```


Note sur les retours d'une fonction :
- Soit la fonction return avec une valeur, on récupère alors le dernie rreturn avec un $
- Soit la fonction "echo", on peut récupérer le résultat dans une variable : my_var = $(appel_fonction)





## Exercice 4 : Contrôle d'utilisateur

```
#!/bin/bash

if [ -z $1 ]; then
	echo "Utilisation : $0 nom_utilisateur";
else 
	temp=$(cut -d":" -f1 /etc/passwd | grep $1)
	if [ "x$temp" = "x$1" ]; then
		echo "Utilisateur trouvé";
	else
		echo "Impossible de trouver l'utilisateur $1";
	fi
fi 
```



## Exercice 5 : Factorielle

```
#!/bin/bash

if [ -z $1 ]; then
	echo "Utilisation : $0 entier_naturel";
else 
	a=1
	for i in $(seq 1 $1)
	do 
		a=$(($a * $i))
	done	
fi
echo "$1! = $a"
```



## Exercice 6 : Le juste prix

```
#!/bin/bash

random=$(( $RANDOM % 1000 ))
read -p "Saisissez un entier : " number
while ! [ $random = $number ]; do
	if [ $random -gt $number ]; then
		echo "C'est plus."
	else
		echo "C'est moins." 
	fi
	read -p "Saisissez un entier : " number
done
echo "Bravo, le juste prix est $random !"
```







