# Library-management-system
# Library Management System using Python with book issue and return functionality

import datetime

library = {}

def add_book():
    name = input("Enter Book Name: ")
    if name in library:
        print("Book already exists")
    else:
        library[name] = {"issued": False, "student": "", "issue_date": None, "duration": 0}
        print("Book Added")

def view_books():
    if not library:
        print("No books available")
        return
    print("\nBooks:")
    for book, data in library.items():
        status = "Issued" if data["issued"] else "Available"
        print(f"{book} - {status}")

def issue_book():
    name = input("Enter Book Name: ")
    if name not in library:
        print("Book not found")
        return
    if library[name]["issued"]:
        print("Already issued")
        return
    student = input("Enter Student Name: ")
    duration = int(input("Enter Duration (days): "))
    library[name]["issued"] = True
    library[name]["student"] = student
    library[name]["issue_date"] = datetime.date.today()
    library[name]["duration"] = duration
    print("Book Issued")

def return_book():
    name = input("Enter Book Name: ")
    if name not in library:
        print("Book not found")
        return
    if not library[name]["issued"]:
        print("Book was not issued")
        return
    issue_date = library[name]["issue_date"]
    duration = library[name]["duration"]
    today = datetime.date.today()
    days_used = (today - issue_date).days
    fine = 0
    if days_used > duration:
        late_days = days_used - duration
        weeks = (late_days // 7) + 1
        for i in range(weeks):
            fine += (i + 1) * 10
    print(f"Days Used: {days_used}")
    print(f"Fine: ₹{fine}")
    library[name] = {"issued": False, "student": "", "issue_date": None, "duration": 0}
    print("Book Returned")

def menu():
    while True:
        print("\n1 Add Book")
        print("2 View Books")
        print("3 Issue Book")
        print("4 Return Book")
        print("5 Exit")
        choice = input("Enter choice: ")
        if choice == "1":
            add_book()
        elif choice == "2":
            view_books()
        elif choice == "3":
            issue_book()
        elif choice == "4":
            return_book()
        elif choice == "5":
            break
        else:
            print("Invalid choice")

menu()
