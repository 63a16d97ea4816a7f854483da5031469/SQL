##Add a column to an existing MySQL table


http://www.tech-recipes.com/rx/378/add-a-column-to-an-existing-mysql-table/

To add a column called email to the contacts table created in Create a basic MySQL table with a datatype of VARCHAR(80), use the following SQL statement:

ALTER TABLE contacts ADD email VARCHAR(80);

This first statement will add the email column to the end of the table. To insert the new column after a specific column, such as name, use this statement:

ALTER TABLE contacts ADD email VARCHAR(60) AFTER name;

If you want the new column to be first, use this statement:

ALTER TABLE contacts ADD email VARCHAR(60) FIRST;