# Lab 1 — Getting Started with D3.js

**STATS 401: Data Acquisition and Visualization**

## Learning Objectives

By the end of this lab, you should be able to:

1. Explain the roles of HTML, CSS, and JavaScript in a web visualization.
2. Add the D3.js library to a webpage.
3. Use JavaScript and D3 to manipulate the Document Object Model (DOM).
4. Create basic graphical elements using SVG.
5. Load CSV and JSON data using D3.
6. Build a course webpage containing navigation tabs for all 10 labs.
7. Run a D3 website locally.
8. Publish a D3 website using GitHub Pages.
9. Create and deploy your first D3 visualization.

---

## 0. Preparation

For this course, each student will maintain one website containing all 10 labs.

A recommended project structure is:

```text
stats401-labs/
│
├── index.html
├── css/
│   └── style.css
├── js/
│   └── main.js
│
├── data/
│   ├── students.csv
│   └── students.json
│
├── lab1/
│   └── index.html
├── lab2/
│   └── index.html
├── lab3/
│   └── index.html
├── lab4/
│   └── index.html
├── lab5/
│   └── index.html
├── lab6/
│   └── index.html
├── lab7/
│   └── index.html
├── lab8/
│   └── index.html
├── lab9/
│   └── index.html
└── lab10/
    └── index.html
```

This website will grow throughout the semester.

Your final URL may look similar to:

```text
https://yourusername.github.io/stats401-labs/
```

---

# Task 1 — HTML, CSS, and JavaScript

Before learning D3, we need to understand the three fundamental technologies used by webpages.

For more detailed information about HTML, CSS, and JS, please refer to [w3schools](https://www.w3schools.com/html/default.asp) 

## 1.1 HTML

HTML defines the **structure and content** of a webpage.

Create a file named:

```text
index.html
```

Add the following code:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <title>STATS 401 Labs</title>
</head>

<body>

    <h1>STATS 401: Data Acquisition and Visualization</h1>

    <h2>Lab 1: Getting Started with D3.js</h2>

    <p>
        This is my first webpage for STATS 401.
    </p>

</body>

</html>
```

Open `index.html` in your browser.

You should see a simple webpage containing a heading and paragraph.

---

## 1.2 Common HTML Elements

Some HTML elements you will frequently use include:

```html
<h1>Main heading</h1>

<h2>Section heading</h2>

<p>This is a paragraph.</p>

<a href="https://d3js.org/">Visit D3</a>

<button>Click Me</button>

<div>
    A general container
</div>
```

The `<div>` element is especially important because we frequently use it as a container for visualizations.

For example:

```html
<div id="chart"></div>
```

Later, D3 can locate this element and insert a visualization inside it.

---

## 1.3 CSS

CSS controls the **appearance** of a webpage.

Create:

```text
css/style.css
```

Add:

```css
body {
    font-family: Arial, sans-serif;
    max-width: 1000px;
    margin: 40px auto;
    padding: 0 20px;
}

h1 {
    font-size: 32px;
}

h2 {
    margin-top: 30px;
}

p {
    line-height: 1.6;
}

#chart {
    margin-top: 30px;
}
```

Now connect the CSS file to your HTML.

Inside `<head>`, add:

```html
<link rel="stylesheet" href="css/style.css">
```

Your `<head>` should now look like:

```html
<head>

    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <title>STATS 401 Labs</title>

    <link rel="stylesheet" href="css/style.css">

</head>
```

Refresh the browser.

The webpage should now have improved spacing and typography.

---

## 1.4 JavaScript

JavaScript provides **behavior and interaction**.

Create:

```text
js/main.js
```

Add:

```javascript
console.log("Hello STATS 401!");
```

Connect it to the webpage immediately before `</body>`:

```html
<script src="js/main.js"></script>
```

Your page should end with:

```html
<script src="js/main.js"></script>

</body>
</html>
```

Open the browser's Developer Tools.

Usually:

```text
Right Click → Inspect → Console
```

You should see:

```text
Hello STATS 401!
```

---

## 1.5 JavaScript Variables

Try adding:

```javascript
let course = "STATS 401";
let students = 40;

console.log(course);
console.log(students);
```

JavaScript arrays will be particularly important in D3:

```javascript
let data = [10, 20, 30, 40, 50];

console.log(data);
```

Objects are also frequently used:

```javascript
let student = {
    name: "Alice",
    score: 85
};

console.log(student.name);
console.log(student.score);
```

A D3 dataset is often an **array of objects**:

```javascript
let students = [
    {name: "Alice", score: 85},
    {name: "Bob", score: 72},
    {name: "Carol", score: 91}
];

console.log(students);
```

---

# Task 2 — Set Up D3.js

D3 stands for **Data-Driven Documents**.

D3 is a JavaScript library designed for creating data-driven web visualizations.

It provides tools for:

- selecting webpage elements;
- binding data to elements;
- creating scales;
- creating axes;
- manipulating SVG;
- loading external datasets;
- animation;
- interaction;
- geographic visualization;
- network visualization.

---

## 2.1 Add D3 to the Webpage

For this course, we will initially use D3 through a CDN.

Add the following before your own JavaScript:

```html
<script src="https://cdn.jsdelivr.net/npm/d3@7"></script>

<script src="js/main.js"></script>
```

The order matters.

D3 must be loaded **before** `main.js`.

---

## 2.2 Verify D3

Add this to `main.js`:

```javascript
console.log(d3);
```

Or:

```javascript
console.log("D3 version:", d3.version);
```

Open the browser console.

If D3 was successfully loaded, you should see its version number.

---

## 2.3 Your First D3 Command

Add a paragraph:

```html
<p id="message">Original message</p>
```

Then use D3:

```javascript
d3.select("#message")
    .text("This text was changed using D3!");
```

Refresh the webpage.

The text should change.

This demonstrates one of D3's central ideas:

```text
Find an element
      ↓
Select it
      ↓
Modify it
```

---

# Task 3 — Understanding the DOM

## 3.1 What Is the DOM?

When a browser reads HTML, it converts it into a tree-like structure called the:

**Document Object Model (DOM)**

For example:

```html
<body>

    <h1>STATS 401</h1>

    <div id="chart">

        <p>Hello</p>

    </div>

</body>
```

Conceptually becomes:

```text
document
   │
   └── body
       │
       ├── h1
       │
       └── div #chart
              │
              └── p
```

JavaScript and D3 manipulate this structure.

---

## 3.2 Selecting Elements

Suppose the webpage contains:

```html
<h2 id="title">My Visualization</h2>

<p class="description">
    Visualization description
</p>
```

D3 can select by tag:

```javascript
d3.select("h2");
```

Select by ID:

```javascript
d3.select("#title");
```

Select by class:

```javascript
d3.select(".description");
```

---

## 3.3 Changing Text

```javascript
d3.select("#title")
    .text("Student Score Visualization");
```

---

## 3.4 Changing Styles

```javascript
d3.select("#title")
    .style("color", "steelblue")
    .style("font-size", "28px");
```

Notice that D3 frequently uses **method chaining**:

```javascript
d3.select("#title")
    .style("color", "steelblue")
    .style("font-size", "28px")
    .style("font-weight", "bold");
```

---

## 3.5 Adding Elements

Start with:

```html
<div id="content"></div>
```

Then:

```javascript
d3.select("#content")
    .append("p")
    .text("This paragraph was created using D3.");
```

You can create multiple elements:

```javascript
const content = d3.select("#content");

content.append("h3")
    .text("My Dataset");

content.append("p")
    .text("The dataset contains student scores.");
```

---

## 3.6 Data Binding

The defining feature of D3 is binding data to DOM elements.

Consider:

```javascript
const data = [10, 20, 30, 40, 50];
```

Add:

```html
<div id="numbers"></div>
```

Then:

```javascript
d3.select("#numbers")
    .selectAll("p")
    .data(data)
    .join("p")
    .text(d => `Value: ${d}`);
```

The result is conceptually:

```text
Value: 10
Value: 20
Value: 30
Value: 40
Value: 50
```

The critical pattern is:

```javascript
selection
    .selectAll(...)
    .data(data)
    .join(...)
```

We will use this pattern repeatedly throughout the semester.

---

# Task 4 — SVG

D3 often uses **SVG** to draw visualizations.

SVG stands for:

**Scalable Vector Graphics**

Unlike a normal image, SVG consists of graphical elements represented directly in the DOM.

---

## 4.1 Create an SVG

Add:

```html
<svg width="600" height="300"></svg>
```

You will initially see nothing because the SVG is an empty drawing area.

Think of it as a coordinate system:

```text
(0,0) --------------------→ x
 |
 |
 |
 |
 ↓
 y
```

One important difference from a mathematical coordinate system is that the y-axis increases **downward**.

---

## 4.2 Draw a Circle

```html
<svg width="600" height="300">

    <circle
        cx="100"
        cy="100"
        r="40"
        fill="steelblue">
    </circle>

</svg>
```

Where:

```text
cx = horizontal position
cy = vertical position
r  = radius
```

---

## 4.3 Draw a Rectangle

```html
<svg width="600" height="300">

    <rect
        x="50"
        y="50"
        width="120"
        height="80"
        fill="orange">
    </rect>

</svg>
```

---

## 4.4 Draw SVG with D3

Instead of manually writing SVG, D3 can create it.

First add:

```html
<div id="svg-demo"></div>
```

Then:

```javascript
const svg = d3.select("#svg-demo")
    .append("svg")
    .attr("width", 600)
    .attr("height", 300);
```

Now add a circle:

```javascript
svg.append("circle")
    .attr("cx", 100)
    .attr("cy", 100)
    .attr("r", 40)
    .attr("fill", "steelblue");
```

Add a rectangle:

```javascript
svg.append("rect")
    .attr("x", 200)
    .attr("y", 60)
    .attr("width", 120)
    .attr("height", 80)
    .attr("fill", "orange");
```

---

## 4.5 Create Several Circles from Data

Suppose:

```javascript
const values = [10, 20, 30, 40, 50];
```

Create:

```javascript
const svg = d3.select("#svg-demo")
    .append("svg")
    .attr("width", 600)
    .attr("height", 200);
```

Bind the data:

```javascript
svg.selectAll("circle")
    .data(values)
    .join("circle")
    .attr("cx", (d, i) => 60 + i * 100)
    .attr("cy", 100)
    .attr("r", d => d / 2)
    .attr("fill", "steelblue");
```

Here:

```javascript
d
```

represents the current data value.

And:

```javascript
i
```

represents its index.

For example:

```text
d = 10, i = 0
d = 20, i = 1
d = 30, i = 2
...
```

This is your first example of **data-driven graphics**.

---

# Task 5 — Loading CSV and JSON Data

Most real visualizations do not contain the dataset directly inside JavaScript.

Instead, data comes from external files.

D3 can load formats including:

```text
CSV
JSON
TSV
GeoJSON
```

In this lab, we will use CSV and JSON.

---

## 5.1 Create a CSV Dataset

Create:

```text
data/students.csv
```

Add:

```csv
name,score
Alice,85
Bob,72
Carol,91
David,66
Emma,88
Frank,74
Grace,95
```

---

## 5.2 Load CSV Using D3

Use:

```javascript
d3.csv("data/students.csv")
    .then(data => {

        console.log(data);

    });
```

Open Developer Tools.

You should see an array containing student objects.

---

## 5.3 Important: CSV Values Are Initially Strings

Try:

```javascript
d3.csv("data/students.csv")
    .then(data => {

        console.log(data[0]);
        console.log(typeof data[0].score);

    });
```

You may see:

```text
"85"
```

rather than:

```text
85
```

CSV values are normally loaded as strings.

Convert them:

```javascript
d3.csv("data/students.csv")
    .then(data => {

        data.forEach(d => {
            d.score = +d.score;
        });

        console.log(data);

    });
```

The unary `+` converts the string to a number.

Another approach is:

```javascript
d.score = Number(d.score);
```

---

## 5.4 Row Conversion

A cleaner version is:

```javascript
d3.csv("data/students.csv", d => {

    return {
        name: d.name,
        score: +d.score
    };

}).then(data => {

    console.log(data);

});
```

This converts each row while loading it.

---

## 5.5 JSON Data

Create:

```text
data/students.json
```

Add:

```json
[
    {
        "name": "Alice",
        "score": 85
    },
    {
        "name": "Bob",
        "score": 72
    },
    {
        "name": "Carol",
        "score": 91
    }
]
```

Load it using:

```javascript
d3.json("data/students.json")
    .then(data => {

        console.log(data);

    });
```

Unlike CSV, JSON can preserve numeric data types.

---

## 5.6 Using async/await

We will frequently use `async/await` during this course because it makes data-loading code easier to read.

Example:

```javascript
async function loadData() {

    const data = await d3.csv(
        "data/students.csv",
        d => ({
            name: d.name,
            score: +d.score
        })
    );

    console.log(data);

}

loadData();
```

Conceptually:

```text
Request data
     ↓
Wait until data arrives
     ↓
Convert data
     ↓
Use data
```

---

## 5.7 Run a Local Web Server

Loading local files such as CSV or JSON may not work reliably by double-clicking `index.html` because browsers restrict some requests made from `file://` pages.

Instead, run a local web server.

Because Python will be used elsewhere in this course, we can use Python's built-in HTTP server.

Open a terminal inside your project folder:

```bash
cd stats401-labs
```

Run:

```bash
python -m http.server 8000
```

If your system uses `python3`:

```bash
python3 -m http.server 8000
```

Then visit:

```text
http://localhost:8000
```

Stop the server with:

```text
Ctrl + C
```

You should use a local server for all future D3 labs.

---

# Task 6 — Create Navigation for All 10 Labs

Your website will eventually contain all labs from the course.

We will create the navigation structure now so you can extend the same website throughout the semester.

## 6.1 Create the Navigation Bar

Add this near the top of `index.html`:

```html
<nav class="lab-nav">

    <a href="lab1/index.html">Lab 1</a>
    <a href="lab2/index.html">Lab 2</a>
    <a href="lab3/index.html">Lab 3</a>
    <a href="lab4/index.html">Lab 4</a>
    <a href="lab5/index.html">Lab 5</a>
    <a href="lab6/index.html">Lab 6</a>
    <a href="lab7/index.html">Lab 7</a>
    <a href="lab8/index.html">Lab 8</a>
    <a href="lab9/index.html">Lab 9</a>
    <a href="lab10/index.html">Lab 10</a>

</nav>
```

## 6.2 Style the Navigation

Add to `style.css`:

```css
.lab-nav {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin: 30px 0;
    padding-bottom: 15px;
    border-bottom: 1px solid #ddd;
}

.lab-nav a {
    padding: 8px 14px;
    text-decoration: none;
    background: #f1f1f1;
    color: #333;
    border-radius: 5px;
}

.lab-nav a:hover {
    background: #333;
    color: white;
}
```

Your webpage will now contain navigation resembling:

```text
Lab 1 | Lab 2 | Lab 3 | Lab 4 | Lab 5
Lab 6 | Lab 7 | Lab 8 | Lab 9 | Lab 10
```

## 6.3 Create Placeholder Lab Pages

Create:

```text
lab1/index.html
lab2/index.html
...
lab10/index.html
```

For now, a placeholder page can contain:

```html
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <title>Lab 2</title>

</head>

<body>

    <h1>Lab 2</h1>

    <p>
        Lab 2 will be added here.
    </p>

    <a href="../index.html">
        Back to home
    </a>

</body>

</html>
```

Change the lab number for each folder.

---

# Task 7 — Publish Your Website with GitHub Pages

GitHub Pages allows you to publish static HTML, CSS, and JavaScript websites directly from a GitHub repository.

## 7.1 Create a GitHub Repository

Log in to GitHub.

Create a repository named:

```text
stats401-labs
```

## 7.2 Initialize Git Locally

From your project folder:

```bash
git init
```

Add all files:

```bash
git add .
```

Commit:

```bash
git commit -m "Create STATS 401 lab website"
```

Set the main branch:

```bash
git branch -M main
```

Connect your repository:

```bash
git remote add origin https://github.com/YOUR_USERNAME/stats401-labs.git
```

Push:

```bash
git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.

## 7.3 Enable GitHub Pages

Go to:

```text
Repository
→ Settings
→ Pages
```

Under **Build and deployment**:

```text
Source:
Deploy from a branch
```

Select:

```text
Branch: main
Folder: / (root)
```

Save.

Your URL will normally have the form:

```text
https://YOUR_USERNAME.github.io/stats401-labs/
```

## 7.4 Updating Your Website

After making changes locally:

```bash
git add .
git commit -m "Update Lab 1"
git push
```

The workflow becomes:

```text
Edit locally
     ↓
Test locally
     ↓
git add
     ↓
git commit
     ↓
git push
     ↓
GitHub Pages
     ↓
Public website
```

---

# Assignment — My First D3 Visualization

## Objective

Create your first data-driven visualization using D3 and publish it as **Lab 1** on your STATS 401 GitHub Pages website.

The purpose of this assignment is not to create a sophisticated visualization.

Instead, demonstrate that you understand the complete workflow:

```text
HTML
 ↓
CSS
 ↓
JavaScript
 ↓
D3
 ↓
External data
 ↓
SVG
 ↓
GitHub
 ↓
GitHub Pages
```

## Assignment Dataset

Create:

```text
data/students.csv
```

Use at least **8 observations**.

For example:

```csv
name,score
Alice,85
Bob,72
Carol,91
David,66
Emma,88
Frank,74
Grace,95
Henry,82
```

You may use this example dataset or create your own small dataset.

Possible alternatives include:

- movie ratings;
- game scores;
- course enrollment;
- city populations;
- book ratings;
- sports statistics;
- personal activity data;
- music listening counts.

For Lab 1, keep the dataset small.

## Assignment Requirements

Your submission must satisfy the following requirements:

1. Your website must contain `index.html`, `css/`, `js/`, `data/`, and `lab1/` through `lab10/`.
2. Your main webpage must provide navigation to all 10 labs.
3. The visualization must load data from an external `.csv` or `.json` file.
4. You must use D3 to create the visualization.
5. The visualization must use SVG.
6. Graphical marks must be created through D3 data binding.
7. At least one visual property must encode a data variable.
8. The visualization must contain a descriptive title, labels, and interpretable values.
9. CSS must be used to improve readability.
10. The completed visualization must be publicly accessible through GitHub Pages.

---

# Sample Assignment — Student Score Bar Chart

## Step 1 — Dataset

Create:

```text
data/students.csv
```

```csv
name,score
Alice,85
Bob,72
Carol,91
David,66
Emma,88
Frank,74
Grace,95
Henry,82
```

## Step 2 — Lab 1 HTML

Create:

```text
lab1/index.html
```

```html
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <title>Lab 1 - My First D3 Visualization</title>

    <link rel="stylesheet"
          href="../css/style.css">

</head>

<body>

<header>

    <h1>STATS 401</h1>

    <p>Data Acquisition and Visualization</p>

</header>

<nav class="lab-nav">

    <a href="../lab1/index.html">Lab 1</a>
    <a href="../lab2/index.html">Lab 2</a>
    <a href="../lab3/index.html">Lab 3</a>
    <a href="../lab4/index.html">Lab 4</a>
    <a href="../lab5/index.html">Lab 5</a>
    <a href="../lab6/index.html">Lab 6</a>
    <a href="../lab7/index.html">Lab 7</a>
    <a href="../lab8/index.html">Lab 8</a>
    <a href="../lab9/index.html">Lab 9</a>
    <a href="../lab10/index.html">Lab 10</a>

</nav>

<main>

    <h2>Lab 1: My First D3 Visualization</h2>

    <p>
        This visualization shows the scores of
        eight students.
    </p>

    <div id="chart"></div>

</main>

<script src="https://cdn.jsdelivr.net/npm/d3@7"></script>

<script src="lab1.js"></script>

</body>

</html>
```

## Step 3 — JavaScript

Create:

```text
lab1/lab1.js
```

```javascript
const width = 700;
const height = 400;

const margin = {
    top: 30,
    right: 30,
    bottom: 60,
    left: 60
};

d3.csv("../data/students.csv", d => ({
    name: d.name,
    score: +d.score
}))
.then(data => {

    console.log(data);

    const svg = d3.select("#chart")
        .append("svg")
        .attr("width", width)
        .attr("height", height);

    const xScale = d3.scaleBand()
        .domain(data.map(d => d.name))
        .range([
            margin.left,
            width - margin.right
        ])
        .padding(0.2);

    const yScale = d3.scaleLinear()
        .domain([0, 100])
        .range([
            height - margin.bottom,
            margin.top
        ]);

    svg.selectAll("rect")
        .data(data)
        .join("rect")
        .attr("x", d => xScale(d.name))
        .attr("y", d => yScale(d.score))
        .attr("width", xScale.bandwidth())
        .attr(
            "height",
            d => height - margin.bottom - yScale(d.score)
        )
        .attr("fill", "steelblue");

    svg.append("g")
        .attr(
            "transform",
            `translate(0, ${height - margin.bottom})`
        )
        .call(d3.axisBottom(xScale));

    svg.append("g")
        .attr(
            "transform",
            `translate(${margin.left}, 0)`
        )
        .call(d3.axisLeft(yScale));

    svg.selectAll(".value-label")
        .data(data)
        .join("text")
        .attr("class", "value-label")
        .attr(
            "x",
            d => xScale(d.name) +
                 xScale.bandwidth() / 2
        )
        .attr(
            "y",
            d => yScale(d.score) - 8
        )
        .attr("text-anchor", "middle")
        .text(d => d.score);

});
```

## Step 4 — CSS

Add to:

```text
css/style.css
```

```css
body {
    font-family: Arial, sans-serif;
    max-width: 1000px;
    margin: 40px auto;
    padding: 0 20px;
    color: #222;
}

header {
    margin-bottom: 20px;
}

header h1 {
    margin-bottom: 5px;
}

header p {
    color: #666;
}

.lab-nav {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin: 25px 0;
    padding-bottom: 15px;
    border-bottom: 1px solid #ddd;
}

.lab-nav a {
    padding: 8px 14px;
    background: #f1f1f1;
    color: #333;
    text-decoration: none;
    border-radius: 5px;
}

.lab-nav a:hover {
    background: #333;
    color: white;
}

#chart {
    margin-top: 30px;
    overflow-x: auto;
}

svg {
    background: #fafafa;
    border: 1px solid #eee;
}

.value-label {
    font-size: 12px;
    font-weight: bold;
}
```

---

# Challenge Exercises

If you finish early, try one or more of the following.

## Challenge 1

Change the dataset.

## Challenge 2

Change the bar color based on score.

```javascript
.attr("fill", d => {

    if (d.score >= 90) {
        return "green";
    }

    return "steelblue";

});
```

## Challenge 3

Make the bars respond to the mouse.

```javascript
.on("mouseover", function() {

    d3.select(this)
        .attr("opacity", 0.6);

})
.on("mouseout", function() {

    d3.select(this)
        .attr("opacity", 1);

});
```

## Challenge 4

Automatically determine the maximum score.

Instead of:

```javascript
.domain([0, 100])
```

try:

```javascript
.domain([
    0,
    d3.max(data, d => d.score)
])
```

---

# Debugging Guide

## Problem 1 — Nothing Appears

Open:

```text
Developer Tools → Console
```

Look for errors.

A JavaScript error can prevent the remainder of the visualization from running.

## Problem 2 — `d3 is not defined`

Check that:

```html
<script src="https://cdn.jsdelivr.net/npm/d3@7"></script>
```

appears before:

```html
<script src="lab1.js"></script>
```

## Problem 3 — CSV Does Not Load

Run:

```bash
python -m http.server 8000
```

and visit:

```text
http://localhost:8000
```

Also verify the relative path.

For a structure like:

```text
data/
    students.csv

lab1/
    index.html
    lab1.js
```

the correct path from `lab1.js` is:

```javascript
"../data/students.csv"
```

## Problem 4 — GitHub Page Shows 404

Check:

```text
Settings
→ Pages
```

and confirm:

```text
main
/
```

is configured as the publishing source.

Also make sure the repository contains:

```text
index.html
```

## Problem 5 — Works Locally but Not on GitHub

File names on GitHub Pages are case-sensitive.

For example:

```text
students.csv
```

is different from:

```text
Students.csv
```

Keep filenames lowercase to avoid these problems.

---

# Submission Requirements

Submit the following through the course LMS.

## 1. GitHub Repository URL

Example:

```text
https://github.com/username/stats401-labs
```

## 2. GitHub Pages URL

Example:

```text
https://username.github.io/stats401-labs/
```

## 3. Direct Lab 1 URL

Example:

```text
https://username.github.io/stats401-labs/lab1/
```

---

# Submission Checklist

- [ ] My website opens successfully.
- [ ] My website contains navigation for all 10 labs.
- [ ] Lab 1 opens from the navigation menu.
- [ ] Labs 2–10 have working placeholder pages.
- [ ] My visualization uses D3.js.
- [ ] My visualization uses SVG.
- [ ] My data comes from an external CSV or JSON file.
- [ ] My dataset contains at least 8 observations.
- [ ] My code converts numeric CSV values to numbers.
- [ ] I use D3 data binding to create graphical marks.
- [ ] My visualization has a title.
- [ ] Categories or observations are labeled.
- [ ] Data values can be interpreted from the visualization.
- [ ] My CSS improves the page's readability.
- [ ] There are no major JavaScript errors in the browser console.
- [ ] The visualization works through GitHub Pages.
- [ ] I submitted both the repository URL and published URL.

---

# What You Learned

In this lab you completed the entire basic D3 workflow:

```text
HTML
  │
  ├── defines page structure
  │
CSS
  │
  ├── controls appearance
  │
JavaScript
  │
  ├── controls behavior
  │
D3.js
  │
  ├── binds data to DOM elements
  ├── loads external data
  └── creates SVG graphics
  │
CSV / JSON
  │
  └── provides external data
  │
Git + GitHub
  │
  └── stores and versions code
  │
GitHub Pages
  │
  └── publishes the visualization
```

This infrastructure will be reused throughout the rest of the course.

In later labs, we will keep the same website but progressively add:

```text
Lab 1   D3 foundations
Lab 2   Multivariate visualization
Lab 3   Web data acquisition
Lab 4   Data cleaning
Lab 5   Network visualization
Lab 6   Temporal visualization
Lab 7   Hierarchical visualization
Lab 8   Text visualization
Lab 9   Geographic visualization
Lab 10  Interaction and coordinated views
```

By the end of the course, the website will serve as a portfolio containing all of your data acquisition and visualization work.
