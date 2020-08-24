# To Do List Script with Pickles and Error Handling
*AJehle, 8.24.2020*

## Introduction
The purpose of this document is to familiarize the reader with the concepts of pickling and exception handling in Python. This is done using the program from the Mod06 Assignment with variations made. The original program can be accessed here: https://github.com/anjehle/IntroToProg-Python-Mod06

## Pickling
Pickling is a way for python users to condense data using serialization during the reading and loading process. By unloading data through pickles the user is converting their file into a binary protocol using a byte stream. Inversely, when they unload data, or “unpickle”, they are converting that binary file into the traditional object hierarchy. This process is as simple as altering the way the read and write commands are written. Instead of simply using the read command, a special pickle.load([File to load]) command is used, as seen in Figure 1. Additionally, to write to a pickled file the pickle.dump([data to be written], [File]) command is used as seen in Figure 2. Apart from these changes, no other edits are necessary, making this a convenient and easily executable change to help with any basic file!
![Example of a Pickle](https://github.com/anjehle/ITFnd100-Mod07/blob/master/docs/images/pickle.jpg "Pickle")

### Application with To-Do List Program
Pickles were incorporated into the previous program from the Mod06 assignment. This was used to pickle and unpickle the to-do list via the code shown in Figure 1 and Figure 2.

##### Figure 1: Reading data from the to-do list using pickles
```
def read_data_from_file(file_name, list_of_rows):
    """ Reads data from a file into a list of dictionary rows
    :param file_name: (string) with name of file:
    :param list_of_rows: (list) you want filled with file data:
    :return: (list) of dictionary rows
    """
    list_of_rows.clear()  #clear current data
    try:
        objFile = open(file_name, 'rb')
        print('File found!')
        list_of_rows = pickle.load(objFile)
        objFile.close()
    except:
        print('No existing to-do list available')
    return list_of_rows, 'Success'

```
#### Figure 2: Unloading data from the to-do list using pickles
```
def write_data_to_file(file_name, list_of_rows):
    """ Writes data from list of dictionary rows to file
        :param file_name: (string) with name of file:
        :param list_of_rows: (list) you want added to text file:
        :return: (list) of dictionary rows
    """
    objFile = open(file_name, 'wb')
    pickle.dump(list_of_rows, objFile)
    objFile.close()
    return list_of_rows, 'Success'
```

### Execution in PyCharm
The program with the code modifications shown above was executed in PyCharm. The program was successfully pickled and unpickled, as shown in Figure 3.

#### Figure 3: Execution of pickled file in PyCharm
![Figure 3: Execution of pickled file in PyCharm](https://github.com/anjehle/ITFnd100-Mod07/blob/master/docs/images/PicklesPC1.png "Pickle from PyCharm")
![ ](https://github.com/anjehle/ITFnd100-Mod07/blob/master/docs/images/PicklesPC2.png "Pickle")

### Execution in Terminal
Immediately after execution in PyCharm, the program was ran via the terminal. As you can see in Figure 4, the changes made in the PyCharm execution were successfully saved and unpickled. 
#### Figure 4: Execution of pickled file in the terminal
![ ](https://github.com/anjehle/ITFnd100-Mod07/blob/master/docs/images/PicklesT.png "Pickle")

## Exception and Error Handling
Effectively using exceptions and error handling in python can be a powerful way to make your code more robust. Although this document will only cover a basic example of this, they are very modifiable. The programmer is able to alter these exceptions to encapsulate a vast range of errors that would normally stall out a program. These can be user defined (using a similar method as defining a class) or more traditional try/except cases. In this example, a try: was added to the program as seen in Figure 5. This alteration checks to see if a file exists before it is opened. If it does not exist the except: line is ran. The user is notified whichever case is ran by outputting either “File found!” or “No existing to-do list available”. 

#### Figure 5: A file load with a try: command in it
```
def read_data_from_file(file_name, list_of_rows):
    """ Reads data from a file into a list of dictionary rows
    :param file_name: (string) with name of file:
    :param list_of_rows: (list) you want filled with file data:
    :return: (list) of dictionary rows
    """
    list_of_rows.clear()  #clear current data
    try:
        objFile = open(file_name, 'rb')
        print('File found!')
        list_of_rows = pickle.load(objFile)
        objFile.close()
    except:
        print('No existing to-do list available')
    return list_of_rows, 'Success'
```

### Execution in PyCharm
The program with the code modifications shown above was executed in PyCharm. The program successfully identified that no file was found. When a task was saved, it successfully recognized the new file.

#### Figure 6: Execution of try/except program in PyCharm
![ ](https://github.com/anjehle/ITFnd100-Mod07/blob/master/docs/images/TryPC1.png "Try")
![ ](https://github.com/anjehle/ITFnd100-Mod07/blob/master/docs/images/TryPC2.png "Try")

### Execution in Terminal
The same example as above was ran in the terminal next after deleting the .dat file. The program successfully identified that no file was found as seen in Figure 7. When a task was saved, it successfully recognized the new file. All of these resources were selected because they have a basic explanation but wide range of what they cover. The examples are clear and were found to be completely accurate and executable. In general, they provide a very insightful introduction but shouldn’t be referenced for advanced instruction on the concepts.

#### Figure 7: Execution of try/except program in the terminal
![ ](https://github.com/anjehle/ITFnd100-Mod07/blob/master/docs/images/TryT1.png "Try")
![ ](https://github.com/anjehle/ITFnd100-Mod07/blob/master/docs/images/TryT2.png "Try")

## Summary
Although these were both very basic examples, there is much more to learn about pickles and error handling in python. The websites cited in the ‘Resources’ section below expand on these concept and provide much more information and examples of various use cases.

## Appendix I: Full Python Script
```
# ---------------------------------------------------------------------------- #
# Title: Assignment 07
# Description: Working with functions in a class,
#              When the program starts, load each "row" of data
#              in "ToDoToDoList.txt" into a python Dictionary.
#              Add the each dictionary "row" to a python list "table"
# ChangeLog (Who,When,What):
# RRoot,1.1.2030,Created started script
# RRoot,1.1.2030,Added code to complete assignment 5
# AJehle,8.11.2020,Modified code to complete assignment 6
# AJehle,8.23.2020,Modified code to complete assignment 7
# ---------------------------------------------------------------------------- #

# Data ---------------------------------------------------------------------- #
import pickle
# Declare variables and constants
strFileName = "ToDoFile.dat"  # The name of the data file
objFile = None  # An object that represents a file
dicRow = {}  # A row of data separated into elements of a dictionary {Task,Priority}
lstTable = []  # A list that acts as a 'table' of rows
strChoice = ""  # Captures the user option selection
strTask = ""  # Captures the user task data
strPriority = ""  # Captures the user priority data
strStatus = ""  # Captures the status of an processing functions


# Processing  --------------------------------------------------------------- #
class Processor:
    """  Performs Processing tasks """

    @staticmethod
    def read_data_from_file(file_name, list_of_rows):
        """ Reads data from a file into a list of dictionary rows
        :param file_name: (string) with name of file:
        :param list_of_rows: (list) you want filled with file data:
        :return: (list) of dictionary rows
        """
        list_of_rows.clear()  #clear current data
        try:
            objFile = open(file_name, 'rb')
            print('File found!')
            list_of_rows = pickle.load(objFile)
            objFile.close()
        except:
            print('No existing to-do list available')
        return list_of_rows, 'Success'

    @staticmethod
    def add_data_to_list(task, priority, list_of_rows):
        """ Adds task from input to the list of dictionary rows
                :param task: (string) with name of task:
                :param priority: (string) with priority of task:
                :param list_of_rows: (list) you want filled with additional task:
                :return: (list) of dictionary rows
        """
        dicRow = {"Task": task.strip(), "Priority": priority.strip()}
        list_of_rows.append(dicRow)
        return list_of_rows, 'Success'

    @staticmethod
    def remove_data_from_list(task, list_of_rows):
        """ Removes task from input from the list of dictionary rows
            :param task: (string) with name of task:
            :param list_of_rows: (list) you want task removed from:
            :return: (list) of dictionary rows
        """
        boolfound = False
        for dicRow in list_of_rows:
            if dicRow["Task"] == task:
                list_of_rows.remove(dicRow)
                boolfound = True
        if boolfound == False:
            print('Task not found')
        return list_of_rows, 'Success'

    @staticmethod
    def write_data_to_file(file_name, list_of_rows):
        """ Writes data from list of dictionary rows to file
            :param file_name: (string) with name of file:
            :param list_of_rows: (list) you want added to text file:
            :return: (list) of dictionary rows
        """
        objFile = open(file_name, 'wb')
        pickle.dump(list_of_rows, objFile)
        objFile.close()
        return list_of_rows, 'Success'


# Presentation (Input/Output)  -------------------------------------------- #
class IO:
    """ Performs Input and Output tasks """

    @staticmethod
    def print_menu_Tasks():
        """  Display a menu of choices to the user
        :return: nothing
        """
        print('''
        Menu of Options
        1) Add a new Task
        2) Remove an existing Task
        3) Save Data to File        
        4) Reload Data from File
        5) Exit Program
        ''')
        print()  # Add an extra line for looks

    @staticmethod
    def input_menu_choice():
        """ Gets the menu choice from a user
        :return: string
        """
        choice = str(input("Which option would you like to perform? [1 to 5] - ")).strip()
        print()  # Add an extra line for looks
        return choice

    @staticmethod
    def print_current_Tasks_in_list(list_of_rows):
        """ Shows the current Tasks in the list of dictionaries rows
        :param list_of_rows: (list) of rows you want to display
        :return: nothing
        """
        print("******* The current Tasks ToDo are: *******")
        for dicRow in list_of_rows:
            print(dicRow["Task"] + " (" + dicRow["Priority"] + ")")
        print("*******************************************")
        print()  # Add an extra line for looks

    @staticmethod
    def input_yes_no_choice(message):
        """ Gets a yes or no choice from the user
        :return: string
        """
        return str(input(message)).strip().lower()

    @staticmethod
    def input_press_to_continue(optional_message=''):
        """ Pause program and show a message before continuing

        :param optional_message:  An optional message you want to display
        :return: nothing
        """
        print(optional_message)
        input('Press the [Enter] key to continue.')

    @staticmethod
    def input_new_task_and_priority():
        pass  # TODO: Add Code Here!
        task = str(input("Which task would you like to add? ")).strip()
        priority = str(input('What priority should ' + task + ' have?: ')).strip()
        return task, priority

    @staticmethod
    def input_task_to_remove():
        pass  # TODO: Add Code Here!
        task = str(input("Which task would you like to remove? ")).strip()
        return task


# Main Body of Script  ------------------------------------------------------ #

# Step 1 - When the program starts, Load data from ToDoFile.txt.
lstTable, success = Processor.read_data_from_file(strFileName, lstTable)  # read file data

# Step 2 - Display a menu of choices to the user
while (True):
    # Step 3 Show current data
    IO.print_current_Tasks_in_list(lstTable)  # Show current data in the list/table
    IO.print_menu_Tasks()  # Shows menu
    strChoice = IO.input_menu_choice()  # Get menu option

    # Step 4 - Process user's menu choice
    if strChoice.strip() == '1':  # Add a new Task
        task, priority = IO.input_new_task_and_priority()
        lstTable, strStatus = Processor.add_data_to_list(task, priority, lstTable)
        IO.input_press_to_continue(strStatus)
        continue  # to show the menu

    elif strChoice == '2':  # Remove an existing Task
        task = IO.input_task_to_remove()
        lstTable, strStatus = Processor.remove_data_from_list(task, lstTable)
        IO.input_press_to_continue(strStatus)
        continue  # to show the menu

    elif strChoice == '3':  # Save Data to File
        strChoice = IO.input_yes_no_choice("Save this data to file? (y/n) - ")
        if strChoice.lower() == "y":
            lstTable, strStatus = Processor.write_data_to_file(strFileName, lstTable)
            IO.input_press_to_continue(strStatus)
        else:
            IO.input_press_to_continue("Save Cancelled!")
        continue  # to show the menu

    elif strChoice == '4':  # Reload Data from File
        print("Warning: Unsaved Data Will Be Lost!")
        strChoice = IO.input_yes_no_choice("Are you sure you want to reload data from file? (y/n) -  ")
        if strChoice.lower() == 'y':
            lstTable, strStatus = Processor.read_data_from_file(strFileName, lstTable)
            IO.input_press_to_continue(strStatus)
        else:
            IO.input_press_to_continue("File Reload  Cancelled!")
        continue  # to show the menu

    elif strChoice == '5':  # Exit Program
        print("Goodbye!")
        break  # and Exit
    else:
        print("Valid option not selected.")
        continue 
```

## Resources
P. (2017, July 20). How to Pickle: A Beginner's Guide to Pickling and Unpickling. Retrieved August 24, 2020, from https://www.pythoncentral.io/how-to-pickle-unpickle-tutorial/

P. (2020). 8. Errors and Exceptions. Retrieved August 24, 2020, from https://docs.python.org/3/tutorial/errors.html

P. (n.d.). Python Exception Handling Using try, except and finally statement. Retrieved August 24, 2020, from https://www.programiz.com/python-programming/exception-handling

P. (n.d.). Python Pickle Module for saving Objects by serialization. Retrieved August 24, 2020, from https://pythonprogramming.net/python-pickle-module-save-objects-serialization/

Z0o0p, G., Z0o0p, & Geeks for Geeks. (2020, July 26). Read List of Dictionaries from File in Python. Retrieved August 24, 2020, from https://www.geeksforgeeks.org/read-list-of-dictionaries-from-file-in-python/

