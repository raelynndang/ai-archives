# Hosting Decision for FullStack Application

## Problem
The application cannot be hosted entirely on S3 because the project contains APIs that require a runtime environment. Static S3 hosting only supports static files such as HTML, CSS, and JavaScript.

Since the project uses Next.js with backend logic, it requires a server environment capable of running Node.js.

## Options Considered

### Option 1: S3 Static Hosting
S3 can host static files such as HTML, CSS, and JavaScript. However, it cannot run server-side APIs or backend logic.

**Limitation:**  
Does not support runtime environments required for the Next.js backend.

### Option 2: EC2 Hosting
EC2 allows running a Node.js server which can support both frontend and backend logic.

Using EC2 also allows configuring additional services such as Nginx for reverse proxy and HTTPS using Certbot.

## Proposed Architecture

Client  
↓  
Nginx (Reverse Proxy + HTTPS)  
↓  
Node.js / Next.js Application (EC2)  
↓  
PostgreSQL Database  

Amazon S3 can be used separately for static asset storage or archived data.

## Final Decision

Host the full-stack application on **EC2** where Node.js can run the Next.js server.  
Use **Nginx** as a reverse proxy and configure **HTTPS using Certbot**.  
Use **PostgreSQL** as the main database and **S3** for object storage if needed.
