# Flow Control

Flow control is the bread and butter of programming. It is how you can program different paths for the program to take or to loop through a task many times. Let's create a new file for this section, "flow_control.py".

## If,elif,else statements

- An "If statement" is a programming construct that allows you to execute code based on if a condition is met.

- If, elif (else if), and else statements are used in python to control what happens based on the circumstance of one or more events:
    +  <img src="figures/cf16e796.png" alt="if flow" width="600px"/>

- The following are valid orders of statements. In both scenarios where elif is, as many elif statements can be there as desired.
    +  <img src="figures/92a150bb.png" alt="if flow" width="600px"/>

\*\*\***INDENTATION MATTERS!!!**\*\*\*

In many other languages, the "body" of an "if statement" (or any other programming construct that has a "body") is designated by curly braces. However, python doesn't do that. Instead, the "body" is designated by indentation. Any code that is indented to the same level is considered to be part of the same "body". However, you should not mix tabs and space characters. The "condition" of the if statement is evaluated to be True or False. If True, then the code block associated with that statement is executed and not any others. If False, then the next statement is evaluated. "else" is the catchall default.

```
print("\nIF Statements\n")


print("\nIF Statement 1\n")
diffexp = 67
if (diffexp > 0):
    print("Upregulated")
else:
    print("Downregulated")

print("\nIF Statement 2\n")
diffexp = -9
if (diffexp > 0):
    print("Upregulated")
else:
    print("Downregulated")

print("\nIF Statement 3\n")
# An if statement doesn't need an else
if (diffexp < 0):
    print("Downregulated")

print("\nIF Statement 4\n")
# If statements can have multiple elif (else if)
# Try changing the value of diffexp to see how the output changes.
# The if statement below has a logical error, see if you can find it.
diffexp = 25
if (diffexp > 50):
    print("Very Upregulated")
elif (diffexp > 0):
    print("Upregulated")
elif (diffexp < 0):
    print("Downregulated")
elif (diffexp < -50):
    print("Very Downregulated")

print("\nIF Statement 5\n")
# You can use "and", "or", & "not" to write more complex conditions
if (diffexp > 0 and diffexp < 50):
    print("Differential expression between 0 and 50")

print("\nIF Statement 6\n")
if (diffexp < -50 or diffexp > 50):
    print("High Down or Up regulation")

print("\nIF Statement 7\n")
# The body of an if statement can have multiple lines of code
diffexp=25
if (diffexp > 0 and diffexp < 50):
    print("Differential expression between 0 and 50")
    print("Check the significance")

print("\nIF Statement 8\n")
# You can have nested if statements
sig = 0.049
if (diffexp > 0 and diffexp < 50):
    print("Differential expression between 0 and 50")

    if (sig < 0.05):
        print("It's significant!")
```

**PRACTICE**: Create a gene expression dictionary like the one from the Dictionary section to use below. Write an if statement (or statements) that do the following:
* if both SYF2 and FBX04 exist in the dictionary and both are upregulated (i.e. values > 0), then print "GO:1"
* Otherwise, if ATF2 does not exist in the dictionary or PLK1 exists and is downregulated (i.e. value < 0), then print "GO:2"
* Otherwise, if HUS1B exists and HUS1B is downregulated or SYF2 does not exist, then print "GO:3"
* Otherwise, print "GO:4"

Change the keys and values in your dictionary to get each of the print statements to execute.


# For Loops

A "For Loop" is a programming construct that is used to run a task many times in a row, where you know how many times you want to loop.

### Iterating using indices

```
print("\nFor Loops\n")

# The range(n) function returns values from 0 to n-1
for i in range(5):
    print(i)
```

### Iterating through a List

```
gene_list = ["DDX11L1","WASH7P","MIR6859-1","MIR1302-2HG","MIR1302-2","FAM138A"]

print("\nIterating through a list\n")

for id in gene_list:
    print(id + " is a gene of interest")
```

### Iterating through a Dictionary

```
gene_exp_dict = {"DDX11L1":43.2,"WASH7P":45,"MIR6859-1":60.1,"MIR1302-2HG":12,"MIR1302-2":0.5,"FAM138A":23}

print("\nIterating through a dictionary\n")

for gene in gene_exp_dict.keys():
    print("Gene", gene, "has expression value:", gene_exp_dict[gene])
```


# While Loops

A "While Loop" is used when you don't know how many times something will loop. The body of the loop will continue to execute, over and over, until the loop condition becomes false.

```
print("\nWhile Loops\n")

n = 1
fact = 1
while (n < 8):
    fact = fact * n
    n += 1
print(fact)
```

### Break & Continue

'break' and 'continue' are two commands that can be used in loops. 'break' exits the loop and 'continue' skips the rest of the loop body (for the current iteration) and starts with the next iteration of the loop.

```
gene_list = ["DDX11L1","WASH7P","MIR6859-1","MIR1302-2HG","MIR1302-2","FAM138A"]


print("\nBreak\n")

for id in gene_list:
    print(id + " is a gene of interest")
    if (id == "MIR1302-2HG"):
        break

print("\nContinue\n")

for id in gene_list:
    if (id == "MIR1302-2HG"):
        continue

    print(id + " is a gene of interest")
```

**PRACTICE**: Using your personnel dictionary (from the Dictionary practice), use a single loop to print out all of the information for all of the employees. Using the gene expression dictionary (from the Dictionary practice), use multiple nested loops to print out all of the expression values individually for each sample.

# Functions

A function is a block of code that only gets run when it is called. It can take multiple parameters and can return values as well. Functions are an integral part of making reusable and clear code. 

```
# imports are used to be able to use code from other libraries
import math

print("\nFunctions\n")

print("\nFunction 1\n")
# Functions can have zero parameters and return nothing
def hello():
    print("Hello, World!")

hello()

print("\nFunction 2\n")
# Or they can have multiple parameters and return something
def logfc(exp1,exp2):
    retval = math.log(exp2/exp1)
    return(retval)

gene_exp_dict = {"DDX11L1":43.2,"WASH7P":45,"MIR6859-1":60.1,"MIR1302-2HG":12,"MIR1302-2":0.5,"FAM138A":23}

de = logfc(gene_exp_dict['WASH7P'], gene_exp_dict['FAM138A'])
print("The DE value is", de)

print("\nFunction 3\n")

# They can also have default values for any of the parameters
def logfc(exp1,exp2,sigdig=3):
    retval = math.log(exp2/exp1)
    retval = round(retval, sigdig)
    return(retval)

print(logfc(89,12,5))
print(logfc(89,12))
```

## Scope: Local vs. Global variables

When a variable is defined outside of a function, it is known as a Global Variable. Variables defined inside functions are called Local Variables. A local variable is only accessible within the function, whereas a global variable can be accessed anywhere. It is generally good programming practice to use local variables in functions, and not global ones. If you need to access a global variable inside a function, you should pass it in as a parameter.

```
# this will produce an error!
def hello():
    myvar=3

hello()
print(myvar)
```

**PRACTICE**: Write a function to calculate the Fibonacci numbers given a maximum value. Return a list of Fibonacci numbers below that value.

For example, if the max is 100, the return value from the function should be:
[1,1,2,3,5,8,13,21,34,55,89]


# File Handling

Reading from and writing to files is a integral part of programming. First let's [download a TSV (tab separated values) file](data/DMR.GBM2.vs.NB1.tsv). Make sure to save it to the directory that your code is in.

```
print("\nFile Handling\n")

# open the file for reading
f = open("DMR.GBM2.vs.NB1.tsv", "r")
print(f.readline())
print(f.readline())

# you can use a loop to read the whole file, line by line
f2 = open("DMR.GBM2.vs.NB1.tsv", "r")
for line in f2:
    print(line)

# always close file handles when you're done with them
f.close()
f2.close()
```

Now let's try writing to a file. When opening a file for writing, you can use either "w" for (over)write or "a" for append.

```
# open a new file for writing, will create if doesn't exist
f3 = open("myfile.txt", "w")
f3.write("Hello World!")
f3.close()

# read the whole file at once
f4 = open("myfile.txt","r")
print(f4.read())
f4.close()

# Now append to the file
f3 = open("myfile.txt", "a")
f3.write("How are you?")
f3.close()

f4 = open("myfile.txt","r")
print(f4.read())
f4.close()
```

**PRACTICE**: Using your personnel dictionary, loop through the employees and create a TSV with one employee per line. You will need to use the tab character, which is "\t". Make sure to have a header line. Do the same for the gene expression dictionary.


# Errors

As you code more, you will certainly run into different kinds of errors. In python there are 3 main types of errors: Syntax, Logical, and Runtime. 

### Syntax error

A syntax error is an error arising from writing incorrect python code. Most syntax errors arise from typos, improper indentation, or incorrect function usage. 

```
print("\nErrors\n")

# This will produce a syntax error in the terminal
print "Hello World!"
```

### Logical error

Logical errors are the hardest to find because the python interpreter cannot catch them for you. It is an error that is based on an incorrect coding of whatever algorithm you are trying to create.

```
# this will run, but the average is not calculated
# correctly. Python follows the Order of Operations.
x = 3
y = 4
average = x + y / 2
print(average)
```

### Runtime error

Because python is an interpreted language, some errors will only get produced when that piece of code is actually run. Common examples of runtime errors are using an undefined variable or mistyping the variable name. 

```
# this will NOT produce an error, even though myVar is undefined
# because the function does not get called
myvar = 9
def px():
    print(myVar)
```

```
# This will produce the error when the function is called
myvar = 9
def px():
    print(myVar)
px()
```

**It is important that you look at the output of syntax or runtime errors and use it to figure out the problem. The python interpreter will give you the line number of where the error occurred and the specific error that it found. This is very useful in fixing your problem. Logical errors are harder to figure out and as a beginner it is easiest to add print statements in your code to figure out where things went wrong.**