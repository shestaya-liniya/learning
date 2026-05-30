# common

ls -R : recursively print files

grep / rg : find by symbol

sed : text transformation, replacement

awk : find column(s)/line(s) from file, very powerful
`awk -F ',' '{print $1}'` -> use ',' as the delimiter of columns and print column 1
`awk '/John/' file` -> print a line containing 'John' 
`awk -F ',' '{$1 > 10 print $1}'` -> if ids are in the fisrt column, return ids lower than 10

cut : dump column extractor
`cut -d ',' -f 1 file.csv` -> use ',' as the delimiter of columns and print column 1

sort : print sorted file  

# shell operators

echo "hello" > file : send output to a file

sort < names.txt : send names.txt as input to sort func
