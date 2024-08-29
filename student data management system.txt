import mysql.connector

def connect_to_db():

    try:
        connection = mysql.connector.connect(
            host = 'localhost',
            user = 'root',
            password = 'password',
            database = 'project')
        return connection

    except mysql.connector.Error as err:
        print(f'Error: {err}')
        return None



def add_std(connection):

    std_name = input("Enter Student Name: ")
    age = input("Enter the Age: ")
    dob = input("Enter DOB(YYYY-MM-DD): ")
    roll_number = input("Enter Roll number: ")
    department = input("Enter the department: ")
    email = input("Enter e-mail: ")
    mob_num = input("Enter Mobile number: ")
    

    cursor = connection.cursor()
    sql = "INSERT INTO students VALUES(%s,%s,%s,%s,%s,%s,%s)"
    values = (std_name,age,dob,roll_number,department,email,mob_num)

    try:
        cursor.execute(sql,values)
        connection.commit()
        print("Student data added successfully!")
        return None
    except mysql.connector.Error as err:
        print(f"Error: {err}")
        return None

def update_std(connection):

    std_name = input("Enter the name of the whome to be updated: ")
    cursor = connection.cursor()
    sql = "SELECT * FROM students WHERE std_name = %s"
    cursor.execute(sql,(std_name,))
    result = cursor.fetchone()

    if result:
        print(f"Current Details: Name: {result[0]}\n Age: {result[1]}\n DOB: {result[2]}\n Roll Number: {result[3]}\n Department: {result[4]}\n Email: {result[5]}\n Mobile number: {result[6]}")
        
        print("\nWhat would you like to update?")
        print("1: Age")
        print("2: DOB")
        print("3: Roll Number")
        print("4: Department")
        print("5: Email ID")
        print("6: Mobile number")
        print("7: All Fields")

        choice = int(input("Enter your choice: "))
        

        if choice == 1:
            age = input("Enter New Age: ")
            sql_update = "UPDATE students SET age = %s WHERE std_name = %s"
            values = (age, std_name)

        elif choice == 2:
            dob = input("Enter the New DOB: ")
            sql_update = "UPDATE students SET dob = %s WHERE std_name = %s"
            values = (dob, std_name)
            
        elif choice == 4:
            department = input("Enter New Department: ")
            sql_update = "UPDATE students SET department = %s WHERE std_name = %s"
            values = (department, std_name)

        elif choice == 3:
            roll_number = input("Enter New Roll Number: ")
            sql_update = "UPDATE students SET roll_number = %s WHERE std_name = %s"
            values = (roll_number, std_name)

        elif choice == 5:
            email = input("Enter New Email ID: ")
            sql_update = "UPDATE students SET email = %s WHERE std_name = %s"
            values = (email, std_name)

        elif choice == 6:
            mob_num = input("Enter New Mobile number: ")
            sql_update = "UPDATE students SET mob_num = %s WHERE std_name = %s"
            values = (mob_num, std_name)

        elif choice == 7:
            age = input("Enter New Age: ")
            dob = input("Enter New DOB: ")
            department = input("Enter New Department: ")
            roll_number = input("Enter New Roll Number: ")
            email = input("Enter New Email ID: ")
            mob_num = input("Enter New Mobile number: ")
            sql_update = """
            UPDATE students 
            SET age = %s, dob = %s, department = %s, roll_number = %s, email = %s, mob_num = %s 
            WHERE std_name = %s
            """
            values = (age, dob, department, roll_number, email, mob_num, std_name)
        
        else:
            print("Invalid choice!")
            return
        
        try:
            cursor.execute(sql_update, values)
            connection.commit()
            print("Student details updated successfully!")
        except mysql.connector.Error as err:
            print(f"Error: {err}")
    else:
        print("Student not found!")

def delete_std(connection):
    std_name = input("Enter Student name: ")
    
    cursor = connection.cursor()
    sql_delete = "DELETE FROM students WHERE std_name = %s"
    
    try:
        cursor.execute(sql_delete, (std_name,))
        connection.commit()
        if cursor.rowcount > 0:
            print("Student deleted successfully!")
            print()
        else:
            print("Student not found!")
            print()
    except mysql.connector.Error as err:
        print(f"Error: {err}")


def view_std(connection):
    
    cursor = connection.cursor()
    sql = "SELECT * FROM students"
    
    cursor.execute(sql)
    results = cursor.fetchall()
    
    if results:
        print("\nCurrent Students List:")
        for row in results:
            print(f" Name: {row[0]}\n Age: {row[1]}\n DOB: {row[2]}\n Roll Number: {row[3]}\n Department: {row[4]}\n Email: {row[5]}\n Mobile Number: {row[6]}")
            print()
    else:
        print("No students found.")


def count_std(connection):

    cursor = connection.cursor()
    sql = "SELECT COUNT(*) FROM students"
    
    cursor.execute(sql)
    result = cursor.fetchone()
    
    if result:
        print(f"\nTotal Number of Students: {result[0]}")
        print()
    else:
        print("Failed to retrieve student count.")

def view_std_data(connection):
    connection = connect_to_db()
    cursor = connection.cursor()
    std_name = input("Enter your name: ")
    sql = "SELECT * FROM students WHERE std_name = %s"
    values = (std_name,)
    cursor.execute(sql,values)
    result = cursor.fetchall()

    try:
        if result:
            for row in result: 
                print(f"\nYOUR DETAILS:\n Name: {row[0]}\n Age: {row[1]}\n DOB: {row[2]}\n Roll Number: {row[3]}\n Department: {row[4]}\n Email: {row[5]}\n Mobile Number: {row[6]}")
                print()
                return
        else:
            print("Student not found!")
            return
    except mysql.connector.Error as err:
        print(f"Error: {err}")
    


def student():
    
    connection = connect_to_db()

    if connection:
        print('Connected to database successfully!')
        print()
    else:
        print('Database connection failed!')
        return None

    while True:

        print('1.View my details')
        print('2.Exit system')
        print('Enter a choice: ',end="")
        choice = int(input())

        if choice == 1:
            view_std_data(connection)
            
        elif choice == 2:
            return None
        else:
            print('CAUTION: Invalid choice')
            print()

            
        
def format_std(connection):

    cursor = connection.cursor()
    sql = "TRUNCATE TABLE students"

    try:
        cursor.execute(sql)
        connection.commit()
        print("Data Formated successfully!")
        return
    except mysql.connector.Error as err:
        print(f"Error: {err}")
        return None
    

def admin():

    connection = connect_to_db()

    if connection:
        print('Connected to database successfully!')
        print()
    else:
        print('Database connection failed!')
        return None

    while True:

        print('1.Add student data')
        print('2.Update student data')
        print('3.Delete student data')
        print('4.View student data')
        print('5.Total number of students')
        print('6.Format students data')
        print('7.Exit system')
        print()
        print('Enter your choice: ',end="")
        choice = int(input())

        if choice == 1:
            add_std(connection)
        elif choice == 2:
            update_std(connection)
        elif choice == 3:
            delete_std(connection)
        elif choice == 4:
            view_std(connection)
        elif choice == 5:
            count_std(connection)
        elif choice == 6:
            format_std(connection)
        elif choice == 7:
            return None
        else:
            print('CAUTION: Enter a valid choice')
            print()


def password():
    count = 0
    while count<3:
        count+=1
        print('Enter Password: ',end="")
        password = input()
        if password == 'password': #predefined
            admin()
            break
        else:
            if count < 3:
                print('CAUTION: Enter the correct password')
                print()
            else:
                print('Limit exceeded')
                return False
        

def login():
    count = 0
    while count<3:
        count+=1
        print('Enter Admin Name: ',end="")
        admin_name = input()
        if admin_name == 'admin': #predefined
            if password():
                break
            else:
                return None
        else:
            if count<3:
                print('CAUTION: Incorrect Admin Name')
                print()
            else:
                print('Limit exceeded')
                return None



def main():

    print('     STUDENT MANAGEMENT SYSTEM      ')
    print('------------------------------------')

    print('1.Admin')
    print('2.Student')
    
    print('Enter your choice: ',end="")
    choice = int(input())
    if choice == 1:
        login()
    elif choice == 2:
        student()
    else:
        print('CAUTION: Enter a valid choice')
        print()
        main()
    
        

if __name__ == '__main__':
    main()
