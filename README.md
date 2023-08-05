# ValidatingZuzu.Git.Hub.io
<!DOCTYPE html>
<html>
<head>
    <title>OAuth URLs and Data Deletion</title>
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
