<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Content Protection Example</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            overflow: hidden; /* Prevent scrollbars during overlay display */
        }

        .content {
            position: relative;
            padding: 20px;
            background: #f4f4f4;
            z-index: 1;
        }

        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255, 255, 255, 0.7); /* Slightly more opaque overlay */
            pointer-events: none; /* Allows interaction with underlying content */
            z-index: 10; /* Ensure the overlay is on top */
            display: none; /* Initially hidden */
            transition: opacity 0.5s ease-in-out; /* Smooth transition */
        }
    </style>
</head>
<body>
    <div class="content">
        <h1>Sensitive Content</h1>
        <p>This is an example of content that you may want to protect from screenshots.</p>
        <div class="overlay" id="overlay"></div>
    </div>

    <script>
        function showOverlay() {
            const overlay = document.getElementById('overlay');
            overlay.style.display = 'block';
            overlay.style.opacity = '1';
        }

        function hideOverlay() {
            const overlay = document.getElementById('overlay');
            overlay.style.opacity = '0';
            setTimeout(() => {
                overlay.style.display = 'none';
            }, 500); // Match the transition duration
        }

        document.addEventListener('keydown', function(event) {
            if (event.key === 'PrintScreen') {
                showOverlay();
                setTimeout(hideOverlay, 3000);
            }
        });

        document.addEventListener('visibilitychange', function() {
            if (document.hidden) {
                showOverlay();
                setTimeout(hideOverlay, 3000);
            }
        });

        document.addEventListener('mousemove', function(event) {
            if (event.clientY < 10) {
                showOverlay();
                setTimeout(hideOverlay, 3000);
            }
        });
    </script>
</body>
</html>
