# Trishla-demo
<h1>Registration Form </h1>
#import tkinter
from tkinter import *
import mysql.connector
import tkinter.messagebox as m
#create a main window
r = Tk()

# creating customize window
r.geometry("500x500")

#create title
r.title("my Title")

# change bgcolor
r.configure(bg="black")

#connection with database
def createconn():
    return mysql.connector.connect(
        host = "localhost",
        database = "temp1",
        user = "root",
        password = "Enter your database password",
        port = 3306
    )

#insert data
def InsertData():
    r = ern.get()
    f = efn.get()
    l = eln.get()
    e = eem.get()

    if (r == "" or f == "" or l == "" or e == ""):
        m.showinfo("Insert Status", "All fields are Mandatory")
    else:
        try:
            conn = createconn()
            cursor = conn.cursor()
            args = (r,f,l,e)
            query = "insert into student(rollno,fname,lname,email) values(%s,%s,%s,%s)"
            cursor.execute(query,args)
            conn.commit()
            m.showinfo("Insert Status","Data Inserted")
            print("Data successfully inserted")
            conn.close()

        except Exception as ee:
            print("insert Exception : ",ee)

#create lable
rn = Label(r,text="RollNo")
rn.place(x=20,y=20)
#create text box
ern = Entry()                # Roll No
ern.place(x = 100, y= 20)

fn = Label(r,text="Firstname") # First Name
fn.place(x = 20, y = 60)
efn = Entry()
efn.place(x = 100, y= 60)

ln = Label(r,text ="Lastname")  # Last Name
ln.place(x = 20, y= 100)
eln = Entry()
eln.place(x =100 , y =100)

em = Label(r,text="Email")    # Email
em.place(x=20,y=140)
eem = Entry()
eem.place(x =100 , y = 140)

# create buttons
button1 = Button(r, text = "Insert", bg ="white", command=InsertData)
button1.place(x=20, y = 200) 

# mainloop method called
mainloop()
