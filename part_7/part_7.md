# Tableau et Boucle 

Les tableaux (arrays) en bash sont des structures de données qui permettent de stocker plusieurs valeurs dans une seule variable. Chaque valeur est identifiée par un indice numérique. 
Les tableaux en bash sont particulièrement utiles pour organiser et manipuler des données dans les scripts.

![](Aspose.Words.5d461e9c-aee7-4e3b-86c6-a90a397228ab.001.png)

```bash
numbers=(1 2 3 4 5 6 7)
echo $numbers
echo ${number[2]}
echo ${number[@]}
echo ${number[@]:1}
echo ${number[@]:1:2} # number[@]:début:fin
numbers+=(8)
echo ${number[@]}
unset number[2]
echo ${number[@]}
echo ${!number[@]}
number[0]=a
echo ${number[@]}
```

## Readarray

readarray (aussi connu sous le nom de mapfile) est une commande intégrée de bash qui permet de lire des données provenant de l'entrée standard (stdin) ou d'un fichier et de les stocker dans un tableau (array). 
Cette commande est particulièrement utile pour lire des fichiers ligne par ligne et stocker chaque ligne dans un élément du tableau.

```bash
touch days.txt
echo lundi >> days.txt
echo mardi >> days.txt
echo mercrdi >> days.txt
echo jeudi >> days.txt
echo vendredi >> days.txt
echo samedi >> days.txt
echo dimanche >> days.txt
```

```bash
readarray days < days.txt
echo ${days[@]}
echo ${!days[@]}
echo ${days[@]@Q}
readarray -t days < days.txt
echo ${days[@]@Q}
```

## Array + for loops

Une boucle for en bash est une structure de contrôle utilisée pour répéter un bloc de code pour chaque élément d'un ensemble d'éléments. Les boucles for sont souvent utilisées en combinaison avec des tableaux (arrays) pour effectuer des opérations sur chaque élément du tableau.

### Premier exemple

```bash
nano for_loop.sh
```

```bash
for element in first second third; do
  echo "This is $element"
done
```
```bash
chmod 744 for_loop.sh
```

```bash
bash for_loop.sh
```

### Second exemple

```bash
nano for_loop.sh
```

```bash
readarray -t files < files.txt

for file in "${files[@]}"; do
  echo "$file"
done
```

```bash
chmod 744 for_loop.sh
```

```bash
touch files.txt
echo lol1 >> files.txt
echo lol2 >> files.txt
echo lol3 >> files.txt
```

```bash
bash for_loop.sh
```
### Troisième exemple

```bash
nano for_loop.sh
```

```bash
readarray -t files < files.txt

for file in "${files[@]}"; do
	if [ -f "$file" ]; then
		echo "$file already exists"
	else
		touch "$file"
		echo "$file was created"
	fi
done
```

```bash
chmod 744 for_loop.sh
```

```bash
touch files.txt
echo lol1 >> files.txt
echo lol2 >> files.txt
echo lol3 >> files.txt
```

```bash
bash for_loop.sh
```
