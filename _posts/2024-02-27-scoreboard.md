---
layout: default
permalink: /scoreboard
title: Scoreboard
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Leaderboard</title>
</head>
<body>
    <h2>Leaderboard</h2>
    <table id="leaderboard">
        <thead>
            <tr>
                <th>Name</th>
                <th>Score</th>
            </tr>
        </thead>
        <tbody>
            <!-- Leaderboard entries will be inserted here -->
        </tbody>
    </table>
    <script>
        fetch('/leaderboard')
            .then(response => response.json())
            .then(data => {
                const leaderboardTable = document.getElementById('leaderboard').getElementsByTagName('tbody')[0];
                data.forEach(user => {
                    const row = leaderboardTable.insertRow();
                    const nameCell = row.insertCell(0);
                    const scoreCell = row.insertCell(1);
                    nameCell.textContent = user.name;
                    scoreCell.textContent = user.score;
                });
            })
            .catch(error => console.error('Failed to fetch leaderboard data:', error));
    </script>
</body>
</html>

