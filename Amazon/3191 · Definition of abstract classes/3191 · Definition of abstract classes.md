### 3191 · Definition of abstract classes
PHP
Naive
Accepted Rate
94%


### Description
Ming is about to learn about abstract classes in PHP and he wants to create an abstract class named Solution in the Solution.php file. Please help him in implementing this functionality.

Write your code in the Solution.php file under // write your code here.

Example
The question does not have any input data, just create a Solution abstract class in the Solution.php file, we will verify that the class is defined successfully, if it is created successfully, it will output in the console
```py

Abstract class created successfully.
```

Otherwise, it will output

Abstract class created failure.


## Example
```python


```
```python


```
### SOLVE this:

///main.php
```php
<?php
require "Solution.php";

$data = fopen($argv[1], "r");
$out = fopen($argv[2], "w");

// Editable
$solution = new ReflectionClass('Solution');
if($solution->isAbstract()){
	fwrite($out, "Abstract class created successfully.");
} else{
	fwrite($out, "Abstract class created failure.");
}

fclose($data);
fclose($out);
?>


```
//project.php
```php
<?php
// write your code here  

?>
```

### Tags

## Company
Amazon

### Related Problems






### best answer
```php
main.php
<?php
require "Solution.php";

$data = fopen($argv[1], "r");
$out = fopen($argv[2], "w");

// Editable
$solution = new ReflectionClass('Solution');
if($solution->isAbstract()){
	fwrite($out, "Abstract class created successfully.");
} else{
	fwrite($out, "Abstract class created failure.");
}

fclose($data);
fclose($out);
?>
--------------------
project.php

<?php
// write your code here  
abstract class Solution {
}
?>

```
///
```php
main.php
---------
<?php
require "Solution.php";

$data = fopen($argv[1], "r");
$out = fopen($argv[2], "w");

// Editable
$solution = new ReflectionClass('Solution');
if($solution->isAbstract()){
	fwrite($out, "Abstract class created successfully.");
} else{
	fwrite($out, "Abstract class created failure.");
}

fclose($data);
fclose($out);
?>

project.php
-----------------
<?php
// write your code here  
abstract class Solution{}
?>
```


### Official answer from lintcode

```py

```