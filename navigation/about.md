---
layout: page
title: About me
permalink: /about/
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>About Me - Mihir Thaha</title>
    <style>
        /* Gradient background styling */
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(to bottom right, #00c6ff, #0072ff);
            color: white;
        }

        /* Styling for the flag container */
        .flag-container {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-top: 50px;
        }

        .flag {
            text-align: center;
            margin-right: 20px;
        }

        .flag img {
            width: 200px;
        }

        /* Centering and text styling */
        h1 {
            text-align: center;
            margin-top: 30px;
        }

        ul {
            list-style: none;
            padding: 0;
            text-align: center;
            line-height: 1.8;
        }
    </style>
</head>
<body>
    <h1>About Me</h1>
    <p>👋 Hi, I'm <strong>Mihir Thaha</strong>!</p>
    <ul>
        <li>🇮🇳 <strong>Nationality:</strong> Indian</li>
        <li>🎂 <strong>Age:</strong> 15 years old</li>
        <li>🎓 <strong>Education:</strong> Sophomore at Del Norte High School</li>
        <li>🌍 <strong>Location:</strong> California, USA</li>
    </ul>
    <div class="flag-container">
        <div class="flag" id="californiaFlag">
            <p>California</p>
        </div>
        <div class="flag" id="indiaFlag">
            <p>India</p>
        </div>
    </div>

    <script>
        // JavaScript to dynamically insert image URLs
        var californiaFlagUrl = "https://upload.wikimedia.org/wikipedia/commons/0/01/Flag_of_California.svg";
        var indiaFlagUrl = "https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg";

        document.getElementById('californiaFlag').innerHTML = '<img src="' + californiaFlagUrl + '" alt="California Flag"><p>California</p>';
        document.getElementById('indiaFlag').innerHTML = '<img src="' + indiaFlagUrl + '" alt="Indian Flag"><p>India</p>';
    </script>
</body>
</html>
