# Variable and shell Expension

Dans Linux, une variable est un symbole ou un nom qui contient une valeur. Elle peut être utilisée pour stocker une valeur, une chaîne de caractères ou une référence à un fichier ou à un répertoire. Les variables sont souvent utilisées dans les scripts shell pour stocker des informations temporaires ou pour simplifier la réutilisation de données. Elles peuvent être créées, modifiées et supprimées à l'aide de commandes spécifiques dans le terminal. Les variables peuvent également être transmises entre différents programmes et scripts pour faciliter l'automatisation des tâches

![](Aspose.Words.084bf0ca-5bee-42c0-bdcf-4169498c0478.001.jpeg)

## Variable

```bash
touch variable_practice.sh
nano variable_practice.sh
```

```bash
#!/usr/bin/bash
employee="Sarah"
echo "Dear ${employee}"
echo "The board and i would like to thank you for the excellent work that you have been doing over the last month"

echo "Keep up the good work, ${employee}"

echo "Best wishes"
```

```bash
chmod +x variable_practice.sh
bash variable_practice.sh
```

Explication :

- La variable employee stocke la chaîne de caractère Sarah
- Par convention les variables user\_define sont en minuscule (les shell variable, elles sont en majuscule)
- En bash, on ne met pas d’espace pour l’affectation d’un variable typé, car sinon elle sera traitée comme une commande
- On respecte le concept DRY(Don’t reapeat yourself) si jamais on doit utiliser la valeur, on utilise directement la variable employee, si on change la valeur de employee de “Sarah” à “John” pas besoin de le faire partout juste dans employee, ça évite de créer des erreurs

## Bash shell variable


```bash
echo $PATH
```
PATH : contient la liste des dossiers où shell va chercher les différentes exécutable.

```bash
echo $HOME
```
HOME : contient le chemin absolue du dossier “home” de l’utilisateur

```bash
echo $USER
```
USER : contient le nom de l’utilisateur

```bash
echo $HOSTNAME
```
HOSTNAME : contient le nom de l’ordinateur

```bash
echo $HOSTTYPE
```
HOSTTYPE : contient le type d’architecture de l’ordinateur

CONTRAIREMENT AU VARIABLE USER DEFINE LES VARIABLES SHELL SONT EN MAJUSCULE

## Parameter expansion trics

Parameter expansion est une fonctionnalité du shell Bash utilisée pour manipuler les variables et les chaînes de caractères dans Ubuntu (un système d'exploitation de type Linux). 
Cela permet de faire des substitutions, des extractions et des transformations de chaînes de caractères, ainsi que de créer des variables avec des noms dynamiques en utilisant des modificateurs spécifiques. 
Parameter expansion est souvent utilisé pour créer des scripts de shell plus efficaces et automatiser les tâches dans Ubuntu.

Lower case: Les différentes opérations pour mettre en minuscule une chaîne de caractères

- On affecte la valeur à une variable

```bash
name=JoJo
echo $name
```

- On affiche la valeur de la variable transformé

```bash
name=JoJo
echo ${name}
```
```bash
name=JoJo
echo ${name,}
```
```bash
name=JoJo
echo ${name,,}
```

Upper case : Les différentes opérations pour mettre en majuscule une chaîne de caractères

```bash
name=JoJo
echo ${name^}
```
```bash
name=JoJo
echo ${name^^}
```
Length : Permet d’afficher la longueur d’une chaîne de caractère

```bash
name=JoJo
echo ${#name}
```

Truncate : permet d’extraire une sous chaîne d’une chaîne de caractère

![](Aspose.Words.084bf0ca-5bee-42c0-bdcf-4169498c0478.017.png)

```bash
name=JoJo
echo ${name:0:7}
```

```bash
name=JoJo
echo ${name:3:7}
```

```bash
name=JoJo
echo ${name:3:10}
```

## Commande substitution

Permet de stoker les résultats d’une commande

```bash
nano subcription_script.sh
```

```bash
#!/bin/bash

time=$(date +%H:%m:%S)
echo "Hello, $USER, the time right now is $time"
exit 0
```

```bash
chmod +x subcription_script.sh
```

Rappel :

![](Aspose.Words.084bf0ca-5bee-42c0-bdcf-4169498c0478.022.png)

```bash
nano arithmetic.sh
```
```bash
#!/usr/bin/bash


echo $((4 + 2))

x=4
y=2
echo $((x + y))
echo $((x - y))
echo $((x / y))
echo $((x * y))

exit 0
```
![](Aspose.Words.084bf0ca-5bee-42c0-bdcf-4169498c0478.025.png)

## Tilde expansion

L'expansion Tilde (ou tilde expansion en anglais) est une fonctionnalité dans Ubuntu qui permet de raccourcir les chemins d'accès en utilisant le caractère tilde (~) pour représenter le répertoire personnel de l'utilisateur. Cela permet de simplifier les commandes en ligne de commande et d'accéder rapidement aux fichiers et dossiers dans le répertoire personnel.

### Accès à home & root

```bash
echo ~
echo ~root
```
### Accès au répertoire courant

```bash
echo pwd
```
## Brace expansion

La Brace expansion est une fonctionnalité dans Ubuntu qui permet à l'utilisateur de générer rapidement et efficacement une liste de chaînes de caractères en utilisant des accolades pour définir un ensemble de possibilités.

### String list :

Permet de gérer des liste de chaîne de caractère

```bash
echo {a,19,z,barry,19}
```
```bash
echo {a,19,z,barry, 19}
```
```bash
echo {jan,feb,mar,apr,may,jun}
```

### Range list : 
Permet de gérer des liste de nombres et lettres

```bash
echo {1,2,3,4,5,6,7,8,9,10}
```

```bash
echo {1..10}
```

```bash
echo {10..1}
```

```bash
echo {a..z}
```

```bash
echo {1..1000..2}
```

```bash
echo month{1..12}
```