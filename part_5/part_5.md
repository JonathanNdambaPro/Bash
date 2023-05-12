# Logique

## Chainage des commandes avec les opérateurs de liste

Les opérateurs de liste en bash permettent d'exécuter plusieurs commandes les unes après les autres, en contrôlant l'ordre d'exécution et en déterminant si les commandes suivantes doivent être exécutées ou non en fonction du succès ou de l'échec des commandes précédentes.

- List : quand on mets au moins une commande pour une ligne
- List operator : type d’opérateur de contrôle qui permet de créer une liste de commande


exemple :
```bash
- echo 123 & echo 456
```
```bash
- echo 123 ; echo 456
```
```bash
- echo 123 && echo 456
```
```bash
- echo 123 || echo 456
```
```bash
- ls whatever && echo 456
```
```bash
- ls whatever || echo 456
```

![](Aspose.Words.3c439610-78f9-4ab9-b070-b54ce280e67c.001.png)

- & : permet de lancer les commandes de manière asynchrone (parallèles)
- ; : permet de lancer les commandes de manière synchrone (en série)
- && : (et logique) lance les commandes suivante uniquement si les précédentes marche (exit code zéro)
- || : lance les commandes suivant uniquement si la première échoue (on peut le voir comme un backup de la première commande)

## Commande de tests + opérateurs conditionnels

 l'opérateur conditionnel ([ ] ou [[ ]]) en bash sont utilisés pour évaluer des expressions conditionnelles et tester des valeurs. 

Exemple :
```bash
[ 2 -eq 2 ] ; echo $? # (en bash 0 = vrai et 1 = faux comme les exit code vu précédement)
```
```bash
[ 1 -eq 2 ] ; echo $?
```
```bash
[ 1 -ne 2 ] ; echo $?
```
```bash
[ 2 -ne 2 ] ; echo $?
```
- -eq : égale à
- -ne : non égale à
- -gt : greater than (plus grand que)
- -lt : least than (moins que)
- -geq : greater or equal
- -leq : least or equal

```bash
a=hello
```
```bash
b=salut
```
```bash
[[ $a = $b ]]; echo $?
```
```bash
[[ $a != $b ]]; echo $?
```
```bash
[[ -z $c ]]; echo $? (vide ou non ? zero)
```
```bash
c=anything
```
```bash
[ -z $c ]]; echo $?
```
```bash
[ -n $c ]]; echo $? (non-vide ou non ? not-zero)
```
```bash
[[ -e today.txt ]]; echo $? (le fichier existe ou non ?)
```
```bash
touch today.txt
```
```bash
[[ -e today.txt ]]; echo $?
```
```bash
[[ -f today.txt ]]; echo $? (est-ce un fichier ?)
```
```bash
[[ -d today.txt ]]; echo $? (est-ce un dossier ?)
```

# IF statements :

La condition if en bash est une structure de contrôle utilisée pour exécuter des blocs de code en fonction de l'évaluation d'une expression conditionnelle. Si l'expression conditionnelle est vraie (c'est-à-dire que son code de sortie est égal à 0), le bloc de code associé est exécuté. 
Vous pouvez également utiliser des instructions elif et else pour tester des conditions supplémentaires ou exécuter un bloc de code par défaut si aucune condition n'est satisfaite.
```bash
nano if.sh
```

```bash
if [ 2 -gt 1] then
  echo test passed
fi
```

```bash
chmod 744 if.sh
```
```bash
bash /if.sh
```

modifier le code avec :
```bash
nano if.sh
```

```bash
if [ 2 -eq 1] then
  echo test passed
elif [ 1 -eq 1]; then
  echo second test passed
else
  echo test failed
fi
```

```bash
chmod 744 if.sh
```
```bash
bash /if.sh
```


On peut coupler des conditions pour les vérifier en même temps
- && : et logique, les deux condition doivent être vérifié
- || : ou logique, au moins une des deux conditions doit être vérifiée

```bash
nano if_combine.sh
```

```bash
a=$(cat file1.txt)
b=$(cat file2.txt)
c=$(cat file3.txt)

if [[ $a = $b ]] && [[ $a = $c ]]; then
  rm file2.txt file3.txt
else
  echo "Files don't match"
fi
```

```bash
chmod 744 if_combine.sh
```
```bash
echo “pareil” > file1.txt
echo “pareil” > file2.txt
echo “pareil” > file3.txt
```
```bash
bash if_combine.sh
```

```bash
echo “pareil” > file1.txt
echo “pareil” > file2.txt
echo “différent” > file3.txt
```
```bash
bash if_combine.sh
```

## CASE statements

Le case statement en bash, également appelé "case construct" ou "switch case", est une structure de contrôle utilisée pour effectuer différentes actions en fonction de la valeur d'une variable ou d'une expression. 

Il est particulièrement utile lorsque vous avez besoin de tester plusieurs valeurs possibles pour une variable et d'exécuter un bloc de code spécifique pour chaque valeur.

```bash
nano case_script.sh
```

```bash
read -p "Please enter number: " number
case "$number" in
	[0-9]) echo "you've enter a single digit number";;
	[0-9][0-9]) echo "you've enter two digit number";;
	[0-9][0-9][0-9]) echo "you've enter three digit number";;
	*) echo "you've entre more than three digit";;
esac
```
```bash
chmod 744 case_script.sh
bash case_script.sh
```
