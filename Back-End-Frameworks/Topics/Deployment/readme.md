# Deploying an Express API to Production: A Tutorial

Deploying an API to production is a complex process requiring careful planning and adherence to best practices. To deploy an Express API, considerations include server selection, application configuration, security, load balancing, and monitoring. This guide provides a step-by-step approach to deploying an Express API to production using Node.js and popular tools.

- [Deploying an Express API to Production: A Tutorial](#deploying-an-express-api-to-production-a-tutorial)
  - [Learning Outcomes](#learning-outcomes)
  - [1. Server Selection and Setup](#1-server-selection-and-setup)
    - [Popular Server Options](#popular-server-options)
    - [Example: Setting Up a VPS](#example-setting-up-a-vps)
  - [2. Configuring the Application for Production](#2-configuring-the-application-for-production)
    - [Using Environment Variables](#using-environment-variables)
    - [Optimizing for Production](#optimizing-for-production)
  - [3. Load Balancing and Clustering](#3-load-balancing-and-clustering)
    - [Load Balancing](#load-balancing)
    - [Using Clusters](#using-clusters)
  - [4. Monitoring and Logging](#4-monitoring-and-logging)
    - [Application Monitoring](#application-monitoring)
    - [Logging](#logging)
  - [5. Security](#5-security)
    - [SSL Certificates](#ssl-certificates)
    - [Security Best Practices](#security-best-practices)

## Learning Outcomes

By the end of this tutorial, learners will be able to:

- Choose a suitable server and set up an Express API for production.
- Configure the application for a production environment.
- Apply best practices to ensure security and optimize performance.
- Set up load balancing and application monitoring.


## 1. Server Selection and Setup

The first step is to select an appropriate server to host your Express API. Here are popular options:

### Popular Server Options

1. **Virtual Private Server (VPS)**:
   - Providers like DigitalOcean, Linode, and Amazon Lightsail offer VPSs with complete control over configurations.

2. **Platform-as-a-Service (PaaS)**:
   - Services like Heroku, Vercel, and AWS Elastic Beanstalk simplify deployment by managing infrastructure for you.

3. **Container Orchestration**:
   - Docker and Kubernetes are ideal for running applications in containers and managing multiple services.

### Example: Setting Up a VPS

We’ll use DigitalOcean VPS (Droplet) as an example. Assume you’ve created a Droplet and installed Node.js and NPM.

1. **SSH into the Server**

    ```bash
   ssh root@your_server_i
    ```

2. **Install Node.js and NPM**

 Install Node.js if not already installed. Follow [NodeSource instructions.](https://github.com/nodesource/distributions).

   ``` bash
   curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
   sudo apt-get install -y nodejs
   ```

3. **Install Git**

   Paigaldage Git, et kloonida oma rakendus:

   ```bash
   sudo apt-get install git
   ```

4. **Clone Your Application**


   ```bash
   git clone https://github.com/yourusername/yourrepository.git
   cd yourrepository
   ```

5. **Install Dependencies**

   Installige kõik vajalikud sõltuvused:

   ```bash
   npm install
   ```

6. **Start the Application with PM2**

   ```bash
   sudo npm install -g pm2
   pm2 start app.js --name "my-express-app"
   pm2 save
   pm2 startup
   ```

  This ensures your application restarts automatically if the server reboots.

## 2. Configuring the Application for Production

### Using Environment Variables

Use environment variables for production configuration.

Install dotenv:
```bash
npm install dotenv
```

Create a .env file:

```plaintext
PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASS=s1mpl3
```

Access variables in your application:

```javascript
require('dotenv').config();
const express = require('express');
const app = express();

const port = process.env.PORT || 3000;

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```

### Optimizing for Production

- **Memory Management:**:
  node --max-old-space-size=1024 app.js

- **CORS: Install and configure `cors`**:

```javascript
const cors = require('cors');
app.use(cors());
```

- **Security:**:
  - Use `helmet` to secure HTTP headers.

```bash
npm install helmet
```

```javascript
const helmet = require('helmet');
app.use(helmet());
```

- **Static File Caching:**:
  
```javascript
app.use(express.static('public', {
  maxAge: '1d',
}));
```

## 3. Load Balancing and Clustering

### Load Balancing

Use tools like NGINX for load balancing:

  ```nginx
  upstream myapp {
      server 127.0.0.1:3000;
      server 127.0.0.1:3001;
  }

  server {
      listen 80;

      location / {
          proxy_pass http://myapp;
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
      }
  }
  ```

- **AWS ELB (Elastic Load Balancer)**: 

### Using Clusters

Utilize all CPU cores with Node.js clusters:

```javascript
const cluster = require('cluster');
const os = require('os');
const numCPUs = os.cpus().length;

if (cluster.isMaster) {
  // Loome worker-id
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker, code, signal) => {
    console.log(`Worker ${worker.process.pid} died`);
    cluster.fork(); // Asendame surnud worker-i uuega
  });
} else {
  // Worker-id käivitavad Expressi rakenduse
  const app = require('./app');
  const port = process.env.PORT || 3000;

  app.listen(port, () => {
    console.log(`Worker ${process.pid} is running on port ${port}`);
  });
}
```

## 4. Monitoring and Logging

### Application Monitoring

Use tools like PM2 for built-in monitoring:

```bash
pm2 monit
```

- Or third-party tools like New Relic or Datadog for detailed analysis.

### Logging

use `winston` or `morgan` for application logging:
```bash
npm install winston morgan
```

## 5. Security

### SSL Certificates

Configure SSL in NGINX:

```nginx
server {
    listen 443 ssl;
    server_name yourdomain.com;

    ssl_certificate /etc/ssl/certs/your_cert.crt;
    ssl_certificate_key /etc/ssl/private/your_key.key;

    location / {
        proxy_pass http://myapp;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

server {
    listen 80;
    server_name yourdomain.com;
    return 301 https://$host$request_uri;
}
```

### Security Best Practices

- **Environment Variablesd**: Avoid hardcoding sensitive data.
- **Rate Limiting**: Protect against DDoS attacks.

```bash
npm install express-rate-limit
```

```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutit
  max: 100, // Maksimaalselt 100 päringut akna jooksul
});

app.use(limiter);
```
