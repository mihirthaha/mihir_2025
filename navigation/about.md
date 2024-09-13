---
layout: page
title: About
permalink: /about/
---

<style>
    /* Gradient background styling */
    html {
        margin: 0;
        font-family: Arial, sans-serif;
        background: linear-gradient(to bottom right, #b3b3b3, #4d4d4d);
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

<ul>
    <li>👋 Hi, I'm <strong>Mihir Thaha</strong>!</li>
    <li>🇮🇳 <strong>Nationality:</strong> Indian</li>
    <li>🎂 <strong>Age:</strong> 15 years old</li>
    <li>🎓 <strong>Education:</strong> Sophomore at Del Norte High School</li>
    <li>🌍 <strong>Location:</strong> California, USA</li>
</ul>

# About Me

👋 Hi, I'm Mihir Thaha!

I’m currently a sophomore at Del Norte High School in California, USA. I love learning about diverse cultures and languages, which has shaped how I approach life and learning.

### My Interests
I'm passionate about technology, especially in areas like coding, web development, and engineering. I’ve been learning Python and JavaScript, working on small projects that help me build my skills and understanding of how software works.

### Hobbies
I love playing badminton and basketball, as well as going to the gym. I also like reading and watching YouTube in my freetime.

### Future Goals
In this course, I expect to build a functional website and expand my knowledge on computer science. I also want to have fun while coding.

### Connect With Me
Feel free to check out my [GitHub](https://github.com/mihirthaha) for my latest projects, or contact me at [mihirthaha@gmail.com](mailto:mihirthaha@gmail.com).

<div class="flag-container">
    <div class="flag" id="californiaFlag">
        <p>California</p>
    </div>
    <div class="flag" id="indiaFlag">
        <p>India</p>
    </div>
</div>

<script>
    // JavaScript to dynamically insert image URLs using baseurl
    var californiaFlagUrl = "{{ site.baseurl }}/assets/images/Flag_of_California.svg";
    var indiaFlagUrl = "{{ site.baseurl }}/assets/images/Flag_of_India.svg";
    var Mihirt = "{{site.baseurl }}/assets/imagess/

    document.getElementById('californiaFlag').innerHTML = '<img src="' + californiaFlagUrl + '" alt="California Flag"><p>California</p>';
    document.getElementById('indiaFlag').innerHTML = '<img src="' + indiaFlagUrl + '" alt="Indian Flag"><p>India</p>';
    document.getElementById('mihirthaha').innerHTML = '<img src=" ' + Mihirt + ' " alt=MihirT"><p>Me as a kid</p>
</script>
