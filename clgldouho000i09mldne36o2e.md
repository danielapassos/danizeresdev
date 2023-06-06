---
title: "The Path to Developing the SumAI Extension: an AI powered text summarizer"
seoTitle: "Developing SumAI Extension: AI Text Summarizer"
seoDescription: "Introducing SumAI: AI-powered text summarizer for efficient web content consumption. Boost productivity for busy professionals and students."
datePublished: Mon Apr 17 2023 21:59:07 GMT+0000 (Coordinated Universal Time)
cuid: clgldouho000i09mldne36o2e
slug: the-path-to-developing-the-sumai-extension-an-ai-powered-text-summarizer
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681768146614/aec9b240-6639-494a-a1fc-0a85ecbaac4a.png
tags: javascript, chrome-extension, openai

---

Introducing SumAI, the intelligent AI-powered summarizer that helps you digest web content quickly and efficiently. Tired of sifting through lengthy articles and blog posts to find the key points? SumAI is here to make your life easier.

With SumAI, you can:

* Instantly generate concise, bullet-point summaries of web articles.
    
* Save time by focusing on the most important information.
    
* Improve your productivity and overall reading experience.
    

Using the OpenAI API keys, SumAI extracts the most relevant information from any webpage and presents it to you in an easy-to-understand format. Whether you're a busy professional, a student looking to optimize your research, or just someone who enjoys staying informed, SumAI is the perfect tool to help you read more in less time.

### Step 1: Setting up the Project

The first step in writing a Chrome extension is to create a new project. To do this, you'll need to create a new folder and create a file called "manifest.json" in that folder. This file will serve as the foundation for your extension and will contain all of the necessary information about your extension, including its name, description, and permissions.

Here's an example of what the manifest.json file might look like:

```javascript
{
  "manifest_version": 2,
  "name": "SumAI Extension",
  "description":
  "A powerful extension for enhancing the browsing experience.",
  "version": "1.0",
  "permissions": [
    "activeTab",
    "storage"
  ],
  "browser_action": {
  "default_icon": "icon.png",
  "default_popup": "popup.html"
}
}
```

### Step 2: Adding Functionality

Once you have set up the project, the next step is to add functionality to your extension. To do this, you'll need to write some JavaScript code that will run in the background of your extension and perform the necessary tasks.

Here's an example of some simple JavaScript code that will display a message in the console whenever the extension is clicked:

```javascript
chrome.browserAction.onClicked.addListener(function() {
console.log("SumAI Extension was clicked!");
});
```

### Step 3: Creating a Popup

In addition to the background script, you'll also need to create a popup for your extension. The popup is what will be displayed when the user clicks on the extension's icon in the browser. To create a popup, you'll need to create an HTML file (in this case, "popup.html") and a CSS file (in this case, "popup.css").

Here's an example of what the popup.html file might look like:

```javascript
<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" type="text/css" href="popup.css">
  </head>
  <body>
    <h1>Welcome to SumAI Extension!</h1>
  </body>
</html>
```

And here's an example of what the popup.css file might look like:

```javascript
body {
  background-color: lightgray;
  font-family: Arial, sans-serif;
  text-align: center;
}
```

### Step 4: Testing and Debugging

Once you have written your code and created your popup, it's time to test and debug your extension. To do this, you'll need to load your extension in Google Chrome and check for any errors or bugs. To load your extension, go to "chrome://extensions" in your browser and toggle on the "Developer mode" switch. Then, click on the "Load unpacked" button and select the folder containing your extension.

If you encounter any errors or bugs, you can use the Chrome DevTools to debug your code and find the source of the problem. To open the DevTools, right-click on the extension's icon in the browser and select "Inspect popup".

### Step 5: Publishing Your Extension

Once you have tested and debugged your extension, it's time to publish it to the Chrome Web Store. To do this, you'll need to create a developer account on the Chrome Web Store Developer Dashboard and submit your extension for review. Once your extension has been reviewed and approved, it will be available for download in the Chrome Web Store.

In conclusion, the journey of writing a Chrome extension can be challenging, but it's also incredibly rewarding. Whether you're a seasoned developer or just starting out, I hope that this step-by-step tutorial has provided you with the knowledge and inspiration you need to create your own powerful and innovative Chrome extension.

[Check out the GitHub repository here!](https://github.com/Double-String/sumAI)

Happy coding!

---

That is it for this article about my journey Building in Public!

Let's connect on [**Twitter**](https://twitter.com/danizeres) and [**LinkedIn**](https://www.linkedin.com/in/danipassos/) 👋