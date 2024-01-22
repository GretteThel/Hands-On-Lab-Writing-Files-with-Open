# Hands-On-Lab-Writing-Files-with-Open

# Table of Contents

Writing Files
Appending Files
Additional File modes
Copy a File

# Writing Files
We can open a file object using the method write() to save the text file to a list. To write to a file, the mode argument must be set to w. Let’s write a file Example2.txt with the line: “This is line A”

**# Write line to file**
exmp2 = '/Example2.txt'
with open(exmp2, 'w') as writefile:
    writefile.write("This is line A")

We can read the file to see if it worked:
**# Read file**

with open(exmp2, 'r') as testwritefile:
    print(testwritefile.read())

EXPECTED RESULT:
This is line A

We can write multiple lines:
**# Write lines to file**

with open(exmp2, 'w') as writefile:
    writefile.write("This is line A\n")
    writefile.write("This is line B\n")

The method .write() works similar to the method .readline(), except instead of reading a new line it writes a new line. The process is illustrated in the figure. The different colour coding of the grid represents a new line added to the file after each method call.

![image](https://github.com/GretteThel/Hands-On-Lab-Writing-Files-with-Open/assets/117958967/6ada0e93-c60b-47ee-bb93-dec5627293df)

You can check the file to see if your results are correct

**# Check whether write to file**

with open(exmp2, 'r') as testwritefile:
    print(testwritefile.read())

EXPECTED RESULT:    
This is line A
This is line B

We write a list to a .txt file as follows:

**# Sample list of text**

Lines = ["This is line A\n", "This is line B\n", "This is line C\n"]
Lines

EXPECTED RESULT:    
['This is line A\n', 'This is line B\n', 'This is line C\n']

**# Write the strings in the list to text file**

with open('/Example2.txt', 'w') as writefile:
    for line in Lines:
        print(line)
        writefile.write(line)

EXPECTED RESULT:    
This is line A

This is line B

This is line C

We can verify the file is written by reading it and printing out the values:
**# Verify if writing to file is successfully executed**

with open('/Example2.txt', 'r') as testwritefile:
    print(testwritefile.read())

THIS SHOULD BE THE RESULT:    
This is line A
This is line B
This is line C

However, note that setting the mode to w overwrites all the existing data in the file.
with open('/Example2.txt', 'w') as writefile:
    writefile.write("Overwrite\n")
with open('/Example2.txt', 'r') as testwritefile:
    print(testwritefile.read())


THIS SHOULD BE THE RESULT:
 Overwrite


 
    
