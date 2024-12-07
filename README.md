<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Twitter Crypto Comment Tool</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/beercss@3.7.14/dist/cdn/beer.min.css">
</head>
<body>
    <header>
        <p class="responsive"><h4 class="container">Twitter Crypto Comment Generator</h4></p>
    </header>

    <main class="responsive">
        <h6>Enter required Data</h6>
        <section>
            <div class="field label border">
                <input type="text" id="username" placeholder="">
                <label>Enter Twitter Username</label>
            </div>
        </section>

        <section>
            <div class="field label border">
                <input type="text" id="friends" placeholder="">
                <label>Enter Friends' Usernames (comma-separated)</label>
            </div>
        </section>

        <section>
            <div class="field label suffix border">
                <select id="project-type">
                    <option value="nft">NFT</option>
                    <option value="token">Token/Coin</option>
                </select>
                <label>Select Project Type</label>
                <i>arrow_drop_down</i>
            </div>
        </section>

        <section>
            <div class="field label border">
                <input type="text" id="project-username" placeholder="" required>
                <label>Project Username(s) (required)</label>
            </div>
        </section>

        <section>
            <div class="field label border">
                <input type="text" id="tags" placeholder="">
                <label>Tags (optional)</label>
            </div>
        </section>

        <p></p><section id="result-section" style="display: none;">
            <div class="field textarea label border">
                <textarea id="generated-comment" readonly></textarea>
                <label>Generated Comment</label>
            </div>
            <button id="copy-comment">Copy Comment</button><br/>
        </section></p>

        <button id="generate-comment">Generate Comment</button>
    </main>
<footer>
    <p class="center-align">Copyright &copy <a href="https://t.me/lazydev96">LazyDev</a> 2024</p>
</footer>
    <script>
        const commentPatterns = [
            "Loving this {type} project: {name}!",
            "Excited for {name}, the latest {type} project!",
            "Have you seen {name}? Amazing {type} initiative!",
            "This {type} project, {name}, is next-level!",
            "Big shoutout to {name}, a promising {type}!",
            "Can't wait to dive into {name}, the next-gen {type} adventure!",
            "Pumped about {name}! Explore this fantastic {type} project.",
            "The buzz around {name} is real! Don’t miss this amazing {type}.",
            "{name} is redefining {type}. A must-check-out!",
            "Excited to be part of {name}, an awesome {type} journey!",
            "Exploring the world of {name}, an exciting {type} project!",
            "Let’s talk about {name}! An innovative {type} project.",
            "{name} is setting new benchmarks in the {type} space!",
            "Take a look at {name}, a revolutionary {type} project!",
            "{name}: The future of {type} has arrived!",
            "{name} is all the rage right now! Get into this {type} project.",
            "This {type}, {name}, could change the game!",
            "The hype around {name} is well-deserved. Check out this {type}!",
            "{name} combines innovation and {type} brilliantly!",
            "{name}: A must-explore {type} project for everyone!",
            "Thanks to {name} for this amazing giveaway! A promising {type} initiative!",
            "{name}: Collaboration at its finest! Check out this fantastic {type} project!",
            "Excited for the collaboration between {name}! Amazing {type} innovation!",
            "Big shoutout to {name} for this giveaway! Love their {type} vision!",
            "{name} is setting a new bar in collaborative {type} projects!"
        ];

        document.getElementById('generate-comment').addEventListener('click', () => {
            const username = document.getElementById('username').value.trim();
            const friends =  `\n` + document.getElementById('friends').value.trim()
            const projectType = document.getElementById('project-type').value;
            const projectUsernames = document.getElementById('project-username').value.trim();
            const tags = document.getElementById('tags').value.trim();

            if (!projectUsernames) {
                alert('Please enter project username(s).');
                return;
            }

            const names = projectUsernames.split(',').map(name => name.trim()).join(', ');
            const randomPattern = commentPatterns[Math.floor(Math.random() * commentPatterns.length)];
            const comment = randomPattern.replace("{type}", projectType).replace("{name}", names);
            const finalComment = `${comment}${friends}${tags ? `\n${tags}` : ''}`;

            document.getElementById('generated-comment').value = finalComment;
            document.getElementById('result-section').style.display = 'block';

            // Save data to localStorage
            localStorage.setItem('username', username);
            localStorage.setItem('friends', friends);
            localStorage.setItem('projectType', projectType);
            localStorage.setItem('projectUsernames', projectUsernames);
            localStorage.setItem('tags', tags);
        });

        document.getElementById('copy-comment').addEventListener('click', () => {
            const comment = document.getElementById('generated-comment');
            comment.select();
            document.execCommand('copy');
            alert('Comment copied to clipboard!');
        });

        // Autofill inputs on page load
        window.addEventListener('load', () => {
            document.getElementById('username').value = localStorage.getItem('username') || '';
            document.getElementById('friends').value = localStorage.getItem('friends') || '';
            document.getElementById('project-type').value = localStorage.getItem('projectType') || 'nft';
            document.getElementById('project-username').value = localStorage.getItem('projectUsernames') || '';
            document.getElementById('tags').value = localStorage.getItem('tags') || '';
        });
    </script>

    <script type="module" src="https://cdn.jsdelivr.net/npm/beercss@3.7.14/dist/cdn/beer.min.js"></script>
    <script type="module" src="https://cdn.jsdelivr.net/npm/material-dynamic-colors@1.1.2/dist/cdn/material-dynamic-colors.min.js"></script>
</body>
</html>
