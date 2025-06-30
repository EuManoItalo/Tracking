<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Share Your Location</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            text-align: center;
        }
        .container {
            background: #f5f5f5;
            border-radius: 10px;
            padding: 30px;
            margin-top: 50px;
        }
        button {
            background: #4285f4;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            margin: 20px 0;
        }
        #location-display {
            margin-top: 20px;
            padding: 15px;
            background: white;
            border-radius: 5px;
            display: none;
        }
        .privacy-notice {
            font-size: 14px;
            color: #666;
            margin-top: 30px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Share Your Location</h1>
        <p>This service requires your explicit permission to access your location. The location data will only be used for the purpose you request.</p>
        
        <button id="share-btn">Share My Location</button>
        
        <div id="location-display">
            <p>Your location: <span id="coordinates"></span></p>
            <p>Approximate address: <span id="address"></span></p>
        </div>
        
        <div class="privacy-notice">
            <p><strong>Privacy Notice:</strong> Your location will only be shared after you click the button above and grant permission. This website does not store your location data.</p>
        </div>
    </div>

    <script>
        document.getElementById('share-btn').addEventListener('click', function() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    function(position) {
                        const latitude = position.coords.latitude;
                        const longitude = position.coords.longitude;
                        
                        document.getElementById('coordinates').textContent = 
                            `${latitude.toFixed(4)}, ${longitude.toFixed(4)}`;
                        
                        // Using geocoding to get approximate address (would need a proper service for production)
                        document.getElementById('address').textContent = 
                            getApproximateAddress(latitude, longitude);
                        
                        document.getElementById('location-display').style.display = 'block';
                    },
                    function(error) {
                        alert('Error getting location: ' + error.message);
                    },
                    { 
                        enableHighAccuracy: true,
                        timeout: 5000,
                        maximumAge: 0
                    }
                );
            } else {
                alert('Geolocation is not supported by this browser.');
            }
        });

        function getApproximateAddress(lat, lng) {
            // Note: In a real application, you would call a geocoding service API here
            return "Location services would convert coordinates to address";
        }
    </script>
</body>
</html>

