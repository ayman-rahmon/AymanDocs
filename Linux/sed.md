# Sed


sed is a String streaming tool that helps you find and replace patterns.


## substitutions:
```
sed 's/find/replace/'  < inputFile  > outputFile #  (this command will be the basic substitution command - first instance in each line)
sed 's/find/replace/g'  < inputFile  > outputFile #  (this command will be the basic substitution command - every instance in each line) we did this by giving it the global flag- like in regex -
sed 's/find/replace/g' inputAndOutputFile   # when writing on the same file we don't need any symbols
sed '/find/s/find/replace/'  # this means that you wanna find a line that has some pattern and change some other pattern in the same line.
sed '/find/d' # delete lines that has the pattern...
sed -e 's/find/replace/g' -e 's/find/replace/g'  # this is considering the situation where you're doing multiple finding and replacing in one command.
```

## printing:
```
sed -n '/find/p' # print the lines that contains the pattern (like grep)

```

## tricks and tips:
```
# you can delete white space in the end of lines using some sed and regex trickery...like the following:
sed -i 's/ *//' # this means replace every white space with it's reaccurunces in the end of the lines with nothing (deleting them). -- useful for deleting whitespaces in the end of lines in files.
# you can also delete tabs at the end of lines::
sed -i 's/[[:space:]]*$//'
# you can also get rid of empty lines using sed.
sed '/^$/g'
# replace all lowercase chars with uppercase letters.
sed 's/[a-z]/\U&/g'
sed 's/[a-z]/\L&/g'
# using sed as a replacement of the head command:
sed 11q file
# you can remove all of the comments in a file using sed like :
sed 's/#.*//g'
sed 's/#.*/d'
```
