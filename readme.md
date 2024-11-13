### Step 1: Install Node.js and NPM
1. **Download Node.js**:
   - Go to the [Node.js download page](https://nodejs.org/).
   - Download the **LTS version** as it is more stable and recommended for most users.
   
2. **Install Node.js**:
   - Run the downloaded installer.
   - Follow the prompts and ensure the **"Add to PATH"** option is selected.
   - Complete the installation.

3. **Verify Installation**:
   - Open Command Prompt.
   - Run the following commands to check versions:
     ```bash
     node -v
     npm -v
     ```
   - You should see version numbers for both Node.js and NPM.

### Step 2: Install MySQL
1. **Download MySQL**:
   - Visit the [MySQL Community Downloads page](https://dev.mysql.com/downloads/mysql/).
   - Download and install the **MySQL Community Server** for Windows.

2. **Install MySQL**:
   - Follow the installation instructions, and set up a root password for the database.
   - Choose the **default port 3306**.
   - Ensure MySQL is set to run as a Windows Service.

3. **Start MySQL Server**:
   - Open the MySQL Workbench or run the command prompt as an administrator, and enter the following to start MySQL:
     ```bash
     mysql -u root -p
     ```
   - Enter the password you set during installation to access the MySQL CLI.

4. **Create a Database for Your Application**:
   - In the MySQL CLI, create a new database:
     ```sql
     CREATE DATABASE mean_stack;
     ```
   - This database will be used by your Express app.

### Step 3: Install Angular CLI
1. **Install Angular CLI via NPM**:
   - Run the following command in Command Prompt:
     ```bash
     npm install -g @angular/cli
     ```

2. **Verify Installation**:
   - Check the Angular CLI version by running:
     ```bash
     ng version
     ```
   - You should see the version details if it installed correctly.

### Step 4: Create a New Angular Project
1. **Generate an Angular Project**:
   - In Command Prompt, navigate to the directory where you want your project, and run:
     ```bash
     ng new my-mean-app
     ```
   - Angular CLI will prompt you to choose styles (CSS, SCSS, etc.)—select according to your preference.
   
2. **Run the Angular Application**:
   - Navigate to the project directory:
     ```bash
     cd my-mean-app
     ```
   - Start the Angular development server:
     ```bash
     ng serve
     ```
   - Open a browser and go to `http://localhost:4200` to see your running Angular app.

### Step 5: Install Express and Set Up Node Server
1. **Navigate to the Backend Directory**:
   - Within your Angular project, create a folder for your backend server:
     ```bash
     mkdir backend
     cd backend
     ```

2. **Initialize a New Node Project**:
   - Run:
     ```bash
     npm init -y
     ```
   - This will create a `package.json` file.

3. **Install Express and MySQL2**:
   - Install the necessary packages:
     ```bash
     npm install express mysql2
     ```
   - **Express** will handle server requests, and **mysql2** will help connect to the MySQL database.

4. **Create a Simple Server File**:
   - In the `backend` directory, create an `app.js` file with the following code:
     ```javascript
     const express = require('express');
     const mysql = require('mysql2');
     const app = express();

     // Middleware
     app.use(express.json());

     // MySQL Database Connection
     const db = mysql.createConnection({
       host: 'localhost',
       user: 'root',
       password: 'your_mysql_password', // Replace with your MySQL root password
       database: 'mean_stack'
     });

     db.connect(err => {
       if (err) {
         console.error('MySQL connection error:', err);
         return;
       }
       console.log('Connected to MySQL');
     });

     // Routes
     app.get('/', (req, res) => {
       res.send('Hello from Express and MySQL!');
     });

     // Start Server
     const PORT = 3000;
     app.listen(PORT, () => {
       console.log(`Server running on http://localhost:${PORT}`);
     });
     ```
   - **Note**: Replace `'your_mysql_password'` with the password you set for MySQL.

5. **Start the Server**:
   - In Command Prompt, run the following in the `backend` folder:
     ```bash
     node app.js
     ```
   - You should see a message indicating that the server is connected to MySQL.

### Step 6: Connect Angular and Express
1. **Proxy Configuration**:
   - In the Angular app (`my-mean-app`), create a `proxy.conf.json` file with the following:
     ```json
     {
       "/api": {
         "target": "http://localhost:3000",
         "secure": false
       }
     }
     ```
   - This will forward requests from Angular to your Express server.

2. **Update Angular `angular.json`**:
   - Add this line in the `"serve"` section:
     ```json
     "proxyConfig": "src/proxy.conf.json"
     ```

3. **Restart the Angular Development Server**:
   - Run:
     ```bash
     ng serve
     ```
   - Angular Requests to `/api` will now be proxied to the Express server.

---

After these steps, you should have a working MEAN stack setup with MySQL on your Windows machine. This configuration enables you to build a full-stack application, using MySQL as the backend database and Express to handle API requests. Let me know if you need any additional help!
