# No more Access-Control-Allow-Origin error

## Problem

>*No 'Access-Control-Allow-Origin' header is present on the requested resource*

This is the error that bugged me the most in the early stages of my web development journey.😪

To know more about this error and about CORS: 

https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/Errors/CORSMissingAllowOrigin

## Solution

The simplest way to resolve this issue is to build a proxy server.

>In computer networks, a proxy is a type of proxy server that retrieves resources on behalf of a client from one or more servers.

Don't let the name fool you, it is simple, dead simple. Of course only if you have, 

1. Visual Studio Code or any other code editor of your preference.
2. Node JS installed.
3. Some basics of Express JS
4. Some knowledge about Axios


If you don't know anything about Express, go to any tutorial on the internet and learn to setup an Express app, just the basics nothing much.

I have created a cors activated API for this tutorial (Lets call it Random value API), for which we are building the proxy server.

Random value API: https://random-value-generator.herokuapp.com/

Alright lets get started 💪

### Step 1

Create an empty folder, lets say its name is *proxy-server-demo* and open it with VS Code. Open terminal and enter 
```npm init -y```

This will create a file called package.json in the folder.

### Step 2

Install Express JS using 
```npm install express --save``` 
command in the terminal.

This creates package-lock.json and node_modules folder.

### Step 3

In order to send requests from the server we are creating, we need a package called ***axios*** which can be installed through the following command.

``npm install axios --save``

To set the Access-Control-Allow-Origin property to allow all origins the access to the response we need a package called ***cors***. So install that using

``npm install cors --save``

### Step 4

Create a new file ***index.js*** and enter the code below


```
const axios = require("axios");
const cors = require("cors");
const express = require("express");

const app = express();

const port = 3000;

app.use(
	cors({
		origin: "*", // Sets Access-Control-Allow-Origin to allow all origins
	})
); 

app.get("/", async (req, res) => {
	// Requesting Random value API
	try {
		const response = await axios.get(
			"https://random-value-generator.herokuapp.com/"
		);
		console.log(response.data);
		res.send(`${response.data}`);
	} catch (error) {
		console.log(error);
	}
});

app.listen(port, () => {
	console.log("Switched On");
});
``` 

### Step 5

Run the server using ``node index.js`` and make sure you add some reaction to this article😉.

Voila! 🎉 You have successfully setup a proxy server, Test it with your frontend.

Repository for the proxy server created in this tutorial: https://github.com/ikkurthis1998/proxy-server-demo 

## Conclusion
It is short one, but a useful one. If you have any queries still unresolved, please comment down below, I will try my best to resolve them.

See you in the next one. Howdy🤠