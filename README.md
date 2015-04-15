# Validator
Simple form validation PHP class for POST request, useful when coding without a framework.

# Featured constraints
It supports the following constraints:
- required: checks if the field is not empty
- unique: checks if the field value is not taken through a callback function provided by you
- char: checks if the field does not contain digits (0-9)
- integer: checks if the field is an integer number
- float: checks if the field is a decimal number
- email: checks if the field is a valid email address

# Callback for unique constraint
This feature is intended for database checks and calls an user-provided function which should check for uniqueness of the value in the database.
To the user-provided function will be passed two arguments, $id and $value, respectively the id of the record we are modifying (0 in case we are adding a new record) 
and the value to check.

A basic example would be:
```
function isNameAvailable($id, $value)
{
  $connection = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8', 'username', 'password');
	
	$statement = $connection->prepare('SELECT title FROM articles WHERE title = :name AND id != :id');
	$statement->bindValue(':name', $value, PDO::PARAM_STR);
	$statement->bindValue(':id', $id, PDO::PARAM_INT);
	
	$statement->execute();
	
	return $statement->fetchAll() != null;
}
```
