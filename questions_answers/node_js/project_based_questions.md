## Create a basic Express server with a /api/health route returning {status:”OK”}.
To create a basic Express server with a `/api/health` route that returns `{status: "OK"}`, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir express-server
   cd express-server
   npm init -y
   ```
2. **Install Express**:
   ```bash
    npm install express
    ```
3. **Create the server**:
   Create a file named `server.js` and add the following code:
   ```javascript
    const express = require('express');
    const app = express();
    const PORT = process.env.PORT || 3000;
    // Define the /api/health route
    app.get('/api/health', (req, res) => {
        res.json({ status: "OK" });
    });
    // Start the server
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
    ```
4. **Run the server**:
    ```bash
    node server.js
    ```
5. **Test the route**:
   You can test the `/api/health` route by navigating to `http://localhost:3000/api/health` in your web browser or using a tool like `curl` or Postman. You should see the response:
   ```json
   {
     "status": "OK"
   }
   ```
This is a basic Express server that listens on port 3000 and has a single route `/api/health` that returns a JSON response indicating the server's health status.

## Build a REST API for CRUD operations using Express and MongoDB.
To build a REST API for CRUD operations using Express and MongoDB, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir express-mongodb-api
   cd express-mongodb-api
   npm init -y
   ```
2. **Install necessary packages**:
   ```bash
    npm install express mongoose body-parser
    ```
3. **Set up MongoDB connection**:
   Create a file named `db.js` and add the following code to connect to MongoDB
    ```javascript
     const mongoose = require('mongoose');
     const uri = 'your_mongodb_connection_string'; // Replace with your MongoDB connection string
     mongoose.connect(uri, { useNewUrlParser: true, useUnifiedTopology: true })
          .then(() => console.log('MongoDB connected'))
          .catch(err => console.log(err));
     module.exports = mongoose;
     ```
4. **Define a Mongoose model**:
   Create a file named `models/Item.js` and add the following code to define a Mongoose model for an item:
   ```javascript
    const mongoose = require('../db');
    const ItemSchema = new mongoose.Schema({
        name: { type: String, required: true },
        description: String,
        price: Number
    });
    module.exports = mongoose.model('Item', ItemSchema);
    ```
5. **Create the Express server**:
   Create a file named `server.js` and add the following code to set up the Express server and define the CRUD routes:
   ```javascript
    const express = require('express');
    const bodyParser = require('body-parser');
    const Item = require('./models/Item');
    const app = express();
    const PORT = process.env.PORT || 3000;
    // Middleware
    app.use(bodyParser.json());
    // Create a new item
    app.post('/api/items', async (req, res) => {
        try {
            const newItem = new Item(req.body);
            const savedItem = await newItem.save();
            res.status(201).json(savedItem);
        } catch (err) {
            res.status(400).json({ error: err.message });
        }
    });
    // Get all items
    app.get('/api/items', async (req, res) => {
        try {
            const items = await Item.find();
            res.json(items);
        } catch (err) {
            res.status(500).json({ error: err.message });
        }
    });
    // Get a single item by ID
    app.get('/api/items/:id', async (req, res) => {
        try {
            const item = await Item.findById(req.params.id);
            if (!item) return res.status(404).json({ error: 'Item not found' });
            res.json(item);
        } catch (err) {
            res.status(500).json({ error: err.message });
        }
    });
    // Update an item by ID
    app.put('/api/items/:id', async (req, res) => {
        try {
            const updatedItem = await Item.findByIdAndUpdate(req.params.id, req.body, { new: true });
            if (!updatedItem) return res.status(404).json({ error: 'Item not found' });
            res.json(updatedItem);
        } catch (err) {
            res.status(400).json({ error: err.message });
        }
    });
    // Delete an item by ID
    app.delete('/api/items/:id', async (req, res) => {
        try {
            const deletedItem = await Item.findByIdAndDelete(req.params.id);
            if (!deletedItem) return res.status(404).json({ error: 'Item not found' });
            res.json({ message: 'Item deleted' });
        } catch (err) {
            res.status(500).json({ error: err.message
        });    });
    // Start the server
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
    ```
6. **Run the server**:
    ```bash
    node server.js
    ```
7. **Test the API**:
   You can test the API using tools like Postman or `curl` to perform CRUD operations on the `/api/items` endpoint. For example:
- **Create an item**:
   ```bash
   curl -X POST -H "Content-Type: application/json" -d '{"name":"Item 1","description":"This is item 1","price":10}' http://localhost:3000/api/items
   ```
- **Get all items**:
   ```bash
   curl http://localhost:3000/api/items
   ```
- **Get a single item by ID**:
   ```bash
    curl http://localhost:3000/api/items/{id}
    ```
- **Update an item by ID**:
   ```bash
    curl -X PUT -H "Content-Type: application/json" -d '{"name":"Updated Item","description":"This is the updated item","price":20}' http://localhost:3000/api/items/{id}
    ```
- **Delete an item by ID**:
   ```bash
    curl -X DELETE http://localhost:3000/api/items/{id}
    ```
This setup provides a basic REST API for managing items in a MongoDB database using Express. You can expand this further by adding authentication, validation, and more complex relationships between models as needed.

## Implement JWT authentication (signup + login + protected route).
To implement JWT authentication in a Node.js application using Express, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir jwt-authentication
   cd jwt-authentication
   npm init -y
   ```
2. **Install necessary packages**:
   ```bash
    npm install express mongoose bcryptjs jsonwebtoken body-parser
    ```
3. **Set up MongoDB connection**:
   Create a file named `db.js` and add the following code to connect to MongoDB:
   ```javascript
    const mongoose = require('mongoose');
    const uri = 'your_mongodb_connection_string'; // Replace with your MongoDB connection string
    mongoose.connect(uri, { useNewUrlParser: true, useUnifiedTopology: true })
        .then(() => console.log('MongoDB connected'))
        .catch(err => console.log(err));
    module.exports = mongoose;
    ```
4. **Define a Mongoose model for User**:
   Create a file named `models/User.js` and add the following code to define a Mongoose model for a user:
   ```javascript
    const mongoose = require('../db');
    const UserSchema = new mongoose.Schema({
        username: { type: String, required: true, unique: true },
        password: { type: String, required: true }
    });
    module.exports = mongoose.model('User', UserSchema);
    ```
5. **Create the Express server**:
   Create a file named `server.js` and add the following code to set up the Express server and define the authentication routes:
   ```javascript
    const express = require('express');
    const bodyParser = require('body-parser');
    const bcrypt = require('bcryptjs');
    const jwt = require('jsonwebtoken');
    const User = require('./models/User');
    const app = express();
    const PORT = process.env.PORT || 3000;
    const JWT_SECRET = 'your_jwt_secret'; // Replace with your own secret key
    // Middleware
    app.use(bodyParser.json());
    // Signup route
    app.post('/api/signup', async (req, res) => {
        try {
            const { username, password } = req.body;
            // Check if user already exists
            let user = await User.findOne({ username });
            if (user) return res.status(400).json({ error: 'User already exists' });
            // Hash the password
            const salt = await bcrypt.genSalt(10);
            const hashedPassword = await bcrypt.hash(password, salt);
            // Create new user
            user = new User({ username, password: hashedPassword });
            await user.save();
            res.status(201).json({ message: 'User created successfully' });
        } catch (err) {
            res.status(500).json({ error: err.message });
        }
    });
    // Login route
    app.post('/api/login', async (req, res) => {
        try {
            const { username, password } = req.body;
            // Find user by username
            const user = await User.findOne({ username });
            if (!user) return res.status(400).json({ error: 'Invalid credentials' });
            // Compare password
            const isMatch = await bcrypt.compare(password, user.password);
            if (!isMatch) return res.status(400).json({ error: 'Invalid credentials' });
            // Create JWT token
            const token = jwt.sign({ id: user._id }, JWT_SECRET, { expiresIn: '1h' });
            res.json({ token });
        } catch (err) {
            res.status(500).json({ error: err.message });
        }
    });
    // Middleware to protect routes
    const authMiddleware = (req, res, next) => {
        const token = req.header('Authorization');
        if (!token) return res.status(401).json({ error: 'No token provided' });
        try {
            const decoded = jwt.verify(token, JWT_SECRET);
            req.user = decoded;
            next();
        } catch (err) {
            res.status(401).json({ error: 'Invalid token' });
        }
    };
    // Protected route
    app.get('/api/protected', authMiddleware, (req, res) => {
        res.json({ message: 'This is a protected route', user: req.user });
    });
    // Start the server
    app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
    ```
6. **Run the server**:
    ```bash
    node server.js
    ```
7. **Test the API**:
   You can test the API using tools like Postman or `curl` to perform signup, login, and access the protected route. For example:
- **Signup**:
   ```bash
   curl -X POST -H "Content-Type: application/json" -d '{"username":"testuser","password":"testpassword"}' http://localhost:3000/api/signup
   ```
- **Login**:
   ```bash
    curl -X POST -H "Content-Type: application/json" -d '{"username":"testuser","password":"testpassword"}' http://localhost:3000/api/login
    ```
- **Access protected route** (replace `your_jwt_token` with the token received from the login response):
   ```bash
    curl -H "Authorization: your_jwt_token" http://localhost:3000/api/protected
    ```
This setup provides a basic JWT authentication system with signup, login, and a protected route. You can expand this further by adding features like password reset, email verification, and role-based access control as needed.

## Create middleware for request logging.
To create middleware for request logging in an Express application, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir express-request-logging
   cd express-request-logging
   npm init -y
   ```
2. **Install Express**:
   ```bash
    npm install express
    ```
3. **Create the logging middleware**:
   Create a file named `middleware/logger.js` and add the following code to define the logging middleware:
   ```javascript
    const logger = (req, res, next) => {
        const method = req.method;
        const url = req.originalUrl;
        const timestamp = new Date().toISOString();
        console.log(`[${timestamp}] ${method} ${url}`);
        next();
    };
    module.exports = logger;
    ```
4. **Set up the Express server**:
   Create a file named `server.js` and add the following code to set up the Express server and use the logging middleware:
   ```javascript
    const express = require('express');
    const logger = require('./middleware/logger');
    const app = express();
    const PORT = process.env.PORT || 3000;
    // Use the logging middleware
    app.use(logger);
    // Define a sample route
    app.get('/', (req, res) => {
        res.send('Hello, World!');
    });
    // Start the server
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
    ```
5. **Run the server**:
    ```bash
    node server.js
    ```
6. **Test the logging**:
   You can test the logging by navigating to `http://localhost:3000/` in your web browser or using a tool like `curl`. You should see the log output in the console for each request made to the server. For example, when you access the root route, you might see something like:
   ```
   [2024-06-01T12:00:00.000Z] GET /
   ```
This middleware will log the HTTP method, the requested URL, and a timestamp for each incoming request to the server. You can customize the logging format or add additional information (like request headers or body) as needed.

## Implement password hashing using bcrypt.
To implement password hashing using bcrypt in a Node.js application, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir bcrypt-password-hashing
   cd bcrypt-password-hashing
   npm init -y
   ```
2. **Install bcrypt**:
   ```bash
    npm install bcryptjs
    ```
3. **Create a file to demonstrate password hashing**:
   Create a file named `hashPassword.js` and add the following code to hash a password using bcrypt:
   ```javascript
    const bcrypt = require('bcryptjs');
    const password = 'mysecretpassword'; // Replace with the password you want to hash
    const saltRounds = 10; // Number of salt rounds for hashing

    // Hash the password
    bcrypt.hash(password, saltRounds, (err, hash) => {
        if (err) {
            console.error('Error hashing password:', err);
        } else {
            console.log('Hashed password:', hash);
        }
    });
    ```
4. **Run the password hashing script**:
    ```bash
    node hashPassword.js
    ```
5. **Verify the password**:
   You can also verify a password against the hashed version. Create a file named `verifyPassword.js` and add the following code:
   ```javascript
    const bcrypt = require('bcryptjs');
    const password = 'mysecretpassword'; // Replace with the password you want to verify
    const hashedPassword = '$2a$10$XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'; // Replace with the hashed password you want to verify against

    // Verify the password
    bcrypt.compare(password, hashedPassword, (err, result) => {
        if (err) {
            console.error('Error verifying password:', err);
        } else {
            console.log('Password match:', result);
        }
    });
    ```
6. **Run the password verification script**:
    ```bash
    node verifyPassword.js
    ```
This setup demonstrates how to hash a password using bcrypt and verify it later. In a real application, you would typically store the hashed password in a database and use the verification step during user login to authenticate users.

## Design a MongoDB schema for a User model.
To design a MongoDB schema for a User model using Mongoose in a Node.js application, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir user-model-schema
   cd user-model-schema
   npm init -y
   ```
2. **Install Mongoose**:
   ```bash
    npm install mongoose
    ```
3. **Set up MongoDB connection**:
   Create a file named `db.js` and add the following code to connect to MongoDB:
   ```javascript
    const mongoose = require('mongoose');
    const uri = 'your_mongodb_connection_string'; // Replace with your MongoDB connection string
    mongoose.connect(uri, { useNewUrlParser: true, useUnifiedTopology: true })
        .then(() => console.log('MongoDB connected'))
        .catch(err => console.log(err));
    module.exports = mongoose;
    ```
4. **Define the User schema**:
   Create a file named `models/User.js` and add the following code to define the User schema:
   ```javascript
    const mongoose = require('../db');
    const UserSchema = new mongoose.Schema({
        username: { type: String, required: true, unique: true },
        email: { type: String, required: true, unique: true },
        password: { type: String, required: true },
        createdAt: { type: Date, default: Date.now },
        updatedAt: { type: Date, default: Date.now }
    });
    // Middleware to update the updatedAt field before saving
    UserSchema.pre('save', function(next) {
        this.updatedAt = Date.now();
        next();
    });
    module.exports = mongoose.model('User', UserSchema);
    ```
This User schema includes the following fields:
- `username`: A string that is required and must be unique.
- `email`: A string that is required and must be unique.
- `password`: A string that is required.
- `createdAt`: A date that defaults to the current date and time.
- `updatedAt`: A date that defaults to the current date and time and is updated before each save operation.
You can expand this schema further by adding additional fields such as `firstName`, `lastName`, `role`, etc., depending on the requirements of your application.
This schema can be used to create, read, update, and delete user documents in a MongoDB collection using Mongoose.

## Implement pagination in API responses.
To implement pagination in API responses using Express and MongoDB with Mongoose, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir pagination-api
   cd pagination-api
   npm init -y
   ```
2. **Install necessary packages**:
   ```bash
    npm install express mongoose body-parser
    ```
3. **Set up MongoDB connection**:
   Create a file named `db.js` and add the following code to connect to MongoDB:
   ```javascript
    const mongoose = require('mongoose');
    const uri = 'your_mongodb_connection_string'; // Replace with your MongoDB connection string
    mongoose.connect(uri, { useNewUrlParser: true, useUnifiedTopology: true })
        .then(() => console.log('MongoDB connected'))
        .catch(err => console.log(err));
    module.exports = mongoose;
    ```
4. **Define a Mongoose model**:
   Create a file named `models/Item.js` and add the following code to define a Mongoose model for an item:
   ```javascript
    const mongoose = require('../db');
    const ItemSchema = new mongoose.Schema({
        name: { type: String, required: true },
        description: String,
        price: Number
    });
    module.exports = mongoose.model('Item', ItemSchema);
    ```
5. **Create the Express server with pagination**:
   Create a file named `server.js` and add the following code to set up the Express server and define a route that implements pagination:
   ```javascript
    const express = require('express');
    const bodyParser = require('body-parser');
    const Item = require('./models/Item');
    const app = express();
    const PORT = process.env.PORT || 3000;
    // Middleware
    app.use(bodyParser.json());
    // Get items with pagination
    app.get('/api/items', async (req, res) => {
        try {
            const page = parseInt(req.query.page) || 1; // Default to page 1
            const limit = parseInt(req.query.limit) || 10; // Default to 10 items per page
            const skip = (page - 1) * limit; // Calculate the number of items to skip
            const totalItems = await Item.countDocuments(); // Get total number of items
            const totalPages = Math.ceil(totalItems / limit); // Calculate total pages
            const items = await Item.find().skip(skip).limit(limit); // Fetch paginated items
            res.json({
                page,
                totalPages,
                totalItems,
                items
            });
        } catch (err) {
            res.status(500).json({ error: err.message });
        }
    });
    // Start the server
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
    ```
6. **Run the server**:
    ```bash
    node server.js
    ```
7. **Test the pagination**:
   You can test the pagination by navigating to `http://localhost:3000/api/items?page=1&limit=10` in your web browser or using a tool like `curl`. You should see a response that includes the current page, total pages, total items, and the items for that page. For example:
   ```json
   {
     "page": 1,
     "totalPages": 5,
     "totalItems": 50,
     "items": [
       {
         "_id": "60c72b2f9b1d8e5a4c8b4567",
         "name": "Item 1",
         "description": "This is item 1",
         "price": 10
       },
       // More items...
     ]
   }
   ```
This implementation allows you to fetch items from the database in a paginated manner, improving performance and user experience when dealing with large datasets. You can adjust the default values for `page` and `limit` as needed.

## Upload files using Multer and store them locally.
To upload files using Multer and store them locally in a Node.js application with Express, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir multer-file-upload
   cd multer-file-upload
   npm init -y
   ```
2. **Install necessary packages**:
   ```bash
    npm install express multer
    ```
3. **Create the Express server with Multer**:
   Create a file named `server.js` and add the following code to set up the Express server and define a route for file uploads using Multer:
   ```javascript
    const express = require('express');
    const multer = require('multer');
    const path = require('path');
    const app = express();
    const PORT = process.env.PORT || 3000;
    // Set up storage engine for Multer
    const storage = multer.diskStorage({
        destination: (req, file, cb) => {
            cb(null, 'uploads/'); // Directory to store uploaded files
        },
        filename: (req, file, cb) => {
            cb(null, Date.now() + path.extname(file.originalname)); // Unique filename with original extension
        }
    });
    const upload = multer({ storage });
    // Route to handle file upload
    app.post('/api/upload', upload.single('file'), (req, res) => {
        if (!req.file) {
            return res.status(400).json({ error: 'No file uploaded' });
        }
        res.json({ message: 'File uploaded successfully', filePath: req.file.path });
    });
    // Start the server
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
    ```
4. **Create the uploads directory**:
   Make sure to create an `uploads` directory in the root of your project to store the uploaded files:
   ```bash
    mkdir uploads
    ```
5. **Run the server**:
    ```bash
    node server.js
    ```
6. **Test the file upload**:
   You can test the file upload using a tool like Postman or `curl`. For example, using `curl`:
   ```bash
    curl -X POST -F "file=@/path/to/your/file.jpg" http://localhost:3000/api/upload
    ```
This will upload the specified file to the server and store it in the `uploads` directory. The response will include a message confirming the upload and the path to the uploaded file. You can adjust the storage configuration in Multer to change how files are named or where they are stored as needed.
This setup allows you to handle file uploads in your Express application using Multer, making it easy to manage and store files locally.

## Implement role-based authorization (admin, user).
To implement role-based authorization in a Node.js application using Express and JWT, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir role-based-authorization
   cd role-based-authorization
   npm init -y
   ```
2. **Install necessary packages**:
   ```bash
    npm install express mongoose bcryptjs jsonwebtoken body-parser
    ```
3. **Set up MongoDB connection**:
   Create a file named `db.js` and add the following code to connect to MongoDB:
   ```javascript
    const mongoose = require('mongoose');
    const uri = 'your_mongodb_connection_string'; // Replace with your MongoDB connection string
    mongoose.connect(uri, { useNewUrlParser: true, useUnifiedTopology: true })
        .then(() => console.log('MongoDB connected'))
        .catch(err => console.log(err));
    module.exports = mongoose;
    ```
4. **Define a Mongoose model for User with roles**:
   Create a file named `models/User.js` and add the following code to define a Mongoose model for a user with roles:
   ```javascript
    const mongoose = require('../db');
    const UserSchema = new mongoose.Schema({
        username: { type: String, required: true, unique: true },
        email: { type: String, required: true, unique: true },
        password: { type: String, required: true },
        role: { type: String, enum: ['admin', 'user'], default: 'user' }, // Role field
        createdAt: { type: Date, default: Date.now },
        updatedAt: { type: Date, default: Date.now }
    });
    // Middleware to update the updatedAt field before saving
    UserSchema.pre('save', function(next) {
        this.updatedAt = Date.now();
        next();
    });
    module.exports = mongoose.model('User', UserSchema);
    ```
5. **Create the Express server with role-based authorization**:
   Create a file named `server.js` and add the following code to set up the Express server and define routes for signup, login, and protected routes based on user roles:
   ```javascript
    const express = require('express');
    const bodyParser = require('body-parser');
    const bcrypt = require('bcryptjs');
    const jwt = require('jsonwebtoken');
    const User = require('./models/User');
    const app = express();
    const PORT = process.env.PORT || 3000;
    const JWT_SECRET = 'your_jwt_secret'; // Replace with your own secret key
    // Middleware
    app.use(bodyParser.json());
    // Signup route
    app.post('/api/signup', async (req, res) => {
        try {
            const { username, email, password, role } = req.body;
            // Check if user already exists
            let user = await User.findOne({ username });
            if (user) return res.status(400).json({ error: 'User already exists' });
            // Hash the password
            const salt = await bcrypt.genSalt(10);
            const hashedPassword = await bcrypt.hash(password, salt);
            // Create new user
            user = new User({ username, email, password: hashedPassword, role });
            await user.save();
            res.status(201).json({ message: 'User created successfully' });
        } catch (err) {
            res.status(500).json({ error: err.message });
        }
    });
    // Login route
    app.post('/api/login', async (req, res) => {
        try {
            const { username, password } = req.body;
            // Find user by username
            const user = await User.findOne({ username });
            if (!user) return res.status(400).json({ error: 'Invalid credentials' });
            // Compare password
            const isMatch = await bcrypt.compare(password, user.password);
            if (!isMatch) return res.status(400).json({ error: 'Invalid credentials' });
            // Create JWT token
            const token = jwt.sign({ id: user._id, role: user.role }, JWT_SECRET, { expiresIn: '1h' });
            res.json({ token });
        } catch (err) {
            res.status(500).json({ error: err.message });
        }
    });
    // Middleware to protect routes and check roles
    const authMiddleware = (roles) => (req, res, next) => {
        const token = req.header('Authorization');
        if (!token) return res.status(401).json({ error: 'No token provided' });
        try {
            const decoded = jwt.verify(token, JWT_SECRET);
            req.user = decoded;
            if (!roles.includes(decoded.role)) {
                return res.status(403).json({ error: 'Access denied' });
            }
            next();
        } catch (err) {
            res.status(401).json({ error: 'Invalid token' });
        }
    };
    // Protected route for admin only
    app.get('/api/admin', authMiddleware(['admin']), (req, res) => {
        res.json({ message: 'Welcome, admin!' });
    });
    // Protected route for users and admins
    app.get('/api/user', authMiddleware(['user', 'admin']), (req, res) => {
        res.json({ message: 'Welcome, user!' });
    });
    // Start the server
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
    ```
6. **Run the server**:
    ```bash
    node server.js
    ```
7. **Test the API**:
   You can test the API using tools like Postman or `curl` to perform signup, login, and access the protected routes based on user roles. For example:
- **Signup**:
   ```bash
   curl -X POST -H "Content-Type: application/json" -d '{"username":"adminuser","email":"admin@example.com","password":"password123","role":"admin"}' http://localhost:3000/api/signup
   ```
- **Login**:
   ```bash
    curl -X POST -H "Content-Type: application/json" -d '{"username":"adminuser","password":"password123"}' http://localhost:3000/api/login
    ```
- **Access admin route** (replace `your_jwt_token` with the token received from the login response):
   ```bash
    curl -H "Authorization: your_jwt_token" http://localhost:3000/api/admin
    ```
- **Access user route** (replace `your_jwt_token` with the token received from the login response):
   ```bash
    curl -H "Authorization: your_jwt_token" http://localhost:3000/api/user
    ```
This setup provides a basic role-based authorization system with signup, login, and protected routes for different user roles. You can expand this further by adding features like password reset, email verification, and more complex role hierarchies as needed.

## Add global error handling middleware in Express.
To add global error handling middleware in an Express application, you can follow these steps:
1. **Initialize a new Node.js project**:
   ```bash
   mkdir express-error-handling
   cd express-error-handling
   npm init -y
   ```
2. **Install Express**:
   ```bash
    npm install express
    ```
3. **Create the Express server with global error handling**:
   Create a file named `server.js` and add the following code to set up the Express server and define global error handling middleware:
   ```javascript
    const express = require('express');
    const app = express();
    const PORT = process.env.PORT || 3000;
    // Middleware to parse JSON bodies
    app.use(express.json());
    // Sample route that throws an error
    app.get('/api/error', (req, res) => {
        throw new Error('This is a sample error');
    });
    // Global error handling middleware
    app.use((err, req, res, next) => {
        console.error(err.stack); // Log the error stack trace
        res.status(500).json({ error: err.message }); // Send a JSON response with the error message
    });
    // Start the server
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
    ```
4. **Run the server**:
    ```bash
    node server.js
    ```
5. **Test the error handling**:
   You can test the error handling by navigating to `http://localhost:3000/api/error` in your web browser or using a tool like `curl`. You should see a JSON response with the error message:
   ```json
   {
     "error": "This is a sample error"
   }
   ```
This setup demonstrates how to add global error handling middleware in an Express application. The middleware catches any errors thrown in the routes and sends a JSON response with the error message. You can customize the error handling further by adding different status codes, logging mechanisms, or handling specific types of errors differently as needed.

## Write a Node.js program to create a simple HTTP server that returns “Hello Node.js”.
```javascript
const http = require('http');
const PORT = 3000;
const server = http.createServer((req, res) => {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello Node.js');
});
server.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}/`);
});
```

## Write a Node.js script to read a file asynchronously using the fs module.
```javascript
const fs = require('fs');
const filePath = 'path/to/your/file.txt'; // Replace with your file path

fs.readFile(filePath, 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log('File content:', data);
});
```

## Write a program to append text to an existing file using Node.js.
```javascript
const fs = require('fs');
const filePath = 'path/to/your/file.txt'; // Replace with your file path
const textToAppend = 'This is the text to append.\n'; // Replace with your text

fs.appendFile(filePath, textToAppend, (err) => {
    if (err) {
        console.error('Error appending to file:', err);
        return;
    }
    console.log('Text appended successfully.');
});
```

## Create a function that reads JSON data from a file and converts it into a JavaScript object.
```javascript
const fs = require('fs');
const filePath = 'path/to/your/data.json'; // Replace with your JSON file path

function readJsonFile(filePath, callback) {
    fs.readFile(filePath, 'utf8', (err, data) => {
        if (err) {
            callback(err, null);
            return;
        }
        try {
            const jsonData = JSON.parse(data);
            callback(null, jsonData);
        } catch (parseErr) {
            callback(parseErr, null);
        }
    });
}

// Usage example
readJsonFile(filePath, (err, jsonData) => {
    if (err) {
        console.error('Error reading JSON file:', err);
        return;
    }
    console.log('JSON data:', jsonData);
});
```
## Write a Node.js program to create and use environment variables.
```javascript
// Create a .env file in the root of your project and add the following line:
// MY_VARIABLE=HelloWorld

require('dotenv').config();

const myVariable = process.env.MY_VARIABLE;
console.log('My variable:', myVariable);

// To run this program, make sure to install the dotenv package:
// npm install dotenv
```

## Write a script to create a directory and then delete it.
```javascript
const fs = require('fs');
const dirPath = 'path/to/your/directory'; // Replace with your directory path

// Create the directory
fs.mkdir(dirPath, { recursive: true }, (err) => {
    if (err) {
        console.error('Error creating directory:', err);
        return;
    }
    console.log('Directory created successfully.');

    // Delete the directory
    fs.rmdir(dirPath, (err) => {
        if (err) {
            console.error('Error deleting directory:', err);
            return;
        }
        console.log('Directory deleted successfully.');
    });
});
```

## Write a Node.js program to log request method, URL, and headers for every incoming request.
```javascript
const http = require('http');
const PORT = 3000;
const server = http.createServer((req, res) => {
    console.log('Request Method:', req.method);
    console.log('Request URL:', req.url);
    console.log('Request Headers:', req.headers);
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Request logged successfully.');
});
server.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}/`);
});
```

## Write a Node.js script to convert a callback-based function into a Promise-based function.
```javascript
const fs = require('fs');

function readFileAsync(filePath) {
    return new Promise((resolve, reject) => {
        fs.readFile(filePath, 'utf8', (err, data) => {
            if (err) {
                reject(err);
                return;
            }
            resolve(data);
        });
    });
}

// Usage example
const filePath = 'path/to/your/file.txt'; // Replace with your file path
readFileAsync(filePath)
    .then((data) => {
        console.log('File content:', data);
    })
    .catch((err) => {
        console.error('Error reading file:', err);
    });
```

## Create a Node.js program to parse query parameters from a URL.
```javascript
const http = require('http');
const PORT = 3000;
const server = http.createServer((req, res) => {
    const url = new URL(req.url, `http://${req.headers.host}`);
    const queryParams = url.searchParams;
    console.log('Query Parameters:', Object.fromEntries(queryParams.entries()));
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Query parameters parsed successfully.');
});
server.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}/`);
});
```

## Write a script to generate a random OTP of 6 digits.
```javascript
function generateOTP() {
    return Math.floor(100000 + Math.random() * 900000).toString();
}
console.log('Generated OTP:', generateOTP());
```
without using built-in functions:
```javascript
function generateOTP() {
    let otp = '';
    for (let i = 0; i < 6; i++) {
        otp += Math.floor(Math.random() * 10).toString();
    }
    return otp;
}
console.log('Generated OTP:', generateOTP());
```

## Build a REST API using Express.js that performs CRUD operations on a users collection.
```javascript
const express = require('express');
const bodyParser = require('body-parser');
const app = express();
const PORT = process.env.PORT || 3000;
app.use(bodyParser.json());
let users = []; // In-memory users collection
// Create a new user
app.post('/users', (req, res) => {
    const user = { id: users.length + 1, ...req.body };
    users.push(user);
    res.status(201).json(user);
});
// Read all users
app.get('/users', (req, res) => {
    res.json(users);
});
// Read a user by ID
app.get('/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    if (!user) return res.status(404).json({ error: 'User not found' });
    res.json(user);
});
// Update a user by ID
app.put('/users/:id', (req, res) => {
    const user = users.find(u => u.id === parseInt(req.params.id));
    if (!user) return res.status(404).json({ error: 'User not found' });
    Object.assign(user, req.body);
    res.json(user);
});
// Delete a user by ID
app.delete('/users/:id', (req, res) => {
    const userIndex = users.findIndex(u => u.id === parseInt(req.params.id));
    if (userIndex === -1) return res.status(404).json({ error: 'User not found' });
    users.splice(userIndex, 1);
    res.json({ message: 'User deleted successfully' });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Create JWT-based authentication with login and protected routes.
```javascript
const express = require('express');
const bodyParser = require('body-parser');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const app = express();
const PORT = process.env.PORT || 3000;
const JWT_SECRET = 'your_jwt_secret'; // Replace with your own secret key
app.use(bodyParser.json());
// In-memory user store (replace with a database in production)
const users = [];
// Signup route
app.post('/api/signup', async (req, res) => {
    try {
        const { username, password } = req.body;
        // Check if user already exists
        if (users.find(u => u.username === username)) {
            return res.status(400).json({ error: 'User already exists' });
        }
        // Hash the password
        const salt = await bcrypt.genSalt(10);
        const hashedPassword = await bcrypt.hash(password, salt);
        // Create new user
        const user = { id: users.length + 1, username, password: hashedPassword };
        users.push(user);
        res.status(201).json({ message: 'User created successfully' });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
// Login route
app.post('/api/login', async (req, res) => {
    try {
        const { username, password } = req.body;
        // Find user by username
        const user = users.find(u => u.username === username);
        if (!user) return res.status(400).json({ error: 'Invalid credentials' });
        // Compare password
        const isMatch = await bcrypt.compare(password, user.password);
        if (!isMatch) return res.status(400).json({ error: 'Invalid credentials' });
        // Create JWT token
        const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
        res.json({ token });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
// Middleware to protect routes
const authMiddleware = (req, res, next) => {
    const token = req.header('Authorization');
    if (!token) return res.status(401).json({ error: 'No token provided' });
    try {
        const decoded = jwt.verify(token, JWT_SECRET);
        req.user = decoded;
        next();
    } catch (err) {
        res.status(401).json({ error: 'Invalid token' });
    }
};
// Protected route
app.get('/api/protected', authMiddleware, (req, res) => {
    res.json({ message: 'This is a protected route', userId: req.user.id });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement file upload functionality using multer.
```javascript
const express = require('express');
const multer = require('multer');
const app = express();
const PORT = process.env.PORT || 3000;

// Configure multer for file uploads
const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        cb(null, 'uploads/');
    },
    filename: (req, file, cb) => {
        cb(null, `${Date.now()}-${file.originalname}`);
    }
});
const upload = multer({ storage });

// File upload route
app.post('/upload', upload.single('file'), (req, res) => {
    res.json({ message: 'File uploaded successfully', file: req.file });
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Create a rate limiter middleware to restrict API requests.
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;
const rateLimit = require('express-rate-limit');
// Configure rate limiter
const limiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15 minutes
    max: 100, // Limit each IP to 100 requests per windowMs
    message: 'Too many requests from this IP, please try again later'
});
app.use(limiter);
// Sample route
app.get('/', (req, res) => {
    res.send('Hello, World!');
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build a custom middleware to log request time and response status.
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Custom middleware to log request time and response status
const logMiddleware = (req, res, next) => {
    const start = Date.now();
    res.on('finish', () => {
        const duration = Date.now() - start;
        console.log(`${req.method} ${req.originalUrl} ${res.statusCode} - ${duration}ms`);
    });
    next();
};

app.use(logMiddleware);

// Sample route
app.get('/', (req, res) => {
    res.send('Hello, World!');
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement pagination and filtering in a REST API.
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Sample data
const items = [
    { id: 1, name: 'Item 1', category: 'A' },
    { id: 2, name: 'Item 2', category: 'B' },
    { id: 3, name: 'Item 3', category: 'A' },
    { id: 4, name: 'Item 4', category: 'C' },
    { id: 5, name: 'Item 5', category: 'B' },
    // Add more items as needed
];

// Pagination and filtering route
app.get('/items', (req, res) => {
    const { page = 1, limit = 10, category } = req.query;
    let filteredItems = items;

    if (category) {
        filteredItems = filteredItems.filter(item => item.category === category);
    }

    const startIndex = (page - 1) * limit;
    const endIndex = page * limit;
    const paginatedItems = filteredItems.slice(startIndex, endIndex);

    res.json({
        page: parseInt(page),
        limit: parseInt(limit),
        total: filteredItems.length,
        items: paginatedItems
    });
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Create a role-based authorization system using middleware.
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Sample users with roles
const users = [
    { id: 1, name: 'Alice', role: 'admin' },
    { id: 2, name: 'Bob', role: 'user' }
];

// Middleware for role-based authorization
const authorize = (roles) => {
    return (req, res, next) => {
        const user = users.find(u => u.id === parseInt(req.header('userId')));
        if (!user || !roles.includes(user.role)) {
            return res.status(403).json({ message: 'Forbidden' });
        }
        req.user = user;
        next();
    };
};

// Sample routes
app.get('/admin', authorize(['admin']), (req, res) => {
    res.send('Welcome, admin!');
});

app.get('/user', authorize(['user', 'admin']), (req, res) => {
    res.send('Welcome, user!');
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build an API to send email using Nodemailer.
```javascript
const express = require('express');
const nodemailer = require('nodemailer');
const app = express();
const PORT = process.env.PORT || 3000;
app.use(express.json());
// Configure Nodemailer transporter
const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: process.env.EMAIL_USER,
        pass: process.env.EMAIL_PASS
    }
});

// Sample route to send email
app.post('/send-email', async (req, res) => {
    const { to, subject, text } = req.body;
    try {
        await transporter.sendMail({
            from: process.env.EMAIL_USER,
            to,
            subject,
            text
        });
        res.json({ message: 'Email sent successfully' });
    } catch (error) {
        res.status(500).json({ message: 'Error sending email', error });
    }
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement socket-based real-time chat backend using Socket.io
```javascript
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');
const app = express();
const server = http.createServer(app);
const io = socketIo(server);
io.on('connection', (socket) => {
    console.log('A user connected');
    socket.on('chat message', (msg) => {
        io.emit('chat message', msg); // Broadcast the message to all clients
    });
    socket.on('disconnect', () => {
        console.log('A user disconnected');
    });
});
server.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

## Design a complete backend authentication system with:
- Signup
- Login
- Forgot Password
- Reset Password

```javascript
const express = require('express');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const app = express();
const PORT = process.env.PORT || 3000;
const JWT_SECRET = process.env.JWT_SECRET || 'your_jwt_secret';
app.use(express.json());
// In-memory user store (replace with a database in production)
const users = [];
// Signup route
app.post('/signup', async (req, res) => {
    const { username, email, password } = req.body;
    if (users.find(u => u.username === username)) {
        return res.status(400).json({ message: 'User already exists' });
    }
    const hashedPassword = await bcrypt.hash(password, 10);
    const user = { id: users.length + 1, username, email, password: hashedPassword };
    users.push(user);
    res.status(201).json({ message: 'User created successfully' });
});
// Login route
app.post('/login', async (req, res) => {
    const { username, password } = req.body;
    const user = users.find(u => u.username === username);
    if (!user) return res.status(400).json({ message: 'Invalid credentials' });
    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) return res.status(400).json({ message: 'Invalid credentials' });
    const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
    res.json({ token });
});
// Forgot Password route
app.post('/forgot-password', (req, res) => {
    const { email } = req.body;
    const user = users.find(u => u.email === email);
    if (!user) return res.status(400).json({ message: 'User not found' });
    // In a real application, you would send an email with a reset link here
    res.json({ message: 'Password reset link sent to email' });
});
// Reset Password route
app.post('/reset-password', async (req, res) => {
    const { email, newPassword } = req.body;
    const user = users.find(u => u.email === email);
    if (!user) return res.status(400).json({ message: 'User not found' });
    user.password = await bcrypt.hash(newPassword, 10);
    res.json({ message: 'Password reset successfully' });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Create user registration API with validation using express-validator.
```javascript
const express = require('express');
const { body, validationResult } = require('express-validator');
const app = express();
const PORT = process.env.PORT || 3000;
app.use(express.json());
// User registration route with validation
app.post('/register', [
    body('username').isLength({ min: 3 }).withMessage('Username must be at least 3 characters long'),
    body('email').isEmail().withMessage('Invalid email address'),
    body('password').isLength({ min: 6 }).withMessage('Password must be at least 6 characters long')
], (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
    }
    // In a real application, you would save the user to the database here
    res.status(201).json({ message: 'User registered successfully' });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement login API with JWT token generation.
```javascript
const express = require('express');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const app = express();
const PORT = process.env.PORT || 3000;
const JWT_SECRET = process.env.JWT_SECRET || 'your_jwt_secret';
app.use(express.json());
// In-memory user store (replace with a database in production)
const users = [
    { id: 1, username: 'testuser', password: bcrypt.hashSync('password123', 10) }
];
// Login route
app.post('/login', async (req, res) => {
    const { username, password } = req.body;
    const user = users.find(u => u.username === username);
    if (!user) return res.status(400).json({ message: 'Invalid credentials' });
    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) return res.status(400).json({ message: 'Invalid credentials' });
    const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
    res.json({ token });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build refresh token mechanism for JWT authentication.
```javascript
const express = require('express');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const app = express();
const PORT = process.env.PORT || 3000;
const JWT_SECRET = process.env.JWT_SECRET || 'your_jwt_secret';
const REFRESH_TOKEN_SECRET = process.env.REFRESH_TOKEN_SECRET || 'your_refresh_token_secret';
app.use(express.json());

// In-memory user store (replace with a database in production)
const users = [
    { id: 1, username: 'testuser', password: bcrypt.hashSync('password123', 10) }
];

// In-memory refresh token store (replace with a database in production)
let refreshTokens = [];

// Login route
app.post('/login', async (req, res) => {
    const { username, password } = req.body;
    const user = users.find(u => u.username === username);
    if (!user) return res.status(400).json({ message: 'Invalid credentials' });
    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) return res.status(400).json({ message: 'Invalid credentials' });
    const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
    const refreshToken = jwt.sign({ id: user.id }, REFRESH_TOKEN_SECRET, { expiresIn: '7d' });
    refreshTokens.push(refreshToken);
    res.json({ token, refreshToken });
});

// Refresh token route
app.post('/token', (req, res) => {
    const { token } = req.body;
    if (!token) return res.sendStatus(401);
    if (!refreshTokens.includes(token)) return res.sendStatus(403);
    jwt.verify(token, REFRESH_TOKEN_SECRET, (err, user) => {
        if (err) return res.sendStatus(403);
        const accessToken = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
        res.json({ accessToken });
    });
});

// Logout route
app.post('/logout', (req, res) => {
    const { token } = req.body;
    refreshTokens = refreshTokens.filter(t => t !== token);
    res.sendStatus(204);
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement rate limiting middleware to prevent API abuse.
```javascript
const express = require('express');
const rateLimit = require('express-rate-limit');
const app = express();
const PORT = process.env.PORT || 3000;
// Configure rate limiter
const limiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15 minutes
    max: 100, // Limit each IP to 100 requests per windowMs
    message: 'Too many requests from this IP, please try again later'
});
app.use(limiter);
// Sample route
app.get('/', (req, res) => {
    res.send('Hello, World!');
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Create MongoDB aggregation query to calculate total user count.
```javascript
db.users.aggregate([
    {
        $group: {
            _id: null,
            totalUsers: { $sum: 1 }
        }
    }
]);
```

## Implement search API using regex in MongoDB.
```javascript
app.get('/search', async (req, res) => {
    const { query } = req.query;
    try {
        const results = await User.find({ username: { $regex: query, $options: 'i' } });
        res.json(results);
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
```

## Build forgot password + reset password APIs.
```javascript
app.post('/forgot-password', (req, res) => {
    const { email } = req.body;
    const user = users.find(u => u.email === email);
    if (!user) return res.status(400).json({ message: 'User not found' });
    // In a real application, you would send an email with a reset link here
    res.json({ message: 'Password reset link sent to email' });
});
app.post('/reset-password', async (req, res) => {
    const { email, newPassword } = req.body;
    const user = users.find(u => u.email === email);
    if (!user) return res.status(400).json({ message: 'User not found' });
    user.password = await bcrypt.hash(newPassword, 10);
    res.json({ message: 'Password reset successfully' });
});
```

## Add API request validation middleware.
```javascript
const { body, validationResult } = require('express-validator');
app.post('/register', [
    body('username').isLength({ min: 3 }).withMessage('Username must be at least 3 characters long'),
    body('email').isEmail().withMessage('Invalid email address'),
    body('password').isLength({ min: 6 }).withMessage('Password must be at least 6 characters long')
], (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
    }
    // In a real application, you would save the user to the database here
    res.status(201).json({ message: 'User registered successfully' });
});
```

## Implement email sending functionality using Nodemailer.
```javascript
const nodemailer = require('nodemailer');
// Configure Nodemailer transporter
const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: process.env.EMAIL_USER,
        pass: process.env.EMAIL_PASS
    }
});
// Sample route to send email
app.post('/send-email', async (req, res) => {
    const { to, subject, text } = req.body;
    try {
        await transporter.sendMail({
            from: process.env.EMAIL_USER,
            to,
            subject,
            text
        });
        res.json({ message: 'Email sent successfully' });
    } catch (error) {
        res.status(500).json({ message: 'Error sending email', error });
    }
});
```

## Build API documentation using Swagger.
```javascript
const swaggerUi = require('swagger-ui-express');
const swaggerDocument = require('./swagger.json'); // Create a swagger.json file with your API documentation
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
```

## Write a Node.js program to create a simple REST API using Express.js.
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;
app.use(express.json());
// Sample route
app.get('/', (req, res) => {
    res.send('Hello, World!');
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Write a script to read command-line arguments using process.argv.
```javascript
const args = process.argv.slice(2);
console.log('Command-line arguments:', args);
```

## Create a function to validate email format using regex.
```javascript
function validateEmail(email) {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
}
console.log(validateEmail('test@example.com')); // true
console.log(validateEmail('invalid-email')); // false
```

## Write a Node.js program to compress a file using the zlib module.
```javascript
const fs = require('fs');
const zlib = require('zlib');
const filePath = 'path/to/your/file.txt'; // Replace with your file path
const compressedFilePath = 'path/to/your/file.txt.gz'; // Replace with your desired compressed file path
const gzip = zlib.createGzip();
const input = fs.createReadStream(filePath);
const output = fs.createWriteStream(compressedFilePath);
input.pipe(gzip).pipe(output);
output.on('finish', () => {
    console.log('File compressed successfully');
});
```

## Create a Node.js script to stream a large file to the client.
```javascript
const express = require('express');
const fs = require('fs');
const app = express();
const PORT = process.env.PORT || 3000;
app.get('/download', (req, res) => {
    const filePath = 'path/to/your/largefile.txt'; // Replace with your large file path
    const readStream = fs.createReadStream(filePath);
    readStream.pipe(res);
    readStream.on('error', (err) => {
        res.status(500).json({ error: 'Error reading file' });
    });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Write a middleware to handle 404 errors globally.
```javascript
app.use((req, res, next) => {
    res.status(404).json({ message: 'Resource not found' });
});
```

## Write a Node.js program to convert a buffer into a string and vice versa.
```javascript
// Convert buffer to string
const buffer = Buffer.from('Hello, World!');
const str = buffer.toString();
console.log('Buffer to String:', str);
// Convert string to buffer
const newBuffer = Buffer.from(str);
console.log('String to Buffer:', newBuffer);
```

## Create a function to generate UUID using Node.js crypto module.
```javascript
const crypto = require('crypto');
function generateUUID() {
    return crypto.randomUUID();
}
console.log('Generated UUID:', generateUUID());
```

## Write a script to rename multiple files inside a directory.
```javascript
const fs = require('fs');
const path = require('path');
const directoryPath = 'path/to/your/directory'; // Replace with your directory path
fs.readdir(directoryPath, (err, files) => {
    if (err) {
        console.error('Error reading directory:', err);
        return;
    }
    files.forEach((file, index) => {
        const oldPath = path.join(directoryPath, file);
        const newPath = path.join(directoryPath, `newname_${index}${path.extname(file)}`);
        fs.rename(oldPath, newPath, (err) => {
            if (err) {
                console.error('Error renaming file:', err);
                return;
            }
            console.log(`Renamed ${file} to ${newPath}`);
        });
    });
});
```

## Build a simple API to return system information (CPU, RAM, OS).
```javascript
const express = require('express');
const os = require('os');
const app = express();
const PORT = process.env.PORT || 3000;
app.get('/system-info', (req, res) => {
    const systemInfo = {
        cpu: os.cpus(),
        ram: os.totalmem(),
        os: os.platform()
    };
    res.json(systemInfo);
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build a JWT refresh-token authentication system.
```javascript
const express = require('express');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const app = express();
const PORT = process.env.PORT || 3000;
const JWT_SECRET = process.env.JWT_SECRET || 'your_jwt_secret';
const REFRESH_TOKEN_SECRET = process.env.REFRESH_TOKEN_SECRET || 'your_refresh_token_secret';
app.use(express.json());
// In-memory user store (replace with a database in production)
const users = [
    { id: 1, username: 'testuser', password: bcrypt.hashSync('password123', 10) }
];
// In-memory refresh token store (replace with a database in production)
let refreshTokens = [];
// Login route
app.post('/login', async (req, res) => {
    const { username, password } = req.body;
    const user = users.find(u => u.username === username);
    if (!user) return res.status(400).json({ message: 'Invalid credentials' });
    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) return res.status(400).json({ message: 'Invalid credentials' });
    const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
    const refreshToken = jwt.sign({ id: user.id }, REFRESH_TOKEN_SECRET, { expiresIn: '7d' });
    refreshTokens.push(refreshToken);
    res.json({ token, refreshToken });
});
// Refresh token route
app.post('/token', (req, res) => {
    const { token } = req.body;
    if (!token) return res.sendStatus(401);
    if (!refreshTokens.includes(token)) return res.sendStatus(403);
    jwt.verify(token, REFRESH_TOKEN_SECRET, (err, user) => {
        if (err) return res.sendStatus(403);
        const accessToken = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
        res.json({ accessToken });
    });
});
// Logout route
app.post('/logout', (req, res) => {
    const { token } = req.body;
    refreshTokens = refreshTokens.filter(t => t !== token);
    res.sendStatus(204);
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement API caching using Redis.
```javascript
const express = require('express');
const redis = require('redis');
const app = express();
const PORT = process.env.PORT || 3000;
const redisClient = redis.createClient();
redisClient.on('error', (err) => {
    console.error('Redis error:', err);
});
// Middleware to check cache
const cacheMiddleware = (req, res, next) => {
    const key = req.originalUrl;
    redisClient.get(key, (err, data) => {
        if (err) {
            console.error('Redis error:', err);
            return next();
        }
        if (data) {
            return res.json(JSON.parse(data));
        }
        res.sendResponse = res.json;
        res.json = (body) => {
            redisClient.setex(key, 3600, JSON.stringify(body)); // Cache for 1 hour
            res.sendResponse(body);
        };
        next();
    });
};
// Sample route with caching
app.get('/data', cacheMiddleware, (req, res) => {
    // Simulate data fetching
    const data = { message: 'This is some data', timestamp: new Date() };
    res.json(data);
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Create a task queue system using BullMQ.
```javascript
const express = require('express');
const { Queue, Worker } = require('bullmq');
const app = express();
const PORT = process.env.PORT || 3000;
const myQueue = new Queue('my-queue');
// Worker to process tasks
const myWorker = new Worker('my-queue', async (job) => {
    console.log(`Processing job ${job.id} with data:`, job.data);
    // Simulate task processing
    await new Promise((resolve) => setTimeout(resolve, 1000));
    return { result: 'Task completed' };
});
// Route to add tasks to the queue
app.post('/add-task', async (req, res) => {
    const { taskData } = req.body;
    const job = await myQueue.add('my-task', taskData);
    res.json({ message: 'Task added to queue', jobId: job.id });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build real-time notifications using Socket.io.
```javascript
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');
const app = express();
const server = http.createServer(app);
const io = socketIo(server);
io.on('connection', (socket) => {
    console.log('A user connected');
    // Simulate sending a notification every 5 seconds
    setInterval(() => {
        socket.emit('notification', { message: 'This is a real-time notification' });
    }, 5000);
    socket.on('disconnect', () => {
        console.log('A user disconnected');
    });
});
server.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```

## Implement server-side pagination + sorting + filtering.
```javascript
app.get('/items', (req, res) => {
    const { page = 1, limit = 10, sortBy = 'name', order = 'asc', filter } = req.query;
    let filteredItems = items;
    if (filter) {
        filteredItems = filteredItems.filter(item => item.name.includes(filter));
    }
    const sortedItems = filteredItems.sort((a, b) => {
        if (order === 'asc') {
            return a[sortBy].localeCompare(b[sortBy]);
        } else {
            return b[sortBy].localeCompare(a[sortBy]);
        }
    });
    const startIndex = (page - 1) * limit;
    const endIndex = page * limit;
    const paginatedItems = sortedItems.slice(startIndex, endIndex);
    res.json({
        page: parseInt(page),
        limit: parseInt(limit),
        total: filteredItems.length,
        items: paginatedItems
    });
});
```

## Create API versioning middleware (v1, v2).
```javascript
app.use('/api/v1', (req, res, next) => {
    req.apiVersion = 'v1';
    next();
});
app.use('/api/v2', (req, res, next) => {
    req.apiVersion = 'v2';
    next();
});
app.get('/api/v1/items', (req, res) => {
    res.json({ message: 'This is API version 1' });
});
app.get('/api/v2/items', (req, res) => {
    res.json({ message: 'This is API version 2' });
});
```

## Implement graceful shutdown handling in Node.js
```javascript
const server = app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
const gracefulShutdown = () => {
    console.log('Shutting down gracefully...');
    server.close(() => {
        console.log('Server closed');
        process.exit(0);
    });
    setTimeout(() => {
        console.error('Forcing shutdown');
        process.exit(1);
    }, 10000); // Force shutdown after 10 seconds
};
process.on('SIGTERM', gracefulShutdown);
process.on('SIGINT', gracefulShutdown);
```

## Build image processing API using Sharp.
```javascript
const express = require('express');
const multer = require('multer');
const sharp = require('sharp');
const app = express();
const PORT = process.env.PORT || 3000;
const storage = multer.memoryStorage();
const upload = multer({ storage });
app.post('/upload-image', upload.single('image'), async (req, res) => {
    try {
        const processedImage = await sharp(req.file.buffer)
            .resize(300, 300)
            .toFormat('jpeg')
            .toBuffer();
        res.set('Content-Type', 'image/jpeg');
        res.send(processedImage);
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement API request validation using Joi or Zod.
```javascript
const express = require('express');
const Joi = require('joi');
const app = express();
const PORT = process.env.PORT || 3000;
app.use(express.json());
const schema = Joi.object({
    username: Joi.string().min(3).required(),
    email: Joi.string().email().required(),
    password: Joi.string().min(6).required()
});
app.post('/register', (req, res) => {
    const { error } = schema.validate(req.body);
    if (error) {
        return res.status(400).json({ error: error.details[0].message });
    }
    // In a real application, you would save the user to the database here
    res.status(201).json({ message: 'User registered successfully' });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build a secure password reset flow with email verification tokens.
```javascript
const express = require('express');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const nodemailer = require('nodemailer');
const app = express();
const PORT = process.env.PORT || 3000;
const JWT_SECRET = process.env.JWT_SECRET || 'your_jwt_secret';
app.use(express.json());
// In-memory user store (replace with a database in production)
const users = [
    { id: 1, username: 'testuser', email: 'testuser@example.com', password: '$2a$10$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36Z1Z/1F1F1F1F1F1F1F1F1' }
];
// Configure Nodemailer transporter
const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: process.env.EMAIL_USER,
        pass: process.env.EMAIL_PASS
    }
});
// Forgot Password route
app.post('/forgot-password', async (req, res) => {
    const { email } = req.body;
    const user = users.find(u => u.email === email);
    if (!user) {
        return res.status(404).json({ error: 'User not found' });
    }
    const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
    const resetLink = `http://localhost:${PORT}/reset-password?token=${token}`;
    await transporter.sendMail({
        from: process.env.EMAIL_USER,
        to: user.email,
        subject: 'Password Reset',
        text: `Click the link to reset your password: ${resetLink}`
    });
    res.json({ message: 'Password reset email sent' });
});
// Reset Password route
app.post('/reset-password', async (req, res) => {
    const { token, newPassword } = req.body;
    try {
        const decoded = jwt.verify(token, JWT_SECRET);
        const user = users.find(u => u.id === decoded.id);
        if (!user) {
            return res.status(404).json({ error: 'User not found' });
        }
        user.password = await bcrypt.hash(newPassword, 10);
        res.json({ message: 'Password reset successfully' });
    } catch (err) {
        res.status(400).json({ error: 'Invalid or expired token' });
    }
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Create a Node.js script to read, write, and delete a file using async/await.
```javascript
const fs = require('fs').promises;
const filePath = 'example.txt';
async function manageFile() {
    try {
        // Write to file
        await fs.writeFile(filePath, 'Hello, World!');
        console.log('File written successfully');
        // Read from file
        const data = await fs.readFile(filePath, 'utf-8');
        console.log('File content:', data);
        // Delete file
        await fs.unlink(filePath);
        console.log('File deleted successfully');
    } catch (err) {
        console.error('Error managing file:', err);
    }
}
manageFile();
```

## Build a simple Express middleware that logs request method, URL, and timestamp.
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;
// Middleware to log request method, URL, and timestamp
app.use((req, res, next) => {
    const timestamp = new Date().toISOString();
    console.log(`[${timestamp}] ${req.method} ${req.originalUrl}`);
    next();
});
// Sample route
app.get('/', (req, res) => {
    res.send('Hello, World!');
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Write a Node.js program to validate mobile numbers using regex.
```javascript
function validateMobileNumber(number) {
    const regex = /^\d{10}$/; // Validates 10-digit numbers
    return regex.test(number);
}
console.log(validateMobileNumber('1234567890')); // true
console.log(validateMobileNumber('12345')); // false
console.log(validateMobileNumber('abcdefghij')); // false
```

## Create a script to zip and unzip files using Node.js.
```javascript
const fs = require('fs');
const zlib = require('zlib');
// Zip a file
function zipFile(inputPath, outputPath) {
    const gzip = zlib.createGzip();
    const input = fs.createReadStream(inputPath);
    const output = fs.createWriteStream(outputPath);
    input.pipe(gzip).pipe(output);
    output.on('finish', () => {
        console.log('File zipped successfully');
    });
}
// Unzip a file
function unzipFile(inputPath, outputPath) {
    const gunzip = zlib.createGunzip();
    const input = fs.createReadStream(inputPath);
    const output = fs.createWriteStream(outputPath);
    input.pipe(gunzip).pipe(output);
    output.on('finish', () => {
        console.log('File unzipped successfully');
    });
}
// Example usage
zipFile('example.txt', 'example.txt.gz');
unzipFile('example.txt.gz', 'example_unzipped.txt');
```

## Write an API to fetch data from a public API using axios.
```javascript
const express = require('express');
const axios = require('axios');
const app = express();
const PORT = process.env.PORT || 3000;
app.get('/fetch-data', async (req, res) => {
    try {
        const response = await axios.get('https://api.publicapis.org/entries');
        res.json(response.data);
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build a Node.js function to hash passwords using bcrypt.
```javascript
const bcrypt = require('bcryptjs');
async function hashPassword(password) {
    const salt = await bcrypt.genSalt(10);
    const hashedPassword = await bcrypt.hash(password, salt);
    return hashedPassword;
}
hashPassword('mysecretpassword').then(hashed => {
    console.log('Hashed Password:', hashed);
});
```

## Write a script to schedule a task using node-cron.
```javascript
const cron = require('node-cron');
// Schedule a task to run every minute
cron.schedule('* * * * *', () => {
    console.log('Task running every minute:', new Date().toISOString());
});
```

## Create an Express API to handle form-data submissions.
```javascript
const express = require('express');
const multer = require('multer');
const app = express();
const PORT = process.env.PORT || 3000;
const storage = multer.memoryStorage();
const upload = multer({ storage });
app.post('/submit-form', upload.single('file'), (req, res) => {
    const { name, email } = req.body;
    const file = req.file;
    // Process form data and file as needed
    res.json({ message: 'Form submitted successfully', name, email, fileName: file.originalname });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build a function to generate secure random tokens using crypto.
```javascript
const crypto = require('crypto');
function generateSecureToken(length = 32) {
    return crypto.randomBytes(length).toString('hex');
}
console.log('Generated Secure Token:', generateSecureToken());
```

## Write a Node.js program to monitor memory usage of the process.
```javascript
setInterval(() => {
    const memoryUsage = process.memoryUsage();
    console.log('Memory Usage:', memoryUsage);
}, 5000); // Log memory usage every 5 seconds
```

## Build a complete REST API using MVC architecture.
```javascript
// This is a simplified example of an MVC architecture in Node.js using Express
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;
app.use(express.json());
// Model
class User {
    constructor(id, name) {
        this.id = id;
        this.name = name;
    }
}
const users = [new User(1, 'Alice'), new User(2, 'Bob')];
// Controller
const userController = {
    getAllUsers: (req, res) => {
        res.json(users);
    },
    getUserById: (req, res) => {
        const user = users.find(u => u.id === parseInt(req.params.id));
        if (!user) return res.status(404).json({ message: 'User not found' });
        res.json(user);
    },
    createUser: (req, res) => {
        const { name } = req.body;
        const newUser = new User(users.length + 1, name);
        users.push(newUser);
        res.status(201).json(newUser);
    }
};
// Routes
app.get('/users', userController.getAllUsers);
app.get('/users/:id', userController.getUserById);
app.post('/users', userController.createUser);
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement refresh token rotation in JWT authentication.
```javascript
// This is a simplified example of refresh token rotation in JWT authentication
const express = require('express');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const app = express();
const PORT = process.env.PORT || 3000;
const JWT_SECRET = process.env.JWT_SECRET || 'your_jwt_secret';
const REFRESH_TOKEN_SECRET = process.env.REFRESH_TOKEN_SECRET || 'your_refresh_token_secret';
app.use(express.json());
// In-memory user store (replace with a database in production)
const users = [
    { id: 1, username: 'testuser', password: bcrypt.hashSync('password123', 10) }
];
// In-memory refresh token store (replace with a database in production)
let refreshTokens = [];
// Login route
app.post('/login', async (req, res) => {
    const { username, password } = req.body;
    const user = users.find(u => u.username === username);
    if (!user) return res.status(400).json({ message: 'Invalid credentials' });
    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) return res.status(400).json({ message: 'Invalid credentials' });
    const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
    const refreshToken = jwt.sign({ id: user.id }, REFRESH_TOKEN_SECRET, { expiresIn: '7d' });
    refreshTokens.push(refreshToken);
    res.json({ token, refreshToken });
});
// Refresh token route with rotation
app.post('/token', (req, res) => {
    const { token } = req.body;
    if (!token) return res.sendStatus(401);
    if (!refreshTokens.includes(token)) return res.sendStatus(403);
    jwt.verify(token, REFRESH_TOKEN_SECRET, (err, user) => {
        if (err) return res.sendStatus(403);
        // Remove the old refresh token
        refreshTokens = refreshTokens.filter(t => t !== token);
        // Generate new tokens
        const accessToken = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
        const newRefreshToken = jwt.sign({ id: user.id }, REFRESH_TOKEN_SECRET, { expiresIn: '7d' });
        refreshTokens.push(newRefreshToken);
        res.json({ accessToken, refreshToken: newRefreshToken });
    });
});
// Logout route
app.post('/logout', (req, res) => {
    const { token } = req.body;
    refreshTokens = refreshTokens.filter(t => t !== token);
    res.sendStatus(204);
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build a secure file upload service with size & type validation.
```javascript
const express = require('express');
const multer = require('multer');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3000;
// Configure multer for file uploads
const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        cb(null, 'uploads/');
    },
    filename: (req, file, cb) => {
        cb(null, `${Date.now()}-${file.originalname}`);
    }
});
const fileFilter = (req, file, cb) => {
    const allowedTypes = ['image/jpeg', 'image/png', 'application/pdf'];
    if (allowedTypes.includes(file.mimetype)) {
        cb(null, true);
    } else {
        cb(new Error('Invalid file type'), false);
    }
};
const upload = multer({
    storage,
    limits: { fileSize: 5 * 1024 * 1024 }, // Limit file size to 5MB
    fileFilter
});
app.post('/upload', upload.single('file'), (req, res) => {
    if (!req.file) {
        return res.status(400).json({ message: 'No file uploaded' });
    }
    res.json({ message: 'File uploaded successfully', filePath: req.file.path });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement API request throttling using Redis.
```javascript
const express = require('express');
const redis = require('redis');
const app = express();
const PORT = process.env.PORT || 3000;
const redisClient = redis.createClient();
redisClient.on('error', (err) => {
    console.error('Redis error:', err);
});
// Middleware to throttle requests
const throttleMiddleware = (req, res, next) => {
    const ip = req.ip;
    const key = `throttle:${ip}`;
    redisClient.get(key, (err, data) => {
        if (err) {
            console.error('Redis error:', err);
            return next();
        }
        if (data) {
            return res.status(429).json({ message: 'Too many requests, please try again later' });
        }
        redisClient.setex(key, 60, '1'); // Throttle for 60 seconds
        next();
    });
};
// Sample route with throttling
app.get('/data', throttleMiddleware, (req, res) => {
    res.json({ message: 'This is some data' });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Create a custom error handling framework for Express.
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;
app.use(express.json());
// Custom error class
class AppError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.statusCode = statusCode;
        this.status = `${statusCode}`.startsWith('4') ? 'fail' : 'error';
        this.isOperational = true;
        Error.captureStackTrace(this, this.constructor);
    }
}
// Sample route that throws an error
app.get('/error', (req, res) => {
    throw new AppError('This is a custom error', 400);
});
// Global error handling middleware
app.use((err, req, res, next) => {
    if (err.isOperational) {
        res.status(err.statusCode).json({ status: err.status, message: err.message });
    } else {
        console.error('Unexpected error:', err);
        res.status(500).json({ status: 'error', message: 'Something went wrong' });
    }
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build real-time chat API using Socket.io + JWT auth.
```javascript
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');
const jwt = require('jsonwebtoken');
const app = express();
const server = http.createServer(app);
const io = socketIo(server);
const JWT_SECRET = process.env.JWT_SECRET
app.use(express.json());
// Middleware to authenticate socket connections
io.use((socket, next) => {
    const token = socket.handshake.query.token;
    if (!token) {
        return next(new Error('Authentication error'));
    }
    jwt.verify(token, JWT_SECRET, (err, decoded) => {
        if (err) {
            return next(new Error('Authentication error'));
        }
        socket.userId = decoded.id;
        next();
    });
});
io.on('connection', (socket) => {
    console.log(`User ${socket.userId} connected`);
    socket.on('chat message', (msg) => {
        io.emit('chat message', { userId: socket.userId, message: msg });
    });
    socket.on('disconnect', () => {
        console.log(`User ${socket.userId} disconnected`);
    });
});
server.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement API logging with Wiston + Morgan.
```javascript
const express = require('express');
const morgan = require('morgan');
const winston = require('winston');
const app = express();
const PORT = process.env.PORT || 3000;
// Configure Winston logger
const logger = winston.createLogger({
    level: 'info',
    format: winston.format.json(),
    transports: [
        new winston.transports.File({ filename: 'error.log', level: 'error' }),
        new winston.transports.File({ filename: 'combined.log' })
    ]
});
// Use Morgan for HTTP request logging
app.use(morgan('combined', {
    stream: {
        write: (message) => logger.info(message.trim())
    }
}));
// Sample route
app.get('/', (req, res) => {
    res.send('Hello, World!');
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Build secure payment order API (Razorpay / Stripe sandbox).
```javascript
const express = require('express');
const Stripe = require('stripe');
const app = express();
const PORT = process.env.PORT || 3000;
const stripe = Stripe(process.env.STRIPE_SECRET_KEY);
app.use(express.json());
app.post('/create-payment-intent', async (req, res) => {
    const { amount, currency } = req.body;
    try {
        const paymentIntent = await stripe.paymentIntents.create({
            amount,
            currency
        });
        res.json({ clientSecret: paymentIntent.client_secret });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```
with real payment gateway integration and secure handling of API keys.
```javascript
// Ensure you have your Stripe secret key in environment variables
const express = require('express');
const Stripe = require('stripe');
const app = express();
const PORT = process.env.PORT || 3000;
const stripe = Stripe(process.env.STRIPE_SECRET_KEY);
app.use(express.json());
app.post('/create-payment-intent', async (req, res) => {
    const { amount, currency } = req.body;
    try {
        const paymentIntent = await stripe.paymentIntents.create({
            amount,
            currency
        });
        res.json({ clientSecret: paymentIntent.client_secret });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```
razorpay integration example:
```javascript
const express = require('express');
const Razorpay = require('razorpay');
const app = express();
const PORT = process.env.PORT || 3000;
const razorpay = new Razorpay({
    key_id: process.env.RAZORPAY_KEY_ID,
    key_secret: process.env.RAZORPAY_KEY_SECRET
});
app.use(express.json());
app.post('/create-order', async (req, res) => {
    const { amount, currency } = req.body;
    try {
        const order = await razorpay.orders.create({
            amount,
            currency
        });
        res.json({ orderId: order.id });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement microservices communication using RabbitMQ.
```javascript
const amqp = require('amqplib');
// Producer
async function sendMessage(queue, message) {
    const connection = await amqp.connect('amqp://localhost');
    const channel = await connection.createChannel();
    await channel.assertQueue(queue);
    channel.sendToQueue(queue, Buffer.from(message));
    console.log(`Message sent to queue ${queue}: ${message}`);
    setTimeout(() => {
        connection.close();
    }, 500);
}
sendMessage('my_queue', 'Hello, RabbitMQ!');
// Consumer
async function receiveMessage(queue) {
    const connection = await amqp.connect('amqp://localhost');
    const channel = await connection.createChannel();
    await channel.assertQueue(queue);
    console.log(`Waiting for messages in queue ${queue}...`);
    channel.consume(queue, (msg) => {
        if (msg !== null) {
            console.log(`Received message from queue ${queue}: ${msg.content.toString()}`);
            channel.ack(msg);
        }
    });
}
receiveMessage('my_queue');
```

## Design a production-ready backend architecture for a scalable app.
Designing a production-ready backend architecture for a scalable app involves several key components and considerations. Below is an example of how you might structure such an architecture:
1. **API Gateway**: Acts as a single entry point for all client requests, handling routing, authentication, and rate limiting.
2. **Microservices**: Break down the application into smaller, independent services that handle specific business logic. Each microservice can be developed, deployed, and scaled independently.
3. **Database**: Use a combination of SQL and NoSQL databases based on the use case. For example, use a relational database for transactional data and a NoSQL database for unstructured data.
4. **Message Broker**: Implement a message broker (like RabbitMQ or Kafka) for asynchronous communication between microservices, allowing for better scalability and decoupling.
5. **Caching**: Use a caching layer (like Redis) to store frequently accessed data, reducing latency and improving performance.
6. **Load Balancer**: Use a load balancer to distribute incoming traffic across multiple instances of your services, ensuring high availability and reliability.
7. **Containerization**: Use Docker to containerize your services, making it easier to deploy and manage them in different environments.
8. **Orchestration**: Use Kubernetes or a similar orchestration tool to manage the deployment, scaling, and operation of your containerized services.
9. **Monitoring and Logging**: Implement monitoring (using tools like Prometheus and Grafana) and centralized logging (using tools like ELK stack) to track the health and performance of your services.
10. **Security**: Implement security best practices, such as using HTTPS, securing APIs with JWT or OAuth, and regularly updating dependencies to mitigate vulnerabilities.
```javascript
// Example of a simple microservice architecture using Express and RabbitMQ
const express = require('express');
const amqp = require('amqplib');
const app = express();
app.use(express.json());
// Microservice 1: User Service
app.post('/users', async (req, res) => {
    const user = req.body;
    // Save user to database (not implemented here)
    // Send a message to the message broker
    const connection = await amqp.connect('amqp://localhost');
    const channel = await connection.createChannel();
    await channel.assertQueue('user_created');
    channel.sendToQueue('user_created', Buffer.from(JSON.stringify(user)));
    res.status(201).json({ message: 'User created successfully' });
});
// Microservice 2: Notification Service
async function receiveUserCreatedMessages() {
    const connection = await amqp.connect('amqp://localhost');
    const channel = await connection.createChannel();
    await channel.assertQueue('user_created');
    console.log('Waiting for messages in user_created queue...');
    channel.consume('user_created', (msg) => {
        if (msg !== null) {
            const user = JSON.parse(msg.content.toString());
            console.log(`Received user created message:`, user);
            // Send notification (not implemented here)
            channel.ack(msg);
        }
    });
}
receiveUserCreatedMessages();
app.listen(3000, () => {
    console.log('User service running on port 3000');
});
```

## Implement API pagination + sorting + filtering together.
```javascript
app.get('/items', (req, res) => {
    const { page = 1, limit = 10, sortBy = 'name', order = 'asc', filter } = req.query;
    let filteredItems = items;
    if (filter) {
        filteredItems = filteredItems.filter(item => item.name.includes(filter));
    }
    const sortedItems = filteredItems.sort((a, b) => {
        if (order === 'asc') {
            return a[sortBy].localeCompare(b[sortBy]);
        } else {
            return b[sortBy].localeCompare(a[sortBy]);
        }
    });
    const startIndex = (page - 1) * limit;
    const endIndex = page * limit;
    const paginatedItems = sortedItems.slice(startIndex, endIndex);
    res.json({
        page: parseInt(page),
        limit: parseInt(limit),
        total: filteredItems.length,
        items: paginatedItems
    });
});
```

## Add MongoDB indexing and explain its impact.
MongoDB indexing is a powerful feature that allows you to improve the performance of your queries by creating indexes on specific fields in your collections. An index is a data structure that stores a portion of the collection's data in a way that makes it faster to search and retrieve documents based on the indexed fields.

When you create an index on a field, MongoDB builds a B-tree data structure that allows it to quickly locate documents that match the query criteria. This can significantly reduce the time it takes to execute queries, especially for large collections.

For example, if you have a collection of users and you frequently query by the "email" field, creating an index on the "email" field will allow MongoDB to quickly find the relevant documents without having to scan the entire collection.
```javascript
db.users.createIndex({ email: 1 });
```
The impact of indexing is that it can greatly improve query performance, but it also comes with some trade-offs. Indexes consume additional disk space and can slow down write operations (inserts, updates, deletes) because MongoDB needs to update the index every time a document is modified. Therefore, it's important to carefully choose which fields to index based on your application's query patterns and performance requirements.

## Implement soft delete using isDeleted flag.
```javascript
// Example of implementing soft delete using an isDeleted flag in a MongoDB collection
const mongoose = require('mongoose');
const itemSchema = new mongoose.Schema({
    name: String,
    isDeleted: { type: Boolean, default: false }
});
const Item = mongoose.model('Item', itemSchema);
// Soft delete an item
async function softDeleteItem(itemId) {
    await Item.findByIdAndUpdate(itemId, { isDeleted: true });
}
// Fetch non-deleted items
async function getActiveItems() {
    const items = await Item.find({ isDeleted: false });
    return items;
}
```

## Create transaction handling using MongoDB sessions.
```javascript
// Example of transaction handling using MongoDB sessions
const mongoose = require('mongoose');
async function performTransaction() {
    const session = await mongoose.startSession();
    session.startTransaction();
    try {
        // Perform multiple operations as part of the transaction
        await Item.create([{ name: 'Item 1' }, { name: 'Item 2' }], { session });
        await User.create({ name: 'User 1' }, { session });
        // Commit the transaction
        await session.commitTransaction();
        console.log('Transaction committed successfully');
    } catch (error) {
        // If an error occurs, abort the transaction
        await session.abortTransaction();
        console.error('Transaction aborted due to error:', error);
    } finally {
        session.endSession();
    }
}
```

## Implement API response compression using compression middleware.
```javascript
const express = require('express');
const compression = require('compression');
const app = express();
const PORT = process.env.PORT || 3000;
// Use compression middleware to compress API responses
app.use(compression());
// Sample route
app.get('/data', (req, res) => {
    const data = { message: 'This is some data that will be compressed' };
    res.json(data);
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Add CORS configuration for production environment
```javascript
const express = require('express');
const cors = require('cors');
const app = express();
const PORT = process.env.PORT || 3000;
// CORS configuration for production environment
const allowedOrigins = ['https://your-production-domain.com'];
app.use(cors({
    origin: function (origin, callback) {
        if (!origin || allowedOrigins.includes(origin)) {
            callback(null, true);
        } else {
            callback(new Error('Not allowed by CORS'));
        }
    }
}));
// Sample route
app.get('/data', (req, res) => {
    res.json({ message: 'This is some data' });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement request timeout handling.
```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;
// Middleware to handle request timeouts
app.use((req, res, next) => {
    const timeout = setTimeout(() => {
        res.status(503).json({ message: 'Request timed out' });
    }, 5000); // Set timeout to 5 seconds
    res.on('finish', () => clearTimeout(timeout)); // Clear timeout on response finish
    next();
});
// Sample route that simulates a long-running process
app.get('/long-process', (req, res) => {
    setTimeout(() => {
        res.json({ message: 'Long process completed' });
    }, 10000); // Simulate a process that takes 10 seconds
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Secure APIs using Helment.js.
```javascript
const express = require('express');
const helmet = require('helmet');
const app = express();
const PORT = process.env.PORT || 3000;
// Use Helmet to secure APIs by setting various HTTP headers
app.use(helmet());
// Sample route
app.get('/data', (req, res) => {
    res.json({ message: 'This is some data' });
});
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

## Implement database backup and restore strategy.
Implementing a database backup and restore strategy is crucial for ensuring data integrity and availability in case of data loss or corruption. Below is an example of how you can implement a backup and restore strategy for a MongoDB database using Node.js.
```javascript
const { exec } = require('child_process');
const dbName = 'your_database_name';
// Function to backup the database
function backupDatabase() {
    const backupCommand = `mongodump --db=${dbName} --out=./backup`;
    exec(backupCommand, (error, stdout, stderr) => {
        if (error) {
            console.error(`Error during backup: ${error.message}`);
            return;
        }
        if (stderr) {
            console.error(`Backup stderr: ${stderr}`);
            return;
        }
        console.log(`Backup stdout: ${stdout}`);
        console.log('Database backup completed successfully');
    });
}
// Function to restore the database
function restoreDatabase() {
    const restoreCommand = `mongorestore --db=${dbName} ./backup/${dbName}`;
    exec(restoreCommand, (error, stdout, stderr) => {
        if (error) {
            console.error(`Error during restore: ${error.message}`);
            return;
        }
        if (stderr) {
            console.error(`Restore stderr: ${stderr}`);
            return;
        }
        console.log(`Restore stdout: ${stdout}`);
        console.log('Database restore completed successfully');
    });
}
// Example usage
backupDatabase();
// To restore the database, you can call restoreDatabase() when needed
```

## Create a centralized config management system.
```javascript
const config = {
    development: {
        db: 'mongodb://localhost/dev_db',
        port: 3000,
        jwtSecret: 'your_jwt_secret'
    },
    production: {
        db: 'mongodb://localhost/prod_db',
        port: 8000,
        jwtSecret: 'your_jwt_secret'
    }
};
function getConfig(env) {
    return config[env] || config.development;
}
module.exports = getConfig;
```
