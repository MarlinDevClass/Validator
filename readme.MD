# Simple PHP Validator


## Usage
```php 
require_once('Validator.php');
```
You must configure PDO connection in Database.php file to use unique method 

## Typical Use
```php
    $data = [
        'name' => 'Test',
        'email' => 'test@email.com',
        'phone' => '+308964433221',
        'password' => 'password',
        'password_confirm' => 'password',
        'date' => '2026-12-31'
    ];

    $val = new Validator($data);
```
Or you can initialize instance without argument. In this case system automatic gets data from $_POST or $_GET source 

```php
    $validate = new Validator;
```
To validate field you must enter field name in method field, and then call needed methods to validate

```php
    $validate->field('name')->required();
    $validate->field('email')->email()->required()->unique('users');
    $validate->field('password')->min(8)->max(12)->required();
    $validate->field('password_confirm')->matches('password');
    $validate->field('phone')->phone();
    $validate->field('date')->date();
    
    echo $validate->displayErrors();
```

## Simple Form HTML Use
```php
    <?php $validate = new Validation; ?>
    
    <form method="POST" action="#">
    	<label for="name">Name:</label>
            <input type="text" name="name">
        <label for="email">E-Mail:</label>
            <input type="email" name="email">
        <label for="password">Password:</label>
            <input type="password" name="password">
        <label for="password_confirm">Password confirm:</label>
            <input type="password" name="password_confirm">
        <button type="submit">Send</button>
    </form>
    
    <?php     	
        if(!empty($_POST)){
          $validate->field('name')->required();
          $validate->field('email')->email()->required()->unique('users');
          $validate->field('password')->min(8)->max(12)->required();
          $validate->field('password_confirm')->matches('password');

          if($validate->isSuccess()){
              echo 'Validation ok!';        
          }else{
              echo $val->displayErrors();
          }
      }
    ?>
```