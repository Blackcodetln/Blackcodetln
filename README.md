- # Creating the requested HTML page with JavaScript functionality
html_content = '''<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Black-code Selection</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: black;
            color: white;
            overflow: hidden;
            position: relative;
            text-align: center;
        }

        #name, #code {
            display: none;
            margin: 20px;
            padding: 10px;
            font-size: 20px;
            border: 1px solid white;
            background-color: transparent;
            color: white;
        }

        #submit {
            padding: 10px 20px;
            font-size: 20px;
            background-color: transparent;
            color: white;
            border: 2px solid white;
            cursor: pointer;
        }

        #wheel {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
        }

        #wheel-content {
            font-size: 30px;
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .number-run {
            position: absolute;
            font-size: 20px;
            color: white;
            white-space: nowrap;
            animation: move 15s infinite linear;
        }

        @keyframes move {
            0% { transform: translateY(0); }
            100% { transform: translateY(-100%); }
        }

        #result {
            display: none;
            margin-top: 20px;
            font-size: 24px;
            background-color: rgba(255, 255, 255, 0.1);
            padding: 20px;
        }

        #black-code {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 50px;
            color: white;
        }
    </style>
</head>
<body>
    <div id="black-code">Black-code</div>
    <input type="text" id="name" placeholder="Enter Name" required>
    <input type="text" id="code" placeholder="Enter Code" required>
    <button id="submit">Submit</button>

    <div id="wheel">
        <div id="wheel-content"></div>
    </div>

    <div id="result"></div>

    <script>
        let participants = [];

        document.getElementById('submit').onclick = function() {
            const name = document.getElementById('name').value;
            const code = document.getElementById('code').value;
            if (name && code) {
                participants.push({ name, code });
                document.getElementById('name').value = '';
                document.getElementById('code').value = '';
            }
        }

        const showWheel = () => {
            const wheel = document.getElementById('wheel');
            const wheelContent = document.getElementById('wheel-content');
            wheel.style.display = 'flex';
            wheelContent.innerHTML = participants.map(p => p.name + ' - ' + p.code).join('<br>');
            setTimeout(selectRandom, 15000);
        }

        const selectRandom = () => {
            const randomIndex = Math.floor(Math.random() * participants.length);
            const selected = participants[randomIndex];
            const message = 'Black-code [ TLN ] : ' + selected.name + ' ' + selected.code + ' đã bị phát hiện [ thực thi mã đen ]';
            document.getElementById('result').innerText = message;
            document.getElementById('result').style.display = 'block';
            document.getElementById('wheel').style.display = 'none';

            setTimeout(() => {
                resetForm();
            }, 120000); // Reset after 2 minutes
        }

        const resetForm = () => {
            document.getElementById('result').style.display = 'none';
            document.getElementById('name').style.display = 'block';
            document.getElementById('code').style.display = 'block';
            document.getElementById('submit').style.display = 'block';
            participants = [];
            document.getElementById('black-code').style.display = 'block';
        }

        setInterval(() => {
            const numDiv = document.createElement('div');
            numDiv.className = 'number-run';
            numDiv.innerText = Math.floor(Math.random() * 10000);
            numDiv.style.top = Math.random() * 100 + 'vh';
            numDiv.style.left = Math.random() * 100 + 'vw';
            document.body.appendChild(numDiv);
            setTimeout(() => numDiv.remove(), 15000); // Remove after 15 seconds
        }, 1000); // Create new number every second

        document.getElementById('name').style.display = 'block';
        document.getElementById('code').style.display = 'block';
        document.getElementById('submit').style.display = 'block';

        setInterval(showWheel, 30000); // Show wheel every 30 seconds
    </script>
</body>
</html>
'''

# Save the created HTML content to a file
web_page_path = "/mnt/data/black_code_selection.html"
with open(web_page_path, 'w') as file:
    file.write(html_content)

web_page_path
