# Mongo, Express, Node Project

**Getting Started:**

1. **Open a terminal or command prompt.**
2. **Create a new directory with your project name 'my_project_name':**
   ```bash
   mkdir my_project_name
   ```
3. **Go into this folder:**

    ```bash
    cd my_project_name
    ```

4. **Initialize a new Node.js project:**

   ```bash
   npm init -y
   ```

5. **Create server file and server folder:**

   ```
   mkdir server && touch server.js
   ```

6. **Lets create the server now**

   ```
   code .
   ```

7. **Copy this into server.js**

    ```javascript
    const express = require("express");
    const cors = require("cors");

    const app = express();
    const PORT = process.env.PORT || 8000;

    // configs
    require("./server/config/mongoose.config");

    // middleware
    app.use(cors());
    app.use(express.json());
    app.use(express.urlencoded({ extended: true }));

    // routes
    require("./server/routes/api.routes")(app);

    // server instance
    app.listen(PORT, () => {
      console.log(`Listening on port ${PORT}`);
    });
    ```

8. **Now we will create out folder structure:**
   ```bash
   cd server
   mkdir config controllers models routes
   ```
9. **Next we will configure and connect the mongoose database:**
   ```bash
   cd config
   touch mongoose.config.js
   ```
10. **Copy this into mongoose.config.js (update as needed):**

    ```javascript
    const mongoose = require("mongoose");

    mongoose
      .connect("mongodb://localhost/{db_name}") // replace db_name with your database name)
      .then(() => console.log("Established a connection to the database"))
      .catch((err) =>
        console.log("Something went wrong when connecting to the database", err)
      );
    ```

11. **Now our server and db should be set up. Start server by going back to the root of the project.**
    ```bash
    cd ../..
    npm run start
    ```
12. **We can update our package.json file to restart server on update by adding the following to scripts.**
    ```json
    "start": "node --watch server.js"
    ```
13. **Lets create our first API message**
    ```bash
    cd server
    touch controllers/api.controller.js
    touch routes/api.routes.js
    ```
14. **Add this to api.controllers.js file:**
    ```javascript
    module.exports.index = (request, response) => {
      response.json({
        message: "Hello, World!",
      });
    };
    ```
15. **Add this to api.routes.js file:**
    ```javascript
    const ApiController = require("../controllers/api.controller");
    
    module.exports = function (app) {
    app.get('/api', ApiController.index);
    };
    ```

16. **Now let's start our server and we should have a working api call on localhost:8000/api:**
  ```bash
  npm run start
  ```
