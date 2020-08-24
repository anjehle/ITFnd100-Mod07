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

