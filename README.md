<!DOCTYPE html>
<html>
<head>
    <title>Location Tracker</title>
</head>
<body>
    <h1>Location Tracker</h1>
    <button onclick="getLocation()">Share My Location</button>
    <p id="status"></p>
    <script>
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(showPosition, showError);
                document.getElementById('status').innerText = "Requesting location...";
            } else {
                document.getElementById('status').innerText = "Geolocation is not supported by this browser.";
            }
        }

        function showPosition(position) {
            const lat = position.coords.latitude;
            const lon = position.coords.longitude;
            document.getElementById('status').innerText = `Latitude: ${lat}, Longitude: ${lon}`;
            // Optionally send to your server:
            // fetch('https://yourserver.com/track', {
            //     method: 'POST',
            //     headers: {'Content-Type': 'application/json'},
            //     body: JSON.stringify({latitude: lat, longitude: lon})
            // });
        }

        function showError(error) {
            switch(error.code) {
                case error.PERMISSION_DENIED:
                    document.getElementById('status').innerText = "User denied the request for Geolocation.";
                    break;
                case error.POSITION_UNAVAILABLE:
                    document.getElementById('status').innerText = "Location information is unavailable.";
                    break;
                case error.TIMEOUT:
                    document.getElementById('status').innerText = "The request to get user location timed out.";
                    break;
                default:
                    document.getElementById('status').innerText = "An unknown error occurred.";
                    break;
            }
        }
    </script>
</body>
</html>
