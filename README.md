Student Records Management System
---------------------------------
This project is a command-line based system designed to manage student records, implementing full CRUD (Create, Read, Update, Delete) operations using Python and MySQL. The goal of this project was to strengthen my understanding of integrating SQL databases with Python, as well as to practice effective data management techniques.

Feature
-------
Create: Add new student records to the database.
Read: Retrieve and display student records.
Update: Modify existing student records.
Delete: Remove student records from the database.

Prerequisites
-
Before running the application, ensure you have the following installed:
1.Python 3.x
2.MySQL Server

Installation
-
Clone this repository:
git clone https://github.com/yourusername/student-records-management.git
cd student-records-management

Install the required Python packages:
pip install -r requirements.txt

Set up the MySQL database:
Open your MySQL client and create a new database:
CREATE DATABASE student_records;

Use the student_records database:
USE student_records;

Create the necessary tables using the provided schema.sql file:

mysql -u your_username -p student_records < schema.sql

Update the config.py file with your MySQL credentials:

DB_HOST = 'localhost'
DB_USER = 'your_username'
DB_PASSWORD = 'your_password'
DB_NAME = 'student_records'

Usage
To start managing student records, run the main.py script:

bash
Copy code
python main.py
You will be prompted with various options to create, read, update, or delete student records.

Example Commands

Add a new student:
1. Enter Student Name: John Doe
2. Enter Student Age: 21
3. Enter Student Major: Computer Science

View all students:
1. View All Students

Update a student’s information:
1. Enter Student ID to update: 3
2. Enter new Student Name: John Smith

Delete a student record:
1. Enter Student ID to delete: 3

Contributing
-
Contributions are welcome! Please fork this repository, make your changes, and submit a pull request.

License
-
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgments
-
This project was created to solidify my understanding of SQL and Python integration.
Thanks to the open-source community for the resources and inspiration!

//HAPPY CODING
