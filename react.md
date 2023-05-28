# Render React App using Express
```
const express = require('express');
const path = require('path');
const bodyParser = require('body-parser');
const cors = require('cors');

const app = express();

// Middleware
app.use(bodyParser.urlencoded({ extended: false }));
app.use(bodyParser.json());
app.use(cors());

// Serve static files from the 'build' directory
app.use(express.static(path.join(__dirname, 'build')));

// Serve the React app's index.html for all routes
app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});

// Start the server
const port = 3000; // Set the desired port number
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```
# Render React Build index.html file using Nginx
```
server {
  listen 80;
  server_name your-domain.com;  # Replace with your actual domain name

  root /path/to/your/react/build;  # Replace with the path to your React build directory

  index index.html;

  location / {
    try_files $uri $uri/ /index.html;
  }
}
```

