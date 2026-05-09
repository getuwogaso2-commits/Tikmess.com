<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Secure Login</title>
<meta name="google-adsense-account" content="ca-pub-5968278007440676">
<style>

*:

body{
    background:black;
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
}

.container{
    width:350px;
    padding:40px;
    border-radius:40px;
    background: #000033;

    box-shadow:
    10px 10px 20px #bebebe,
    -10px -10px 20px #ffffff;
}

h2{
    text-align:center;
    margin-bottom:20px;
    color: white;
}

input{
    width:100%;
    padding:14px;
    margin-top:12px;
    border:none;
    border-radius:12px;
    outline:none;
    font-size:16px;

    box-shadow:
    inset 5px 5px 10px #bebebe,
    inset -5px -5px 10px #ffffff;
}

button{
    width:100%;
    padding:14px;
    margin-top:20px;
    border:none;
    border-radius:12px;
    background: deepskyblue;
    color:white;
    font-size:17px;
    cursor:pointer;
}

#msg{
    margin-top:15px;
    text-align:center;
    color:red;
    font-size:15px;
}

.rules{
    margin-top:15px;
    font-size:13px;
    color:#444;
}

</style>
</head>

<body>

<div class="container">

    <h2>Secure Login</h2>

    <input type="text"
    id="username"
    placeholder="Username">

    <input type="text"
    id="email"
    placeholder="example@gmail.com">

    <input type="password"
    id="password"
    placeholder="Password">

    <div class="rules">

        Password must contain:
        <br><br>

        ✔ Capital Letter
        <br>

        ✔ Small Letter
        <br>

        ✔ Number
        <br>

        ✔ Symbol
        <br>

        ✔ 8 Characters

    </div>

    <button onclick="login()">
        Login
    </button>

    <div id="msg"></div>

</div>

<script>

function validEmail(email){

    // MUST HAVE @
    if(email.indexOf("@") == -1){
        return false;
    }

    // MUST HAVE .com
    if(email.indexOf(".com") == -1){
        return false;
    }

    // MUST NOT START WITH @
    if(email.startsWith("@")){
        return false;
    }

    return true;

}

function validPassword(password){

    let capital =
    /[A-Z]/.test(password);

    let small =
    /[a-z]/.test(password);

    let number =
    /[0-9]/.test(password);

    let symbol =
    /[!@#$%^&*]/.test(password);

    if(
        capital &&
        small &&
        number &&
        symbol &&
        password.length >= 8
    ){

        return true;

    }else{

        return false;

    }

}

function login(){

    let username =
    document.getElementById("username").value;

    let email =
    document.getElementById("email").value;

    let password =
    document.getElementById("password").value;

    let msg =
    document.getElementById("msg");

    // EMPTY CHECK
    if(
        username == "" ||
        email == "" ||
        password == ""
    ){

        msg.innerHTML =
        "Fill all fields";

        return;
    }

    // USERNAME CHECK
    if(username.length < 3){

        msg.innerHTML =
        "Username too short";

        return;
    }

    // EMAIL CHECK
    if(!validEmail(email)){

        msg.innerHTML =
        "Wrong Email";

        return;
    }

    // PASSWORD CHECK
    if(!validPassword(password)){

        msg.innerHTML =
        "Weak Password";

        return;
    }

    // SUCCESS
    msg.style.color = "green";

    msg.innerHTML =
    "Login Successful ✔";

    // GO NEXT PAGE
    setTimeout(function(){

        window.location.href =
        "Tikmess.html";

    },1000);

}

</script>

</body>
</html>
