# password-manager
<!DOCTYPE html>
<html>
<head>
    <title>All in One Project</title>
    <style>
        body { font-family: Arial; text-align: center; }
        .box { border: 1px solid #ccc; padding: 20px; margin: 20px; }
        input { margin: 5px; padding: 5px; }
        button { padding: 6px 12px; }
    </style>
</head>
<body>

<!-- PASSWORD GENERATOR -->
<div class="box">
    <h2>Password Generator</h2>

    Length: <input type="number" id="length" value="8"><br>

    <input type="checkbox" id="num"> Numbers
    <input type="checkbox" id="upper"> Uppercase
    <input type="checkbox" id="special"> Special<br><br>

    <button onclick="generatePassword()">Generate</button>

    <h3 id="password"></h3>
</div>

<!-- REGISTER -->
<div class="box">
    <h2>Register</h2>

    <input type="text" id="username" placeholder="Username"><br>
    <input type="email" id="email" placeholder="Email"><br>
    <input type="password" id="pass" placeholder="Password"><br>
    <input type="password" id="confirm" placeholder="Repeat Password"><br>

    <button onclick="register()">Register</button>
</div>

<!-- LOGIN -->
<div class="box">
    <h2>Login</h2>

    <input type="email" id="loginEmail" placeholder="Email"><br>
    <input type="password" id="loginPass" placeholder="Password"><br>

    <button onclick="login()">Login</button>
</div>

<!-- HOME -->
<div class="box" id="home" style="display:none;">
    <h2>Welcome 🎉</h2>
    <p>Login Successful</p>
</div>

<script>
/* PASSWORD GENERATOR */
function generatePassword() {
    let len = document.getElementById("length").value;
    let chars = "abcdefghijklmnopqrstuvwxyz";

    if (document.getElementById("num").checked)
        chars += "0123456789";

    if (document.getElementById("upper").checked)
        chars += "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    if (document.getElementById("special").checked)
        chars += "!@#$%";

    let pass = "";
    for (let i = 0; i < len; i++) {
        pass += chars[Math.floor(Math.random() * chars.length)];
    }

    document.getElementById("password").innerText = pass;
}

/* REGISTER */
function register() {
    let username = document.getElementById("username").value;
    let email = document.getElementById("email").value;
    let pass = document.getElementById("pass").value;
    let confirm = document.getElementById("confirm").value;

    let emailPattern = /^[^ ]+@[^ ]+\.[a-z]{2,3}$/;

    if (username.length <= 6) {
        alert("Username must be > 6 characters");
        return;
    }

    if (!email.match(emailPattern)) {
        alert("Invalid Email");
        return;
    }

    if (pass.length <= 8) {
        alert("Password must be > 8 characters");
        return;
    }

    if (pass !== confirm) {
        alert("Passwords do not match");
        return;
    }

    localStorage.setItem("email", email);
    localStorage.setItem("password", pass);

    alert("Registered Successfully");
}

/* LOGIN */
function login() {
    let email = document.getElementById("loginEmail").value;
    let pass = document.getElementById("loginPass").value;

    let storedEmail = localStorage.getItem("email");
    let storedPass = localStorage.getItem("password");

    if (email !== storedEmail) {
        alert("Email not registered");
        return;
    }

    if (pass !== storedPass) {
        alert("Invalid credentials");
        return;
    }

    alert("Login Successful");

    document.getElementById("home").style.display = "block";
}
</script>

</body>
</html>
