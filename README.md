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


# Appending Files 

We can write to files without losing any of the existing data as follows by setting the mode argument to append: a. you can append a new line as follows:

**# Write a new line to text file** 

with open('/Example2.txt', 'a') as testwritefile:
    testwritefile.write("This is line C\n")
    testwritefile.write("This is line D\n")
    testwritefile.write("This is line E\n")

You can verify the file has changed by running the following cell:

**# Verify if the new line is in the text file**

with open('/Example2.txt', 'r') as testwritefile:
    print(testwritefile.read())

THIS SHOULD BE THE RESULT:
    
Overwrite
This is line C
This is line D
This is line E

# Additional modes

It's fairly ineffecient to open the file in a or w and then reopening it in r to read any lines. Luckily we can access the file in the following modes:

**r+** : Reading and writing. Cannot truncate the file.
**w+** : Writing and reading. Truncates the file.
**a+** : Appending and Reading. Creates a new file, if none exists. You dont have to dwell on the specifics of each mode for this lab.

**Let's try out the a+ mode:**

with open('/Example2.txt', 'a+') as testwritefile:
    testwritefile.write("This is line E\n")
    print(testwritefile.read())

There were no errors but read() also did not output anything. This is because of our location in the file.

Most of the file methods we've looked at work in a certain location in the file. .write() writes at a certain location in the file. .read() reads at a certain location in the file and so on. You can think of this as moving your pointer around in the notepad to make changes at specific location.

Opening the file in w is akin to opening the .txt file, moving your cursor to the beginning of the text file, writing new text and deleting everything that follows. Whereas opening the file in a is similiar to opening the .txt file, moving your cursor to the very end and then adding the new pieces of text. It is often very useful to know where the 'cursor' is in a file and be able to control it. The following methods allow us to do precisely this -

**.tell()** - returns the current position in bytes
**.seek(offset,from)** - changes the position by 'offset' bytes with respect to 'from'. From can take the value of 0,1,2 corresponding to beginning, relative to current position and end

**Now lets revisit a+**


with open('/Example2.txt', 'a+') as testwritefile:
    print("Initial Location: {}".format(testwritefile.tell()))
    
    data = testwritefile.read()
    if (not data):  #empty strings return false in python
            print('Read nothing') 
    else: 
            print(testwritefile.read())
            
    testwritefile.seek(0,0) # move 0 bytes from beginning.
    
    print("\nNew Location : {}".format(testwritefile.tell()))
    data = testwritefile.read()
    if (not data): 
            print('Read nothing') 
    else: 
            print(data)
    
    print("Location after read: {}".format(testwritefile.tell()) )



THIS SHOUKD BE THE RESULT:
    
Initial Location: 70
Read nothing

New Location : 0
Overwrite
This is line C
This is line D
This is line E
This is line E

Location after read: 70


Finally, a note on the difference between w+ and r+. Both of these modes allow access to read and write methods, however, opening a file in w+ overwrites it and deletes all pre-existing data.

In the following code block, Run the code as it is first and then run it without the .truncate().


with open('/Example2.txt', 'r+') as testwritefile:
    testwritefile.seek(0,0) #write at beginning of file
    testwritefile.write("Line 1" + "\n")
    testwritefile.write("Line 2" + "\n")
    testwritefile.write("Line 3" + "\n")
    testwritefile.write("Line 4" + "\n")
    testwritefile.write("finished\n")
    testwritefile.seek(0,0)
    print(testwritefile.read()


THIS SHOULD BE THE RESULT:
    
Line 1
Line 2
Line 3
Line 4
finished
 D
This is line E
This is line E


To work with a file on existing data, use r+ and a+. While using r+, it can be useful to add a .truncate() method at the end of your data. This will reduce the file to your data and delete everything that follows.

with open('/Example2.txt', 'r+') as testwritefile:
    testwritefile.seek(0,0) #write at beginning of file
    testwritefile.write("Line 1" + "\n")
    testwritefile.write("Line 2" + "\n")
    testwritefile.write("Line 3" + "\n")
    testwritefile.write("Line 4" + "\n")
    testwritefile.write("finished\n")
    #Uncomment the line below
    testwritefile.truncate()
    testwritefile.seek(0,0)
    print(testwritefile.read())

THIS SHOULD BE THE RESULT:
    
Line 1
Line 2
Line 3
Line 4
finished


# Copy a File

Let's copy the file Example2.txt to the file Example3.txt:

**# Copy file to another**

with open('/Example2.txt','r') as readfile:
    with open('/Example3.txt','w') as writefile:
          for line in readfile:
                writefile.write(line)

We can read the file to see if everything works:

**# Verify if the copy is successfully executed**

with open('/Example3.txt','r') as testwritefile:
    print(testwritefile.read())


THIS SHOULD BE THE RESULT:
    
Line 1
Line 2
Line 3
Line 4
finished


