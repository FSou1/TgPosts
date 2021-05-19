# Create a react app

`npx create-react-app my-app`

# Change the manifest.json

```javascript
{
  "name": "Hello Extensions",
  "description": "Base Level Extension",
  "version": "1.0",
  "manifest_version": 2,
  "browser_action": {
    "default_popup": "index.html",
    "default_title": "Open the popup"
  }
}
```

# Build the extension

`npm run build`

# Load the unpacked extension

Chrome > Load unpacked > choose the `build` folder

# Inspect popup

Click the popup button.

It is not displayed.

Right click on the popup > Inspect.

The console contains an error: `Refused to execute inline script because it violates the following Content Security Policy directive`

# Fix the CSP error

Add the `.env` file in the root:

`INLINE_RUNTIME_CHUNK=false`

Rebuild > reload > works.

# Open a new page when click on the popup button

Add the `background.js` file to the `public` folder:

Since I don't want to open a popup, let's turn it off:
```javascript
chrome.browserAction.setPopup({ popup: '' });
```

When the icon is clicked, we'll open a new tab with the `index.html`:
```javascript
chrome.browserAction.onClicked.addListener(() => {
    chrome.tabs.create({ url: 'index.html' });
});
```

Build the app.

Inspect the `build` folder. The `background.js` file is here.

Let's add this file to the `manifest.json`.

# Update the manifest.json

Expand the `manifest.json` with the code:

```javascript
"background": {
  "scripts": [
    "background.js"
  ]
}
```

Build the app > click the popup.

A new tab opens. The `index.html` is loaded.

# Clean up

1. Remove `<header>` from `App.js`;
2. Remove `import logo` from `App.js`;
3. Remove `logo.svg` file
4. Remove `reportWebVitals.js` file
5. Remove `reportWebVitals` from `index.js`
6. Clean up `App.css`
7. Clean up `index.css`

Build the app > a completely empty index.html page is opened.

# Add styles to index.html

Now it's time to add styles to the index page.

First of all, we need to reset and normalize default styles.

# Reset.css

Open the page https://meyerweb.com/eric/tools/css/reset/

Create the `reset.css` file and add the styles

`index.js`:

```javascript
import './reset.css';
```

# Normalize.css

Open the page https://github.com/necolas/normalize.css/

Create the `normalize.css` file and add the styles

`index.js`:

```javascript
import './normalize.css';
```

# Show the difference

Rebuild the app > show the change in font on the index.html

# Add styles

My favorite classless CSS framework is Water.css, so let's open the page: https://cdn.jsdelivr.net/npm/water.css@2/out/water.css

Copy the styles and paste them to the `water.css` file

Add the import to the `index.js`:

`index.js`:

```javascript
import './water.css';
```

Rebuild > the styles are applied.

# Plan the app

Nowadays, the prices are really high and it can be difficult to get something you want.

So I decided to implement an extension, which notifies me when the price is changed or the product has become available.

Let's take a look at the example pages:

1. https://www.amazon.com/GeForce-Graphics-192-bit-IceStorm-DisplayPort/dp/B093QKVRCY/ref=sr_1_18?crid=3NXL8QOYB9T8T&dchild=1&keywords=3070+graphics+card&qid=1621460737&sprefix=3070%2Caps%2C206&sr=8-18
2. https://www.amazon.com/MSI-GeForce-RTX-3060-12G/dp/B08WPRMVWB/ref=sr_1_3?crid=3NXL8QOYB9T8T&dchild=1&keywords=3070+graphics+card&qid=1621460678&sprefix=3070%2Caps%2C206&sr=8-3
3. https://www.amazon.com/MSI-RTX-2070-Super-Architecture/dp/B0856BVRFL/ref=sr_1_21?crid=3NXL8QOYB9T8T&dchild=1&keywords=3070+graphics+card&qid=1621460737&sprefix=3070%2Caps%2C206&sr=8-21

/* Provide info how to get the price (first doesn't always work, second doesn't always work, the third is the most consistent) */

/* Show the loaded markup with the price: https://www.amazon.com/gp/aod/ajax/?asin=B0856BVRFL */

/* Remove useless parameters in URL, get ASIN */

# Add a watcher component

Add the `src/components` folder

Add the `Watcher.js` file:

```javascript
function Watcher() {
    return (
        <div>
            <h2>Watcher</h2>
            <p>This is the content of the watcher component</p>
        </div>
    );
}

export default Watcher;
```

Import into the `App.js`:

```javascript
import Watcher from './components/Watcher';

...

<div className="App">
  <h1>Index</h1>
  <Watcher />
</div>
```

Rebuild the app > `Watchers` is displayed.
