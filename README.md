<!DOCTYPE html>
<html>
<head>
    <title>OAuth URLs and Data Deletion</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f9f9f9;
            margin: 0;
            padding: 0;
        }

        h1 {
            color: #333;
            font-size: 36px;
            text-align: center;
            margin-top: 40px;
            margin-bottom: 30px;
        }

        #urlForm {
            max-width: 400px;
            margin: 0 auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        label {
            color: #333;
            font-size: 18px;
            margin-bottom: 5px;
        }

        input {
            display: block;
            width: 100%;
            padding: 8px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 4px;
            margin-bottom: 15px;
        }

        button {
            display: block;
            background-color: #007bff;
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            margin: 0 auto;
        }

        #deauthUrl, #dataDeletionUrl {
            color: #333;
            font-size: 16px;
            font-weight: bold;
            margin-top: 15px;
        }

        #deauthUrl:before, #dataDeletionUrl:before {
            content: '- ';
        }

        p {
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>OAuth URLs and Data Deletion</h1>
    <form id="urlForm">
        <label for="authUrl">Valid OAuth URL:</label>
        <input type="url" id="authUrl" name="authUrl" placeholder="Enter valid OAuth URL" required>
        <label for="redirectUrls">Valid OAuth Redirect URLs (comma-separated):</label>
        <input type="text" id="redirectUrls" name="redirectUrls" placeholder="Enter valid OAuth Redirect URLs" required>
        <button type="submit">Submit</button>
    </form>
    <p>Deauthorize Callback URL: <span id="deauthUrl">Not provided</span></p>
    <p>Data Deletion Request URL: <span id="dataDeletionUrl">Not provided</span></p>

    <script>
        const form = document.getElementById('urlForm');
        const deauthUrlSpan = document.getElementById('deauthUrl');
        const dataDeletionUrlSpan = document.getElementById('dataDeletionUrl');

        form.addEventListener('submit', function(event) {
            event.preventDefault();
            const authUrl = document.getElementById('authUrl').value;
            const redirectUrls = document.getElementById('redirectUrls').value;
            // You can validate the OAuth URL and Redirect URLs here before displaying them
            // For example, you can split the redirectUrls into an array and add each URL separately
            const redirectUrlsArray = redirectUrls.split(',');
            let deauthUrl = authUrl + "/deauthorize_callback";
            let dataDeletionUrl = authUrl + "/data_deletion_request";
            if (redirectUrlsArray.length > 0) {
                deauthUrl += "?redirect_urls=" + redirectUrlsArray.join(',');
                dataDeletionUrl += "?redirect_urls=" + redirectUrlsArray.join(',');
            }
            deauthUrlSpan.textContent = deauthUrl;
            dataDeletionUrlSpan.textContent = dataDeletionUrl;
        });
    </script>
</body>
</html>
