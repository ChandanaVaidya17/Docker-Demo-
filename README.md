FIle structure

docker-node-app/   # Project folder
│── Dockerfile     # Docker configuration file
│── server.js      # Simple Node.js script

```
npm init -y
```
this will create following file structure

docker-node-app/   # Project folder
│── Dockerfile     # Docker configuration file
│── package.json   # (Optional) Node.js dependencies file
│── server.js      # Simple Node.js script

### **1. Create a Simple Node.js Script (`server.js`)**
```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "text/plain" });
  res.end("Hello from Dockerized Node.js!\n");
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

---

### **2. Create a Dockerfile**
```dockerfile
# Use an official Node.js image as base
FROM node:18

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json first (if exists)
COPY package*.json ./

# Install dependencies (no dependencies needed for this example)
RUN npm install

# Copy the rest of the application files
COPY . .

# Expose port 3000
EXPOSE 3000

# Command to run the app
CMD ["node", "server.js"]
```

---

### **3. Build & Run the Docker Container**
Run these commands in the terminal inside the directory where the files are saved:

```sh
# Build the Docker image
docker build -t my-node-app .

# Run the container
docker run -p 3000:3000 my-node-app
```

---

### **4. Test the Running App**
Once the container is running, open a browser and visit:

```
http://localhost:3000
```

You should see:

```
Hello from Dockerized Node.js!
```

Let me know if you need further simplifications! 🚀
