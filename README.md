##Form Validation With PHP Regular Expression

First Connect the Bootstrap Css and Js cdn

```sh
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

  <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>

```

###Write Down the form html

```sh
  <form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>" method="POST" class="form" id="form">
       <div class="form-group ">
            <input type="name" required class="form-control" placeholder="Enter Your Name*" name="name" id="name">
            <span class="error"><?=$nameerror?$nameerror : "" ?></span>
       </div>
       <div class="form-group">
            <input type="email" required class="form-control" placeholder="Enter Your Email*" name="email" id="email">
            <span class="error"> <?=$emailerror?$emailerror : "" ?></span>
       </div>
       <div class="form-group">
            <input type="number" required class="form-control" placeholder="Enter Your Phone Number*" name="phone" id="phone">
            <span class="error"> <?=$phoneerror?$phoneerror : "" ?></span>
       </div>
        <div class="form-group">
            <textarea name="message" id="message" placeholder="Enter your Message" class="form-control"></textarea>
        </div>
        <div class="form-group">
             <input type="submit" name="send" id="submit" class="btn btn-success" value="send">
        </div>             
  </form> 
```

###Declare the variable

```sh
$name = $email = $phone = $message = $nameerror = $emailerror = $phoneerror = $messageerror = null;
```

###Check all the field is empty or not. if empty then print a message

```sh
if ($_SERVER["REQUEST_METHOD"] == 'POST') {

    if (empty($_POST["name"])) {
        $nameerror = "Name is required";
    } else {
        $name = $_POST["name"];
    }
    if (empty($_POST["email"])) {
        $emailerror = "Email is required";
    } else {
        $email = $_POST["email"];

    }
    if (empty($_POST["phone"])) {
        $phoneerror = "Phone is required & Its must be Bangladesh Number";
    } else {
        $phone = $_POST["phone"];

        $pattern = '/^(?:\+88|88)?(01[3-9]\d{8})$/';

        if (preg_match($pattern, $phone) == 0) {
            $phoneerror = "Please Enter Valid Bangladesh Number";
        } else {
            $phone = $_POST["phone"];
        }
    }

    if (empty($_POST["message"])) {
        $messageerror = "";
    } else {
        $message = $_POST["message"];
    }

}
```


###Here is the html for showing the Result

```sh
        <h6>Output</h6>
        <table>
            <tr>
                <td>Name: </td>
                <td><?=$name?$name:""?></td>
            </tr>
            <tr>
                <td>Email: </td>
                <td><?=$email?$email:""?></td>
            </tr>
            <tr>
                <td>Phone: </td>
                <td><?=$phone?$phone:""?></td>
            </tr>
            <tr>
                <td>Message: </td>
                <td><?=$message?$message:""?></td>
            </tr>
        </table>   
```