<html lang="en">
<head>
    <title>Leaderboard</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
<style>
    * {
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }
    h1 {
        font-size: 32pt;
        text-align: center;
        margin-top: 40px;
        color: white; /* Make header text white */
    }
    body {
        background-color: #333; /* Dark background to contrast with white text */
        color: white; /* Default text color set to white */
    }
    table.board {
        font-size: 13pt;
        border-collapse: collapse;
        margin: 25px auto; /* Center the table */
        width: 90%;
    }
    .board thead tr {
        background-color: #f1cc0c;
        color: #000; /* Keep header row text black for contrast */
    }
    .board th, .board td { /* Added th for consistency */
        text-align: center;
        padding: 12px 15px;
        color: white; /* Make table text white */
    }
    .board tbody tr:nth-of-type(even) {
        background-color: #333;
        color: white; /* Ensure text color is white for contrast */
    }
    .board tbody tr:hover {
        color: #f1cc0c;
        background-color: #5c5c5c;
    }
    #container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
</style>
</head>
<body>

<div id="container">
    <h1>Leaderboard!</h1>

    <table class="board">
        <thead>
            <tr>
                <th>Rank</th>
                <th>Name</th>
                <th>Score</th>
            </tr>
        </thead>
        <tbody id="tbody"></tbody>
    </table>
</div>

<script>
async function sort() {
    try {
        const response = await fetch('https://ajarcade.duckdns.org/api/players/');
        const unsortedDB = await response.json();
        console.log(unsortedDB);

        // Sorts the db by token amount in descending order
        const sortedDB = unsortedDB.sort((a, b) => b.tokens - a.tokens);
        console.log(sortedDB);

        // Fill the table with sorted db info
        tableFill(sortedDB);
    } catch (error) {
        console.error('Failed to fetch leaderboard data:', error);
    }
}

function tableFill(db) {
    const tbody = document.getElementById('tbody');
    db.forEach((player, index) => {
        let tr = document.createElement('tr');
        tr.innerHTML = `<td>${index + 1}</td><td>${player.name}</td><td>${player.tokens}</td>`;
        tbody.appendChild(tr);
    });
}

document.addEventListener('DOMContentLoaded', sort);
</script>
</body>
</html>