If you want to embed your Next.js project using a **single `<script>` tag** that also passes an ID, the solution would involve creating a script that:
- Embeds itself in the host HTML using a single `<script>` tag.
- Fetches an ID from the script tag's attributes.
- Renders a React component using this ID.

The approach involves bundling the script in a way that it handles rendering and parameter passing within the same bundle.

### Steps to Achieve This:

1. **Create a JavaScript Bundle in Your Separate Project**:
   - Modify your Webpack configuration to produce a script that can be used directly in the browser.

2. **Bundle Your Script with Webpack**:
   Create a Webpack configuration to build a JavaScript file that will:
   - Fetch the ID from the script tag’s attributes.
   - Render your React component using this ID.

3. **Expose a Function that Auto-Executes**:
   When the script loads, it should automatically fetch the attributes and mount the Next.js component.

### Step 1: Create a Webpack Configuration

**webpack.config.js**:

```javascript
const path = require('path');

module.exports = {
  entry: './src/index.js', // Entry point for your project
  output: {
    filename: 'embedded-next-project.js', // Output bundle file name
    path: path.resolve(__dirname, 'dist'),
    library: 'EmbeddedNextProject', // Global variable name (optional)
    libraryTarget: 'umd', // Allows the bundle to be loaded in various module systems
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        use: 'babel-loader',
        exclude: /node_modules/,
      },
      // Add other loaders for CSS, images, etc.
    ],
  },
};
```

### Step 2: Create an Entry Point Script that Handles Rendering

**src/index.js**:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import EmbeddedComponent from './components/EmbeddedComponent'; // Your Next.js component

// Function to render the component based on script tag attributes
(function() {
  // Find all script tags that load this bundle
  const scripts = document.getElementsByTagName('script');

  for (let script of scripts) {
    // Check if the script is the one loading our bundle (by src or ID attribute)
    if (script.src.includes('embedded-next-project.js') || script.getAttribute('data-embed') === 'next-project') {
      // Extract attributes or data attributes from the script tag
      const targetId = script.getAttribute('data-target'); // The target container ID
      const userId = script.getAttribute('data-user-id'); // The dynamic user ID passed

      // If targetId is provided, render the React component in that container
      if (targetId && userId) {
        ReactDOM.render(
          <EmbeddedComponent userId={userId} />,
          document.getElementById(targetId)
        );
      }
    }
  }
})();
```

### Step 3: Create a React Component that Uses the Passed ID

**src/components/EmbeddedComponent.js**:

```javascript
import React, { useEffect, useState } from 'react';

const EmbeddedComponent = ({ userId }) => {
  const [userData, setUserData] = useState(null);

  useEffect(() => {
    if (userId) {
      // Example API call based on the userId
      fetch(`https://api.example.com/users/${userId}`)
        .then((res) => res.json())
        .then((data) => setUserData(data));
    }
  }, [userId]);

  return (
    <div>
      {userData ? (
        <div>
          <h2>User Data for ID: {userId}</h2>
          <p>Name: {userData.name}</p>
          <p>Email: {userData.email}</p>
        </div>
      ) : (
        <p>Loading...</p>
      )}
    </div>
  );
};

export default EmbeddedComponent;
```

### Step 4: Build the Script with Webpack

Run the following command to build your project:

```bash
npx webpack --config webpack.config.js
```

### Step 5: Use the Script in the Main Project

In your host project or HTML, include the following:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Main Project</title>
    <!-- Use a single script tag to load and render the component -->
    <script
      src="https://your-cdn.com/path/to/embedded-next-project.js"
      data-embed="next-project"
      data-target="nextjs-container"
      data-user-id="123"
    ></script>
  </head>
  <body>
    <div id="nextjs-container"></div>
  </body>
</html>
```

### How It Works:
1. The script (`embedded-next-project.js`) is loaded via a single `<script>` tag.
2. The script looks for script tags that include the specific `data-embed="next-project"` attribute to identify itself.
3. It extracts the `data-target` (container ID) and `data-user-id` attributes.
4. It uses these attributes to render the React component into the target container (`nextjs-container`), passing the `userId` prop.

### Benefits:
- **Single Script Tag**: Only one `<script>` tag is required in the HTML.
- **Customizable**: The script tag’s `data-*` attributes can be dynamically set, allowing flexibility.
- **Reusable**: This approach makes it easy to embed your Next.js project in any HTML-based project.

This solution leverages the `<script>` tag with custom attributes to pass dynamic values, simplifying embedding and improving flexibility. Let me know if you have any other requirements or questions!

npm install --save-dev babel-loader @babel/core @babel/preset-env @babel/preset-react
