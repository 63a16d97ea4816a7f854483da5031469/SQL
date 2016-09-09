#java.sql.SQLException: Data truncated for column 'MonthlyIncome' at row 1 error


Typically this problem occurs when you are putting in a data that is too long for the column. In this case, whatever data you are updating the 'MonthlyIncome' field with is too long.