---
layout: none
permalink: /stocks/test
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Menu</title>
    <link rel="stylesheet" href="indexstyles.css">
    <style>
        body {
            text-align: center;
            margin-top: 100px;
            font-family: Arial, sans-serif;
            background-image: url('https://img.freepik.com/premium-vector/vector-binary-code-green-background-big-data-programming-hacking-deep-decryption-encryption-computer-streaming-numbers-1-0-coding-hacker-concept_167184-283.jpg');
            background-size: cover;
            background-repeat: no-repeat;
            background-position: center center;
            height: 100vh;
        }
        button,button::after {
            padding: 10px 50px;
            font-size: 80px;
            border: none;
            border-radius: 5px;
            color: white;
            background-color: transparent;
            position: relative;
        }
        button::after {
            --move1: inset(50% 50% 50% 50%);
            --move2: inset(31% 0 40% 0);
            --move3: inset(39% 0 15% 0);
            --move4: inset(45% 0 40% 0);
            --move5: inset(45% 0 6% 0);
            --move6: inset(14% 0 61% 0);
            clip-path: var(--move1);
            content: 'GLITCH';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            display: block;
        }
        button:hover::after {
            animation: glitch_4011 1s;
            text-shadow: 10 10px 10px black;
            animation-timing-function: steps(2, end);
            text-shadow: -3px -3px 0px #1df2f0, 3px 3px 0px #E94BE8;
            background-color: transparent;
            border: 3px solid rgb(0, 255, 213);
        }
        button:hover {
            text-shadow: -1px -1px 0px #1df2f0, 1px 1px 0px #E94BE8;
        }
        button:hover {
            background-color: transparent;
            border: 1px solid rgb(0, 255, 213);
            box-shadow: 0px 10px 10px -10px rgb(0, 255, 213);
        }
        @keyframes glitch_4011 {
            0% {
                clip-path: var(--move1);
                transform: translate(0px,-10px);
            }
            10% {
                clip-path: var(--move2);
                transform: translate(-10px,10px);
            }
            20% {
                clip-path: var(--move3);
                transform: translate(10px,0px);
            }
            30% {
                clip-path: var(--move4);
                transform: translate(-10px,10px);
            }
            40% {
                clip-path: var(--move5);
                transform: translate(10px,-10px);
            }
            50% {
                clip-path: var(--move6);
                transform: translate(-10px,10px);
            }
            60% {
                clip-path: var(--move1);
                transform: translate(10px,-10px);
            }
            70% {
                clip-path: var(--move3);
                transform: translate(-10px,10px);
            }
            80% {
                clip-path: var(--move2);
                transform: translate(10px,-10px);
            }
            90% {
                clip-path: var(--move4);
                transform: translate(-10px,10px);
            }
            100% {
                clip-path: var(--move1);
                transform: translate(0);
            }
        }
        .glitch {
            position: relative;
            font-size: 100px;
            font-weight: 700;
            line-height: 1.2;
            color: #fff;
            letter-spacing: 5px;
            z-index: 1;
            animation: shift 1s ease-in-out infinite alternate;
        }
        .glitch:before,
        .glitch:after {
            display: block;
            content: attr(data-glitch);
            position: absolute;
            top: 0;
            left: 0;
            opacity: 0.8;
        }
        .glitch:before {
            animation: glitch 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94) both infinite;
            color: #8b00ff;
            z-index: -1;
        }
        .glitch:after {
            animation: glitch 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94) reverse both infinite;
            color: #00e571;
            z-index: -2;
        }
        @keyframes glitch {
            0% {
                transform: translate(0);
            }
            20% {
                transform: translate(-3px, 3px);
            }
            40% {
                transform: translate(-3px, -3px);
            }
            60% {
                transform: translate(3px, 3px);
            }
            80% {
                transform: translate(3px, -3px);
            }
            to {
                transform: translate(0);
            }
        }
        @keyframes shift {
            0%, 40%, 44%, 58%, 61%, 65%, 69%, 73%, 100% {
                transform: skewX(0deg);
            }
            41% {
                transform: skewX(10deg);
            }
            42% {
                transform: skewX(-10deg);
            }
            59% {
                transform: skewX(40deg) skewY(10deg);
            }
            60% {
                transform: skewX(-40deg) skewY(-10deg);
            }
            63% {
                transform: skewX(10deg) skewY(-5deg);
            }
            70% {
                transform: skewX(-50deg) skewY(-20deg);
            }
            71% {
                transform: skewX(10deg) skewY(-10deg);
            }
        }
        .login-container {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap; /* allows the cards to wrap onto the next line if the screen is too small */
    color: #fff; /* set text to white */
    padding: 20px;
    border-radius: 10px;
}
.login-card {
    margin-top: 0; /* remove the top margin */
    width: 45%;
    border: 1px solid #ddd;
    border-radius: 5px;
    padding: 20px;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    margin-bottom: 20px;
    overflow-x: auto; /* Enable horizontal scrolling */
    background-color: #000; /* set background to black */
    color: #fff; /* set text to white */
    background-position: center center;
}
.login-card input,
.login-card label,
.login-card button {
    color: #fff; /* set input text, label, and button text to white */
}
.login-card input {
    background-color: #333; /* set input background to dark gray */
    border: 1px solid #fff; /* white border for inputs */
}
.login-card h1 {
    margin-bottom: 20px;
}
.signup-card {
    margin-top: 0; /* remove the top margin */
    width: 45%;
    border: 1px solid #ddd;
    border-radius: 5px;
    padding: 20px;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    margin-bottom: 20px;
    overflow-x: auto; /* Enable horizontal scrolling */
}
.signup-card h1 {
    margin-bottom: 20px;
}
    </style>
</head>
<body>
    <div style="text-align: center; margin-top: 100px;">
        <div class="loader">
            <div data-glitch="CSA Student: The Adventure" class="glitch">CSA Student: The Adventure</div>
        </div>
        <div class="login-container">
    <!-- Python Login Form -->
    <div class="login-card">
        <h1 id="pythonTitle">User Login</h1>
        <form id="pythonForm" onsubmit="pythonLogin(); return false;">
            <p>
                <label>
                    ID:
                    <input type="text" name="uid" id="uid" required>
                </label>
            </p>
            <p>
                <label>
                    Password:
                    <input type="password" name="password" id="password" required>
                </label>
            </p>
            <p>
                <button type="submit">Login</button>
            </p>
            <p id="message" style="color: red;"></p>
        </form>
    
</div>
    </div>

<script type="module">
    import { login, pythonURI, fetchOptions } from '{{site.baseurl}}/assets/js/api/config.js';

    // Function to handle Python login
    window.pythonLogin = function() {
        const options = {
            URL: `${pythonURI}/api/authenticate`,
            callback: pythonDatabase,
            message: "message",
            method: "POST",
            cache: "no-cache",
            body: {
                uid: document.getElementById("uid").value,
                password: document.getElementById("password").value,
            }
        };
        login(options);
    }

    // Function to handle signup
    window.signup = function() {
    const signupButton = document.querySelector(".signup-card button");

    // Disable the button and change its color
    signupButton.disabled = true;
    signupButton.style.backgroundColor = '#d3d3d3'; // Light gray to indicate disabled state

    const signupOptions = {
        URL: `${pythonURI}/api/user`,
        method: "POST",
        cache: "no-cache",
        body: {
            name: document.getElementById("name").value,
            uid: document.getElementById("signupUid").value,
            password: document.getElementById("signupPassword").value,
            kasm_server_needed: document.getElementById("kasmNeeded").checked,
        }
    };

    fetch(signupOptions.URL, {
        method: signupOptions.method,
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(signupOptions.body)
    })
    .then(response => {
        if (!response.ok) {
            throw new Error(`Signup failed: ${response.status}`);
        }
        return response.json();
    })
    .then(data => {
        document.getElementById("signupMessage").textContent = "Signup successful!";
        // Optionally redirect to login page or handle as needed
        // window.location.href = '{{site.baseurl}}/profile';
    })
    .catch(error => {
        console.error("Signup Error:", error);
        document.getElementById("signupMessage").textContent = `Signup Error: ${error.message}`;
        // Re-enable the button if there is an error
        signupButton.disabled = false;
        signupButton.style.backgroundColor = ''; // Reset to default color
    });
}


    // Function to fetch and display Python data
    function pythonDatabase() {
        const URL = `${pythonURI}/api/id`;

        fetch(URL, fetchOptions)
            .then(response => {
                if (!response.ok) {
                    throw new Error(`Flask server response: ${response.status}`);
                }
                return response.json();
            })
            .then(data => {
                window.location.href = '{{site.baseurl}}/profile';
            })
            .catch(error => {
                console.error("Python Database Error:", error);
                const errorMsg = `Python Database Error: ${error.message}`;
            });
    }

    // Call relevant database functions on the page load
    window.onload = function() {
         pythonDatabase();
    };
</script>