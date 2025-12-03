# Title：There is a SQL injection vulnerability in n8n

## 1.summary

- Title：There is a SQL injection vulnerability in n8n

- Vendor：n8n

- Product:n8n

- Affected Versions:all

- Vulnerability Type: SQL injection

## 2.Vulnerability Details

### 2.1Description

The "Import from URL" feature in n8n's workflow contains a **Server-Side Request Forgery (SSRF) vulnerability**. By constructing malicious URL parameters, an attacker can force the server to send requests to internal networks or protected systems. This allows them to bypass firewall restrictions, access internal services, or perform sensitive operations.

### 2.2Proof of Concept (PoC)

- Step 1: Deploy the application using Docker

```bash
docker volume create n8n_data
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

- Step 2: Create an account and complete the login.

- Step 3: Create a workflow and add the Merge module.

- Step 4: In the Merge module, set the **Parameters** value to `SQL Query`, enter `SELECT user()` in the **Query** parameter field, and click **Execute Step** to run it.