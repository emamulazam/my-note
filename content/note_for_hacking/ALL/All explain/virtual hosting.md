
### 🏠 What is Virtual Hosting?

**Virtual hosting** is a technique used by web servers (like Apache, Nginx) to host **multiple websites** on a **single IP address**.

There are two main types:

1. **IP-based virtual hosting** – one IP per website.

2. **Name-based virtual hosting** – multiple websites share the **same IP**, but are distinguished by **domain name**.

### 🌐 What is _Name-Based Virtual Hosting_?

With **name-based virtual hosting**, a single web server (on one IP) can serve **many websites** by checking the **"Host" header** in the HTTP request.

📦 **Example:**

Imagine the server `192.168.1.10` hosts two websites:

- `blog.example.com`
- `shop.example.com`

When you visit `http://blog.example.com`, your browser sends:

```
GET / HTTP/1.1   
Host: blog.example.com
```

The server sees the `Host` header and knows which site to serve — _even though both domains point to the same IP_.