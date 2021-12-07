from tkinter import *
from tkinter import messagebox
import random
import pyperclip
import json
#-----------------------------SEARCH PASSWORD------------------------------------#
def search_password():
    website = website_entry.get()
    try:
        with open("data.json") as data_file:
            data = json.load(data_file)
    except FileNotFoundError:
        messagebox.showinfo(title="Error",message="No Data Found")
    else:
        if website in data:
            email = data[website]["email"]
            password = data[website]["password"]
            messagebox.showinfo(title=website,message=f'Email: {email}\nPassword: {password}')
        else:
            messagebox.showinfo(title="Error",message=f"No details for {website} exists.")
# ---------------------------- PASSWORD GENERATOR ------------------------------- #
def passwword_generator():
    letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
    numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
    symbols = ['!', '#', '$', '%', '&', '(', ')', '*', '+']

    nr_letters = random.randint(8, 10)
    nr_symbols = random.randint(2, 4)
    nr_numbers = random.randint(2, 4)

    password_list = []

    for char in range(nr_letters):
      password_list.append(random.choice(letters))

    for char in range(nr_symbols):
      password_list += random.choice(symbols)

    for char in range(nr_numbers):
      password_list += random.choice(numbers)

    random.shuffle(password_list)

    password = "".join(password_list)

    password_entry.insert(0,password)
    pyperclip.copy(password)
# ---------------------------- SAVE PASSWORD ------------------------------- #
def save():

    website=website_entry.get()
    email=email_entry.get()
    password=password_entry.get()
    new_data = {
        website :{
            "email":email,
            "password":password,
        }
    }
    if (len(website) == 0)or(len(email) == 0)or(len(password) == 0) :
        oops = messagebox.showinfo(title="OOPS",message="Don't leave any field empty")
        email_entry.delete(0, END)
        website_entry.delete(0, END)
        password_entry.delete(0, END)
    else:
        is_ok = messagebox.askokcancel(title="Website",message=f'These are the details you have'
                                                               f' entered: \nEmail: {email} \nPassword: '
                                                               f'{password}\nIs it ok to save?')
        if is_ok:
            try:
                with open("data.json","r") as data_file:
                    data = json.load(data_file)

            except FileNotFoundError:
                with open("data.json", "w") as data_file:
                     json.dump(data,data_file,indent=4)
            else:
                data.update(new_data)
                with open("data.json", "w") as data_file:
                    json.dump(data,data_file,indent=4)
            finally:
                email_entry.delete(0,END)
                website_entry.delete(0,END)
                password_entry.delete(0,END)
        else:
            email_entry.delete(0, END)
            website_entry.delete(0, END)
            password_entry.delete(0, END)



# ---------------------------- UI SETUP ------------------------------- #
windows = Tk()
windows.title("Password Manager")
windows.config(padx=50,pady=50)
canvas =Canvas(width=200,height=200,highlightthickness=0)
logo_img = PhotoImage(file="logo.png")
canvas.create_image(100,100,image=logo_img)
canvas.grid(row=0,column=1)
label_1 = Label(text="Website:" )
label_1.grid(column=0, row=1)
label_2 = Label(text="Email/Username:")
label_2.grid(column=0, row=2)
label_3 = Label(text="Password:")
label_3.grid(column=0, row=3)
website_entry=Entry(width=60)
website_entry.focus()
website_entry.grid(row=1,column=1,columnspan=2)
email_entry=Entry(width=60)
email_entry.grid(row=2,column=1,columnspan=2)
password_entry=Entry(width=60)
password_entry.grid(row=3,column=1,columnspan=2)
generate_button = Button(text="Generate Password",width=14,command=passwword_generator)
generate_button.grid(column=2,row=3)
add_button = Button(text="Add",width=35,command=save)
add_button.grid(column=1,row=4)
search_button = Button(text="Search",width=14,command=search_password)
search_button.grid(column=2,row=1)
windows.mainloop()
