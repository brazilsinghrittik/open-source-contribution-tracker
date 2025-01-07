# Open Source Contribution Tracker

This project is a simple web application that helps track GitHub contributions for any given GitHub username. It fetches data from the GitHub API and displays the number of contributions made by the user to their repositories.

## Features

- User-friendly interface
- Fetches and displays the number of contributions for each repository of a GitHub user
- Uses the GitHub API to retrieve data

## Getting Started

### Prerequisites

To run this project, you need a web browser and an internet connection.

### Running the Application

1. Clone the repository or download the HTML file.
2. Open the HTML file (`index.html`) in a web browser.
3. Enter any GitHub username in the input field.
4. Click on the "Fetch Contributions" button to see the contributions for the specified user.

## Example Usage

1. Open the application in your browser.
2. Enter a GitHub username (e.g., `octocat`).
3. Click the "Fetch Contributions" button.
4. The application will display the number of contributions for each repository of the specified user.

## Code Explanation

The following is the HTML and JavaScript code for the Open Source Contribution Tracker:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Open Source Contribution Tracker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
        }
        .container {
            text-align: center;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        input {
            padding: 10px;
            margin: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #007bff;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background: #e9e9e9;
            margin: 5px 0;
            padding: 10px;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Track GitHub's User Contribution</h1>
        <h3>Write Any GitHub Username</h3>
        <input type="text" id="username" placeholder="GitHub Username">
        <button onclick="fetchContributions()">Fetch Contributions</button>
        <ul id="contributions"></ul>
    </div>
    <script>
        async function fetchContributions() {
            const username = document.getElementById('username').value;
            const contributionsList = document.getElementById('contributions');
            contributionsList.innerHTML = '';

            try {
                const response = await fetch(`https://api.github.com/users/${username}/repos`);
                const repos = await response.json();

                for (const repo of repos) {
                    const repoName = repo.name;
                    const contributionsResponse = await fetch(`https://api.github.com/repos/${username}/${repoName}/contributors`);
                    const contributors = await contributionsResponse.json();

                    const userContribution = contributors.find(contributor => contributor.login === username);
                    const contributions = userContribution ? userContribution.contributions : 0;

                    const listItem = document.createElement('li');
                    listItem.textContent = `${repoName}: ${contributions} contributions`;
                    contributionsList.appendChild(listItem);
                }
            } catch (error) {
                console.error('Error fetching contributions:', error);
            }
        }
    </script>
</body>
</html>****
