# Lecture de fichier et while loops

## While loops

Les boucles while en bash sont des structures de contrôle qui permettent de répéter l'exécution d'un bloc de code tant qu'une certaine condition est vraie. Elles sont souvent utilisées pour traiter des données de manière itérative, comme parcourir des fichiers ligne par ligne, ou pour exécuter des tâches répétitives jusqu'à ce qu'une condition spécifique soit satisfaite.

```bash
nano while.sh
```
```bash
read -p "Enter your number: " num

while [ $num -gt 10 ]; do
	echo $num
done
```
```bash
chmod 744 while.sh
```
```bash
bash while.sh
```

On définit une boucle qui boucle à l’infini dès qu’on rentre un chiffre supérieur à 10

```bash
nano while.sh
```
```bash
read -p "Enter your number: " num

while [ $num -gt 10 ]; do
	echo $num
	num=$(( $num - 1 ))
done
```
```bash
chmod 744 while.sh
```
```bash
bash while.sh
```

## Read-while loops

Les boucles while avec la commande read en bash sont utilisées pour lire des données, généralement à partir de l'entrée standard (stdin) ou d'un fichier, ligne par ligne, et effectuer des actions sur chaque ligne. Cette technique est particulièrement utile pour traiter des fichiers texte et exécuter des commandes sur chaque ligne.

```bash
touch file_test.txt
```

```bash
echo lol1 >> file_test.txt
echo lol2 >> file_test.txt
echo lol3 >> file_test.txt
```

```bash
nano read_while.sh
```
```bash
while read line; do
	echo "$line"
done < "$1"
```
```bash
chmod 744 read_while.sh
```
```bash
bash read_while.sh
```

“$1” permet de dire à la boucle de prendre le premier positional parameter
