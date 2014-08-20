## Console Lab

For this lab, we'd like you to strengthen your Rails console skills. This lab is going to be very familiar to the SQL lab, where we'll ask you to create a model and then write out the console commands you would use to execute these queries

### To Start

1. Create a model called Student, that has a first_name, last_name and age

	rails generate model Student first_name:string last_name:string age:integer

2. Don't forget to run your migrations

	rake db:create
	rake db:migrate

### Tasks to create

to start console: rails c

1. Using the new/save syntax, create a student, first and last name and an age 

	me = Student.new
	me.first_name = "Kevin"
	me.last_name = "Chou"
	me.age = 24

2. Save the student to the database

	me.save

3. Using the find/set/save syntax update the student's first name to taco

	me = Student.find(1)
	me.update_attributes(:first_name => "Taco")

4. Delete the student (where first_name is taco)

	me = Student.find_by_first_name("Taco")
	me.destroy

5. Validate that every Student's last name is unique

	validates_uniqueness_of :last_name => true

6. Validate that every Student has a first and last name that is longer than 4 characters

	validates_length_of :first_name, {:minimum => 4}
	validates_length_of :last_name, {:minimum => 4}

7. Validate that every first and last name cannot be empty

	validates_presence_of :first_name
	validates_presence_of :last_name

8. Combine all of these individual validations into one validation (using validate and a hash) 

	validate :first_name, :presence => true, :length => {:minimum => 4}
	validate :last_name, :presence => true, :length => {:minimum => 4}, :uniqueness => true

9. Using the create syntax create a student named John Doe who is 33 years old

	student = Student.create(:first_name => "John", :last_name => "Doe", :age => 33)

10. Show if this new student entry is valid

	student.valid?

11. Show the number of errors for this student instance

	student.errors.size

12. In one command, Change John Doe's name to Jonathan Doesmith 

	student.update(:first_name => "Jonathan", :last_name => "Doesmith")
	
13. Clear the errors array

	student.errors.clear

14. Save Jonathan Doesmith

	student.save

15. Find all of the Students

	Student.all

16. Find the student with an ID of 128 and if it does not exist, make sure it returns nil and not an error

	Student.find_by_id(128)

17. Find the first student in the table
	
	Student.first

18. Find the last student in the table

	Student.last

19. Find the student with the last name of Doesmith

	Student.find_by_last_name("Doesmith")

20. Find all of the students and limit the search to 5 students, starting with the 2nd student and finally, order the students in alphabetical order
	
	Student.all.order(:first_name).offset(1).limit(5)

21. Delete Jonathan Doesmith
	
	jonathan = Student.where("last_name =?", "Doesmith")
	jonathan.destroy

### Bonus
1. Use the validates_format_of and regex to only validate names that consist of letters (no numbers or symbols) and start with a capital letter
2. Write a custom validation to ensure that no one named Delmer Reed, Tim Licata, Anil Bridgpal or Elie Schoppik is included in the students table


