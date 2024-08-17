  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minecraft Color Code Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #2c2f33;
            color: #ffffff;
            text-align: center;
            padding: 20px;
        }
        input, select, button {
            padding: 10px;
            margin: 10px;
            border-radius: 5px;
            border: none;
        }
        .output {
            margin-top: 20px;
            padding: 10px;
            background-color: #23272a;
            border-radius: 5px;
            text-align: left;
        }
        .output span, .output code {
            font-size: 20px;
            white-space: nowrap;
        }
        .output code {
            background-color: #1e1e1e;
            padding: 5px;
            border-radius: 5px;
            display: block;
            color: #00ff00;
            white-space: pre-wrap;
        }
        .obfuscated {
            animation: obfuscate 1s infinite;
        }
        @keyframes obfuscate {
            0% { opacity: 1; }
            50% { opacity: 0.1; }
            100% { opacity: 1; }
        }
    </style>
</head>
<body>
    <h1>Minecraft Color Code Generator</h1>
    
    <label for="text">Enter Text:</label>
    <input type="text" id="text" placeholder="Type your text here">
    
    <label for="color">Choose Color:</label>
    <select id="color">
        <option value="red">Red</option>
        <option value="blue">Blue</option>
        <option value="green">Green</option>
        <option value="dark_gray">Dark Gray</option>
        <option value="light_purple">Light Purple</option>
        <option value="yellow">Yellow</option>
        <option value="white">White</option>
        <option value="dark_blue">Dark Blue</option>
        <option value="dark_purple">Dark Purple</option>
        <option value="gold">Gold</option>
        <option value="aqua">Aqua</option>
        <option value="gray">Gray</option>
        <option value="dark_green">Dark Green</option>
        <option value="dark_aqua">Dark Aqua</option>
        <option value="black">Black</option>
        <option value="rainbow">Rainbow</option>
    </select>

    <label for="styles">Choose Styles:</label>
    <select id="styles" multiple>
        <option value="bold">Bold</option>
        <option value="italic">Italic</option>
        <option value="underline">Underline</option>
        <option value="strikethrough">Strikethrough</option>
        <option value="obfuscated">Obfuscated</option>
    </select>

    <button onclick="addText()">Add Text</button>
    
    <button onclick="clearText()">Clear Text</button>

    <div class="output">
        <h2>Formatted Text</h2>
        <span id="formattedText"></span>
    </div>

    <div class="output">
        <h2>HTML Code</h2>
        <code id="htmlCode"></code>
    </div>

    <script>
        function addText() {
            const text = document.getElementById('text').value;
            const color = document.getElementById('color').value;
            const styles = Array.from(document.getElementById('styles').selectedOptions).map(option => option.value);
            let formattedText = document.getElementById('formattedText').innerHTML;
            let htmlCode = document.getElementById('htmlCode').innerText;

            let styleTags = '';
            let closingTags = '';
            
            styles.forEach(style => {
                switch(style) {
                    case 'bold':
                        styleTags += '<b>';
                        closingTags = '</b>' + closingTags;
                        break;
                    case 'italic':
                        styleTags += '<i>';
                        closingTags = '</i>' + closingTags;
                        break;
                    case 'underline':
                        styleTags += '<underlined>';
                        closingTags = '</underlined>' + closingTags;
                        break;
                    case 'strikethrough':
                        styleTags += '<st>';
                        closingTags = '</st>' + closingTags;
                        break;
                    case 'obfuscated':
                        styleTags += '<obf>';
                        closingTags = '</obf>' + closingTags;
                        break;
                }
            });

            let newText;
            if (color === 'rainbow') {
                newText = `<rainbow>${styleTags}${text}${closingTags}</rainbow>`;
            } else {
                newText = `${styleTags}<${color}>${text}</${color}>${closingTags}`;
            }

            // Append new formatted text
            formattedText += newText + ' ';
            htmlCode += newText;

            document.getElementById('formattedText').innerHTML = formattedText;
            document.getElementById('htmlCode').innerText = htmlCode;
            document.getElementById('text').value = ''; // Clear input after adding
        }

        function clearText() {
            document.getElementById('formattedText').innerHTML = '';
            document.getElementById('htmlCode').innerText = '';
        }
    </script>
</body>
</html>

