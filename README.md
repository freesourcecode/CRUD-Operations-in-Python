# CRUD Operations in Python With Source Code

The **CRUD Operations in Python** is written in Python programming language and MySQL database, in this article I will teach you how to create a Python crud operation with mysql.

The abbreviation **CRUD** expands to **Create**, **Read**, **Update**, and **Delete**. These four are fundamental operations in a database.

A **CRUD application in Python** is designed in a Graphical User Interface(GUI) using crud python tkinter, it also includes a downloadable python crud operation.

## CRUD in Python: Four Fundamental Operations


* CREATE – This refers to the insertion of new data into the table. Data is inserted in the form of a tuple.

The number of attributes in the tuple must be equal to that defined in the relation schema while creating the table.

* READ – This refers to reading data from a database. A read statement has three clauses:

  * SELECT: Takes as the predicate the attributes to be queried, use * for all attributes.
  * FROM: Takes as the predicate a relation.
  * WHERE: Takes as the predicate a condition, this is not compulsory.

* UPDATE – This refers to the updating of tuple values already present in the table.
* DELETE – This refers to the deletion of the tuple present in the table.
* Before we start to perform this Python CRUD Operation, be sure that you have Pycharm IDE and XAMPP installed on your computer.

By the way, if you are new to Python programming and don’t know what Python IDE to use, I have here a list of the **[Best Python IDE for Windows, Linux, and Mac OS](https://itsourcecode.com/blogs/best-python-ide-for-windows-2021/)** that will suit you.

## How to create a CRUD Operations in Python?

1. **Create a project name**.

First, when you finished installing the Pycharm IDE on your computer, open it and then create a “project name” After creating a project name click the “create” button.

2. **Create a python file**.

Second, after creating a project name, “right-click” your project name and then click “new.” After that click the “python file”.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/9569f923-6390-4e31-8e0d-ed573312ae0f" />

3. **Name your python file**.

Third, after creating a Python file, Name your Python file after that click “enter“.

4. **Open the XAMPP**.

Fourth when you are done creating a project name and python file in PyCharm IDE, open the XAMPP and click the “start” button of “Apache” and “MySQL.”

<img width="670" height="435" alt="image" src="https://github.com/user-attachments/assets/04003b60-53bd-4389-a42e-570735eee8b6" />

5. **Open any browser**.

Fifth open any browser and type in the URL: localhost/phpMyadmin.

6. **Create a database name**.

Sixth click “new” and name your database after that click the “create” button.

7. **Create a database table**.

After creating a database name, create a table name and then select how many “rows” you want to create in your database table after that click the “GO” button.

8. **Add entity and attributes**.

After creating the database table, add the entity and attributes in your database table and set the Stud_ID into a primary key and auto-incremented.

9. **The actual code on how to create CRUD Operations**.

This step gives the code below on how to create CRUD Operations using Python and connect to MySQL as a backend, you are free to copy this code and explore coding in your project.

## Code Explanations

1. **Create a Connection**

The code given below is the connection under Python and MySQL.

```
import mysql.connector
from mysql.connector import Error
 try:
                        conn = mysql.connector.connect(host='localhost',
                                                       database='CRUD',
                                                       user='root',
                                                       password='')
                        mycursor = conn.cursor()
```

In this module which is the connection of the system from a Python connect into MySQL database to perform adding, updating, deleting, and retrieving data.

2. **Main Module**

The code given below is the main module of the project.

```
from tkinter import *
from tkinter import messagebox
import os
import sys
from tkinter import ttk

import mysql.connector
from mysql.connector import Error

py=sys.executable

#creating window
class MainWin(Tk):
    def __init__(self):
        super().__init__()
        self.configure(bg='gray')
        self.canvas = Canvas(width=1366, height=768, bg='gray')
        self.canvas.pack()
        self.maxsize(1320, 768)
        self.minsize(1320,768)
        self.state('zoomed')
        self.title('CRUD Operation In Python')
        self.a = StringVar()
        self.b = StringVar()
        self.mymenu = Menu(self)
#calling scripts

        def ib():
            os.system('%s %s' % (py, 'Update.py'))

        def ret():
            os.system('%s %s' % (py, 'Delete.py'))

        def sea():
            os.system('%s %s' % (py,'Add.py'))


#creating table

        self.listTree = ttk.Treeview(self,height=14,columns=('First Name','Last Name','Gender','Address','Contact Number','Course'))
        self.vsb = ttk.Scrollbar(self,orient="vertical",command=self.listTree.yview)
        self.hsb = ttk.Scrollbar(self,orient="horizontal",command=self.listTree.xview)
        self.listTree.configure(yscrollcommand=self.vsb.set,xscrollcommand=self.hsb.set)
        self.listTree.heading("#0", text='ID')
        self.listTree.column("#0", width=50,minwidth=50,anchor='center')
        self.listTree.heading("First Name", text='First Name')
        self.listTree.column("First Name", width=200, minwidth=200,anchor='center')
        self.listTree.heading("Last Name", text='Last Name')
        self.listTree.column("Last Name", width=200, minwidth=200,anchor='center')
        self.listTree.heading("Gender", text='Gender')
        self.listTree.column("Gender", width=125, minwidth=125,anchor='center')
        self.listTree.heading("Address", text='Address')
        self.listTree.column("Address", width=125, minwidth=125, anchor='center')
        self.listTree.heading("Contact Number", text='Contact Number')
        self.listTree.column("Contact Number", width=125, minwidth=125, anchor='center')
        self.listTree.heading("Course", text='Course')
        self.listTree.column("Course", width=125, minwidth=125, anchor='center')
        self.listTree.place(x=200,y=360)
        self.vsb.place(x=1150,y=361,height=287)
        self.hsb.place(x=200,y=650,width=966)
        ttk.Style().configure("Treeview",font=('Times new Roman',15))


        def ser():
             try:
                conn = mysql.connector.connect(host='localhost',
                                         database='crud',
                                         user='root',
                                         password='')
                cursor = conn.cursor()

                cursor.execute("Select * from tbl_student")
                pc = cursor.fetchall()
                if pc:
                    self.listTree.delete(*self.listTree.get_children())
                    for row in pc:
                        self.listTree.insert("",'end',text=row[0] ,values = (row[1],row[2],row[3],row[4],row[5],row[6]))
                else:
                    messagebox.showinfo("Error", "No Student!")
             except Error:
                #print(Error)
              messagebox.showerror("Error","Something Goes Wrong")

        def check():

                    #label and input box
                    self.label3 = Label(self, text='CRUD Operation In Python',fg='black',bg="gray" ,font=('Courier new', 30, 'bold'))
                    self.label3.place(x=350, y=22)
                    self.label6 = Label(self, text="STUDENT INFORMATION DETAILS",bg="gray",  font=('Courier new', 15, 'underline', 'bold'))
                    self.label6.place(x=560, y=300)
                    self.button = Button(self, text='View Student(s)', width=25,bg='blue', font=('Courier new', 10), command=ser).place(x=240,y=250)
                    self.button = Button(self, text='Add Student', width=25,bg='green', font=('Courier new', 10), command=sea).place(x=520,y=250)
                    self.brt = Button(self, text="Update Student", width=15,bg='orange', font=('Courier new', 10), command=ib).place(x=800, y=250)
                    self.brt = Button(self, text="Delete Student", width=15,bg='red', font=('Courier new', 10), command=ret).place(x=1000, y=250)

        check()

MainWin().mainloop()
```
In this module which is the main module of the system, the CRUD function is connected to this module.

### Output:

<img width="1024" height="564" alt="image" src="https://github.com/user-attachments/assets/cb1e0e99-5d40-4a44-9a73-cfea6c15e0f3" />



3. **Add Data**

The code given below is for adding data.

```
from tkinter import *
from tkinter import messagebox
from tkinter import filedialog
import os
import sys
import mysql.connector
from mysql.connector import Error
py = sys.executable

#creating window
class Add(Tk):
    def __init__(self):
        super().__init__()
        self.maxsize(500,417)
        self.minsize(500,417)
        self.title('Add Student')
        self.canvas = Canvas(width=500, height=417, bg='gray')
        self.canvas.pack()
        fname = StringVar()
        lname = StringVar()
        cn = StringVar()
        gender = StringVar()
        add = StringVar()
        c = StringVar()
#verifying input
        def asi():
                try:
                    self.conn = mysql.connector.connect(host='localhost',
                                                        database='crud',
                                                        user='root',
                                                        password='')
                    self.myCursor = self.conn.cursor()
                    first = fname.get()
                    last = lname.get()
                    contact = cn.get()
                    gend = gender.get()
                    address = add.get()
                    course = c.get()
                    self.myCursor.execute("Insert into tbl_student(FirstName,LastName,Gender,Address,ContactNumber,Course) values (%s,%s,%s,%s,%s,%s)",[first,last,gend,address,contact,course])
                    self.conn.commit()
                    messagebox.showinfo("Done","Student Inserted Successfully")
                    ask = messagebox.askyesno("Confirm","Do you want to add another student?")
                    if ask:
                     self.destroy()
                     os.system('%s %s' % (py, 'Add.py'))
                    else:
                     self.destroy()
                     self.myCursor.close()
                     self.conn.close()
                except Error:
                    messagebox.showerror("Error","Something goes wrong")

        # label and input box
        Label(self, text='Student Details',bg='gray', fg='white', font=('Courier new', 25, 'bold')).pack()
        Label(self, text='First Name:', bg='gray', font=('Courier new', 10, 'bold')).place(x=70, y=102)
        Entry(self, textvariable=fname, width=30).place(x=200, y=104)
        Label(self, text='Last Name:', bg='gray', font=('Courier new', 10, 'bold')).place(x=70, y=150)
        Entry(self, textvariable=lname, width=30).place(x=200, y=152)
        Label(self, text='Gender:', bg='gray', font=('Courier new', 10, 'bold')).place(x=70, y=200)
        Entry(self, textvariable=gender, width=30).place(x=200, y=202)
        Label(self, text='Address:', bg='gray', font=('Courier new', 10, 'bold')).place(x=70, y=250)
        Entry(self, textvariable=add, width=30).place(x=200, y=250)
        Label(self, text='Contact Number:', bg='gray', font=('Courier new', 10, 'bold')).place(x=70, y=300)
        Entry(self, textvariable=cn, width=30).place(x=200, y=300)
        Label(self, text='Course:', bg='gray', font=('Courier new', 10, 'bold')).place(x=70, y=350)
        Entry(self, textvariable=c, width=30).place(x=200, y=350)
        Button(self, text="Save", bg='blue', width=15, command=asi).place(x=230, y=380)

Add().mainloop()
```

In this module which is performing the create function and save into MySQL database.


### Output:

<img width="500" height="446" alt="image" src="https://github.com/user-attachments/assets/ba3d88de-dca6-4929-9db2-f53ec5dfb0d2" />

### 📌 Here's the full documentation for the [CRUD Operations in Python](https://itsourcecode.com/free-projects/python-projects/crud-operations-in-python-with-source-code/)

### Related Articles
* **[CRUD Operations in PHP](https://itsourcecode.com/free-projects/php-project/crud-operations-in-php-with-source-code-complete-guide/)**
* **[CRUD in PHP and MySQ](https://itsourcecode.com/free-projects/php-project/crud-operations-in-php-and-mysql/)L**
* **[CRUD Operations in JavaScript](https://itsourcecode.com/free-projects/jsprojects/crud-operations-in-javascript-with-source-code/)**
* **[Crud Operation in Nodejs and MySQL](https://itsourcecode.com/nodejs-projects/crud-operation-in-nodejs-and-mysql-with-source-code/)**
* **[CRUD Operation in ASP NET MVC](https://itsourcecode.com/free-projects/asp/crud-operation-in-asp-net-mvc-with-source-code/)**
* **[CRUD Operation in React JS](https://itsourcecode.com/free-projects/reactjs/crud-operations-in-react-js-with-source-code/)**
* **[Django CRUD App](https://itsourcecode.com/free-projects/python-projects/crud-app-in-django-with-source-code/)**





