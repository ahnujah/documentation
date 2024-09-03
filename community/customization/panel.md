<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Building Panel Assets</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 20px;
        }
        h1, h2 {
            color: #2c3e50;
        }
        h1 {
            text-align: center;
        }
        h2 {
            margin-top: 40px;
        }
        p {
            margin-bottom: 20px;
        }
        .warning {
            background-color: #f8d7da;
            color: #721c24;
            padding: 15px;
            border-left: 6px solid #f5c6cb;
            margin-bottom: 20px;
        }
        .code-block {
            position: relative;
            background-color: #272822;
            color: #f8f8f2;
            padding: 15px;
            border-radius: 5px;
            font-family: 'Courier New', Courier, monospace;
            margin-bottom: 20px;
            overflow: auto;
        }
        .copy-button {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: #2c3e50;
            color: #fff;
            border: none;
            padding: 5px 10px;
            cursor: pointer;
            border-radius: 3px;
            font-size: 12px;
        }
        .copy-button:hover {
            background-color: #34495e;
        }
        .note {
            background-color: #e2e3e5;
            color: #383d41;
            padding: 10px;
            border-left: 6px solid #d6d8db;
            margin-bottom: 20px;
        }
    </style>
</head>
<body>

    <h1>Building Panel Assets</h1>

    <div class="warning">
        <strong>Warning:</strong> Do <strong>not</strong> run the following steps on your production nodes.
    </div>

    <p>Instructions on how to build the panel are also available in the <a href="https://github.com/pterodactyl/panel/blob/1.0-develop/BUILDING.md" target="_blank">BUILDING.md</a> file.</p>
    
    <p>The frontend of the Panel is built with React. Any changes to the source files require recompiling it. This also applies to style sheets. The following sections explain how to do so.</p>

    <h2>Install Dependencies</h2>

    <p>The following commands will install the necessary dependencies for building the Panel assets. The build tools require NodeJS, and Yarn is used as the package manager.</p>

    <div class="code-block">
        <button class="copy-button" onclick="copyToClipboard(this)">Copy</button>
        <p><strong>For Ubuntu/Debian:</strong></p>
        <code id="code1">
        curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -<br>
        sudo apt install -y nodejs
        </code>

        <p><strong>For CentOS:</strong></p>
        <code id="code2">
        curl -sL https://rpm.nodesource.com/setup_16.x | sudo -E bash -<br>
        sudo yum install -y nodejs yarn # CentOS 7<br>
        sudo dnf install -y nodejs yarn # CentOS 8, Rocky Linux 8, AlmaLinux 8
        </code>
    </div>

    <p>Once NodeJS is installed, you can install the required JavaScript packages:</p>

    <div class="code-block">
        <button class="copy-button" onclick="copyToClipboard(this)">Copy</button>
        <code id="code3">
        npm i -g yarn # Install Yarn<br><br>

        cd /var/www/pterodactyl<br>
        yarn # Installs panel build dependencies
        </code>
    </div>

    <h2>Build Panel Assets</h2>

    <p>The following command will rebuild the Panel frontend. For NodeJS version 17 and above, you must enable the <code>--openssl-legacy-provider</code> option before building:</p>

    <div class="code-block">
        <button class="copy-button" onclick="copyToClipboard(this)">Copy</button>
        <code id="code4">
        cd /var/www/pterodactyl<br>
        export NODE_OPTIONS=--openssl-legacy-provider # for NodeJS v17+<br>
        yarn build:production # Build panel
        </code>
    </div>

    <div class="note">
        <strong>Note:</strong> You can use the command <code>yarn run watch</code> to view the progress of your changes in almost real-time for easier development. Once you're satisfied with your changes, build the panel using the <code>yarn build:production</code> command mentioned above.
    </div>

    <script>
        function copyToClipboard(button) {
            const codeBlock = button.nextElementSibling;
            const range = document.createRange();
            range.selectNode(codeBlock);
            window.getSelection().removeAllRanges(); // Clear existing selections
            window.getSelection().addRange(range);

            try {
                document.execCommand('copy');
                button.textContent = 'Copied!';
                setTimeout(() => button.textContent = 'Copy', 2000);
            } catch (err) {
                button.textContent = 'Error';
            }

            window.getSelection().removeAllRanges(); // Clear selections after copying
        }
    </script>

</body>
</html>
