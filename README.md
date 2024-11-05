<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Horror Login</title>
    <style>
        /* Global Styles */
        body {
            font-family: 'Courier New', monospace; /* Typewriter font for eerie effect */
            background-color: #111; /* Dark, unsettling background */
            color: #ddd; /* Light gray text */
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            flex-direction: column;
            overflow: hidden;
        }

        h1 {
            font-size: 3em;
            text-align: center;
            color: #ff3333; /* Blood red color */
            text-shadow: 2px 2px 5px #000, 0 0 20px #ff3333, 0 0 30px #ff3333; /* Glowing red text effect */
            margin-bottom: 20px;
            animation: flicker 1s infinite; /* Flickering effect for horror */
        }

        @keyframes flicker {
            0% { opacity: 1; }
            50% { opacity: 0.6; }
            100% { opacity: 1; }
        }

        h2 {
            color: #aaa; /* Dimmed gray for headings */
            text-shadow: 0 0 5px #ff3333; /* Subtle red glow */
            margin-bottom: 10px;
        }

        p {
            color: #ff6666; /* Light blood red */
            font-size: 14px;
            text-align: center;
            margin-top: 5px;
        }

        /* Form Styles */
        input[type="text"], input[type="password"] {
            background-color: #333; /* Dark background for inputs */
            border: 2px solid #555; /* Dark border for inputs */
            color: #ddd; /* Light text for inputs */
            padding: 12px;
            width: 250px;
            margin: 15px 0;
            font-size: 16px;
            border-radius: 5px;
            outline: none;
            text-align: center;
            box-shadow: 0 0 10px #ff3333; /* Red glow around input */
            transition: all 0.3s ease-in-out;
        }

        input[type="text"]:focus, input[type="password"]:focus {
            box-shadow: 0 0 20px #ff6666, 0 0 30px #ff6666; /* Redder glow when focused */
        }

        button {
            background-color: #444; /* Dark background for buttons */
            border: 2px solid #ff3333; /* Blood red border */
            color: #ddd; /* Light text */
            padding: 12px 20px;
            cursor: pointer;
            font-size: 16px;
            border-radius: 5px;
            transition: all 0.3s ease-in-out;
            text-transform: uppercase;
            position: relative;
        }

        button:hover {
            background-color: #ff3333; /* Blood red background on hover */
            color: #000; /* Dark text on red background */
            box-shadow: 0 0 15px #ff3333; /* Glowing effect on hover */
        }

        button:active {
            transform: scale(0.95); /* Button shrinking effect on click */
        }

        .hidden {
            display: none;
        }

        /* Welcome Screen Styles */
        #welcome {
            text-align: center;
            color: #aaa;
            font-size: 1.5em;
            margin-top: 20px;
            animation: fadeIn 2s ease-in-out;
        }

        @keyframes fadeIn {
            0% {
                opacity: 0;
            }
            100% {
                opacity: 1;
            }
        }

        /* Error Styles */
        #login-error {
            color: #ff6666; /* Blood red color */
            font-size: 14px;
            text-align: center;
            animation: shake 0.5s ease-in-out infinite; /* Error shake animation */
        }

        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }

        /* Spooky border effect */
        .bordered {
            border: 2px solid #555;
            padding: 20px;
            margin: 20px;
            border-radius: 10px;
            background: #222; /* Darker background for the form */
            box-shadow: 0 0 15px #ff3333;
        }
    </style>
</head>
<body>

    <!-- Login Form -->
    <div id="login-form" class="bordered">
        <h1>Blood Portal</h1>
        <h2>Login to your account</h2>
        <input type="text" id="username" placeholder="Username" />
        <input type="password" id="password" placeholder="Password" />
        <button onclick="login()">Login</button>
        <p id="login-error" class="hidden">Incorrect username or password!</p>
        <button onclick="showRegisterForm()">Don't have an account? Register</button>
    </div>

    <!-- Register Form -->
    <div id="register-form" class="hidden bordered">
        <h2>Register</h2>
        <input type="text" id="new-username" placeholder="Username" />
        <input type="password" id="new-password" placeholder="Password" />
        <button onclick="register()">Register</button>
        <button onclick="showLoginForm()">Back to Login</button>
    </div>

    <!-- Welcome Message -->
    <div id="welcome" class="hidden">
        <h2>Welcome, <span id="user-name"></span>...</h2>
        <button onclick="logout()">Logout</button>
    </div>

    <script>
        // Check if user is already logged in
        if (localStorage.getItem('user')) {
            showWelcomePage();
        }

        function showLoginForm() {
            document.getElementById("login-form").classList.remove("hidden");
            document.getElementById("register-form").classList.add("hidden");
            document.getElementById("login-error").classList.add("hidden");
        }

        function showRegisterForm() {
            document.getElementById("login-form").classList.add("hidden");
            document.getElementById("register-form").classList.remove("hidden");
        }

        function showWelcomePage() {
            document.getElementById("login-form").classList.add("hidden");
            document.getElementById("register-form").classList.add("hidden");
            document.getElementById("welcome").classList.remove("hidden");
            document.getElementById("user-name").innerText = localStorage.getItem('user');
        }

        // Register a new user
        function register() {
            const username = document.getElementById("new-username").value;
            const password = document.getElementById("new-password").value;

            if (!username || !password) {
                alert("Please enter both a username and password!");
                return;
            }

            // Store user credentials in localStorage
            localStorage.setItem('user', username);
            localStorage.setItem('password', password);

            alert("Registration successful... if you dare.");
            showLoginForm();
        }

        // Log in the user
        function login() {
            const username = document.getElementById("username").value;
            const password = document.getElementById("password").value;

            const storedUsername = localStorage.getItem('user');
            const storedPassword = localStorage.getItem('password');

            // Check if credentials match
            if (username === storedUsername && password === storedPassword) {
                showWelcomePage();
            } else {
                document.getElementById("login-error").classList.remove("hidden");
            }
        }

        // Log out the user
        function logout() {
            localStorage.removeItem('user');
            localStorage.removeItem('password');
            showLoginForm();
        }
    </script>

</body>
</html>
