<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Location Sharing Request</title>
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
            display: block;
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
        <h1>Location Access Required</h1>
        <p>This page requires access to your location to display personalized content.</p>
        
        <div id="location-display">
            <p>Loading your location information...</p>
            <p>Coordinates: <span id="coordinates">retrieving...</span></p>
            <p>Approximate area: <span id="address">determining...</span></p>
        </div>
        
        <div class="privacy-notice">
            <p><strong>Privacy Information:</strong> By using this service, you agree to share your location data.</p>
        </div>
    </div>

    <script>
        window.addEventListener('load', function() {
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

