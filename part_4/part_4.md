# Input d'utilisateur

## Positional parameters

Les "positional parameters" (paramètres positionnels) en bash font référence aux arguments passés à un script ou une fonction lors de son exécution. Ils sont appelés "positionnels" parce qu'ils sont associés à leur position dans la liste des arguments fournis.

Exemple :

```bash
nano positional_script.sh
```

```bash
#!/bin/bash
echo "My name is ${1}"
echo "My name directory is ${2}"
echo "My favorite colour is ${3}"
```

```bash
chmod 744 positional_script.sh
```

```bash
bash positional_script.sh john $HOME blue
```
Compte tenu de cela, que feriez-vous si l'utilisateur ne voulait ajouter que 4 numéros, par exemple pour contourner ce problème, réfléchissez à la manière dont vous pourriez utiliser une astuce d'expansion des paramètres

comme ${parameter:-word}

pour substituer une valeur par défaut si un paramètre positionnel donné n'est pas fourni.

Vous pouvez vous référer au manuel GNU Bash pour plus de clarté sur l'utilisation de ce avec ce [lien](https://www.gnu.org/software/bash/manual/bash.html#Shell-Expansions)

## Special parameter:

Les "special parameters" (paramètres spéciaux) en bash sont des variables prédéfinies qui contiennent des informations sur l'environnement d'exécution, le script ou la commande en cours, les arguments passés et d'autres aspects liés au shell.

```bash
nano positional_script.sh
```

```bash
#!/usr/bin/bash

echo "My name is ${1}"
echo "My name directory is ${2}"
echo "My favorite colour is ${3}"

echo $#
```

```bash
bash positional_script.sh
```
si vous avez bien exécuté les commandes, vous devriez voir 3 à la fin, c'est le nombre de paramètres entré dans notre script (john $HOME blue)

maintenant :

```bash
nano positional_script.sh
```

```bash
#!/usr/bin/bash

echo "My name is ${1}"
echo "My name directory is ${2}"
echo "My favorite colour is ${3}"

echo $#
echo $0
```

```bash
bash positional_script.sh
```

il s’agit du nom du script.

Voyons le sens du $@ avec un exemple :

```bash
nano special.sh
```

```bash
#!/usr/bin/bash

echo $@
```

```bash
chmod 744 special.sh
bash special.sh 1 2 3 4 5 6 7 8 9
```

```bash
ls
```

```bash
rm 1 2 3 4 5 6 7 8 9
```


il ”unpack” les différents paramètres $@ : $1 $2 $3 … $N

Maintenant, nous allons faire les commande suivante :

```bash
nano special.sh
```

```bash
#!/usr/bin/bash

touch $@
```

```bash
chmod 744 special.sh
bash special.sh "test super" "generate file"
```

```bash
ls
```

```bash
rm test super generate file
```

puis :

```bash
nano special.sh
```

```bash
#!/usr/bin/bash

touch "$@"
```

```bash
chmod 744 special.sh
bash special.sh "test super" "generate file"
```

```bash
ls
```

```bash
rm "test super" "generate file"
```

## Read command

Permet de lire une valeur fournit par l'utilisateur et de l'affecter à une variable 
exemple :
```bash
- read input1 input2
```
```bash
- echo $input1
- echo $input2
```

utilisons la commande read dans un script :

```bash
nano read.sh
```
```bash
#!/bin/bash

read  name age name

echo “my name is $name”
echo “my age is $age”
echo “i live in $town”
```

```bash
chmod 744 read.sh
bash read.sh
```

Comme pour le positionnal on doit également savoir la valeur améliorons ça :

amélioron cela :
```bash
nano read.sh
```
```bash
#!/bin/bash

read -p “Input first name : ” name
read -p “Input first age : ” age
read -p “Input first town : ” name

echo “my name is $name”
echo “my age is $age”
echo “i live in $town”
```

```bash
chmod 744 read.sh
bash read.sh
```
-p permet d’ajouter une information à l’utilisateur

si le temps est une ressource importante et que vous voulez que le script continue même si l’utilisateur n’a rien tapé, alors il suffit d’ajouter l’argument -t nombre\_de seconde

exemple pour une attente de 5 secondes :

```bash
nano read.sh
```
```bash
#!/bin/bash

read -t 5 -p “Input first name : ” name
read -t 5 -p “Input first age : ” age
read -t 5 -p “Input first town : ” name

echo “my name is $name”
echo “my age is $age”
echo “i live in $town”
```

```bash
chmod 744 read.sh
bash read.sh
```

si pour des raisons de sécurité vous ne voulais pas ajouter les printing sur l’écran ‘ex: mot de passe utiliser l’argument -s

exemple pour une attente de 5 secondes et rende invisible les information :

```bash
nano read.sh
```
```bash
#!/bin/bash

read -s -t 5 -p “Input first name : ” name
read -s -t 5 -p “Input first age : ” age
read -s -t 5 -p “Input first town : ” name

echo “my name is $name”
echo “my age is $age”
echo “i live in $town”
```

```bash
chmod 744 read.sh
bash read.sh
```
## Select Command

la commande select permet de pré-définir la plage de valeur possible pour un variable et les précise à l’utilisateur

créer le script select.sh puis écrire les différente ligne affichée une fois fais exécuter le script

```bash
nano select.sh
```
```bash
#!/bin/bash

select day in mon tue wed thu fri sat sun
do
echo "the day of the week is $day"
done
```

```bash
chmod 744 select.sh
bash select.sh
```

on peut voir un effet de looping (le script demande toujours de nouvelles entrées) pour gérer ce phénomène, on doit ajouter le terme break

```bash
nano select.sh
```
```bash
#!/bin/bash

select day in mon tue wed thu fri sat sun
do
echo "the day of the week is $day"
break
done
```

```bash
chmod 744 select.sh
bash select.sh
```
Nous pouvons grâce à la variable PS3 définir une phrase claires pour aider l’utilisateur


```bash
nano select.sh
```
```bash
#!/bin/bash

PS3="What is the day of the week ? :"
select day in mon tue wed thu fri sat sun
do
echo "the day of the week is $day"
break
done
```

```bash
chmod 744 select.sh
bash select.sh
```