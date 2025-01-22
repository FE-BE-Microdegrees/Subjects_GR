# Ανάπτυξη ενός API Express στην παραγωγή: Εκπαιδευτικό υλικό

Η ανάπτυξη ενός API στην παραγωγή είναι μια πολύπλοκη διαδικασία που απαιτεί προσεκτικό σχεδιασμό και τήρηση βέλτιστων πρακτικών. Για την ανάπτυξη ενός API Express, οι εκτιμήσεις περιλαμβάνουν την επιλογή του διακομιστή, τη διαμόρφωση της εφαρμογής, την ασφάλεια, την εξισορρόπηση φορτίου και την παρακολούθηση. Αυτός ο οδηγός παρέχει μια βήμα προς βήμα προσέγγιση για την ανάπτυξη ενός Express API στην παραγωγή με χρήση του Node.js και δημοφιλών εργαλείων.

- [Ανάπτυξη ενός API Express στην παραγωγή: Εκπαιδευτικό υλικό](#Ανάπτυξη-ενός-API-Express-στην-παραγωγή-Εκπαιδευτικό-υλικό)
  - [Μαθησιακά αποτελέσματα](#Μαθησιακά-αποτελέσματα)
  - [1. Επιλογή και εγκατάσταση διακομιστή](#1-Επιλογή-και-εγκατάσταση-διακομιστή)
    - [Δημοφιλείς επιλογές διακομιστή](#Δημοφιλείς-επιλογές-διακομιστή)
    - [Παράδειγμα: Ρύθμιση ενός VPS](#Παράδειγμα-Ρύθμιση-ενός-VPS)
  - [2. Διαμόρφωση της εφαρμογής για παραγωγή](#2-Διαμόρφωση-της-εφαρμογής-για-παραγωγή)
    - [Χρήση μεταβλητών Environment](#Χρήση-μεταβλητών-Environment)
    - [Βελτιστοποίηση για παραγωγή](#Βελτιστοποίηση-για-παραγωγή)
  - [3. Εξισορρόπηση φορτίου και ομαδοποίηση](#3-Εξισορρόπηση-φορτίου-και-ομαδοποίηση)
    - [Εξισορρόπηση φορτίου](#Εξισορρόπηση-φορτίου)
    - [Χρήση των Clusters](#Χρήση-των-Clusters)
  - [4. Παρακολούθηση και καταγραφή](#4-Παρακολούθηση-και-καταγραφή)
    - [Παρακολούθηση της εφαρμογής](#Παρακολούθηση-της-εφαρμογής)
    - [Logging](#logging)
  - [5. Ασφάλεια](#5-Ασφάλεια)
    - [Πιστοποιητικά SSL](#Πιστοποιητικά-SSL)
    - [Βέλτιστες πρακτικές ασφάλειας](#Βέλτιστες-πρακτικές-ασφάλειας)

## Μαθησιακά αποτελέσματα

Στο τέλος αυτού του σεμιναρίου, οι εκπαιδευόμενοι θα είναι σε θέση να:

- Να επιλέξουν έναν κατάλληλο διακομιστή και να ρυθμίσουν ένα Express API για παραγωγή.
- Να διαμορφώνουν την εφαρμογή για ένα περιβάλλον παραγωγής.
- Να εφαρμόζουν βέλτιστες πρακτικές για να διασφαλίζουν την ασφάλεια και να βελτιστοποιούν την απόδοση.
- Να ρυθμίζουν την εξισορρόπηση φορτίου και την παρακολούθηση της εφαρμογής.

## 1. Επιλογή και εγκατάσταση διακομιστή (Server Selection and Setup)

Το πρώτο βήμα είναι η επιλογή ενός κατάλληλου διακομιστή για τη φιλοξενία του Express API σας. Ακολουθούν δημοφιλείς επιλογές:

### Δημοφιλείς επιλογές διακομιστή

1. **Virtual Private Server (VPS)**:
   - Πάροχοι όπως οι DigitalOcean, Linode και Amazon Lightsail προσφέρουν VPS με πλήρη έλεγχο των ρυθμίσεων..

2. **Platform-as-a-Service (PaaS)**:
   - Υπηρεσίες όπως το Heroku, το Vercel και το AWS Elastic Beanstalk απλοποιούν την ανάπτυξη, διαχειριζόμενες την υποδομή για εσάς.

3. **Container Orchestration**:
   - Το Docker και το Kubernetes είναι ιδανικά για την εκτέλεση εφαρμογών σε εμπορευματοκιβώτια και τη διαχείριση πολλαπλών υπηρεσιών.

### Παράδειγμα: Ρύθμιση ενός VPS

Θα χρησιμοποιήσουμε το DigitalOcean VPS (Droplet) ως παράδειγμα. Ας υποθέσουμε ότι έχετε δημιουργήσει ένα Droplet και έχετε εγκαταστήσει το Node.js και το NPM.

1. **SSH στον διακομιστή**

    ```bash
   ssh root@your_server_i
    ```

2. **Εγκαταστήστε το Node.js και το NPM**

 Install Node.js if not already installed. Follow [NodeSource instructions.](https://github.com/nodesource/distributions).

   ``` bash
   curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
   sudo apt-get install -y nodejs
   ```

3. **Εγκαταστήστε το Git**

   Paigaldage Git, et kloonida oma rakendus:

   ```bash
   sudo apt-get install git
   ```

4. **Κλωνοποιήστε την εφαρμογή σας**


   ```bash
   git clone https://github.com/yourusername/yourrepository.git
   cd yourrepository
   ```

5. **Εγκατάσταση εξαρτήσεων**

   Installige kõik vajalikud sõltuvused:

   ```bash
   npm install
   ```

6. **Ξεκινήστε την εφαρμογή με το PM2**

   ```bash
   sudo npm install -g pm2
   pm2 start app.js --name "my-express-app"
   pm2 save
   pm2 startup
   ```

Αυτό εξασφαλίζει την αυτόματη επανεκκίνηση της εφαρμογής σας σε περίπτωση επανεκκίνησης του διακομιστή.


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
