---

## 🧱 Module 1: **API Basics & Types**

---
## 1. What is an API?

An **API (Application Programming Interface)** is like a messenger between different apps, systems, or devices. It helps them **talk to each other** by sending and receiving data. Developers use APIs to bridge the gaps between small, discrete chunks of code in order to create applications that are powerful, resilient, secure, and able to meet user needs. Even though you can't see them, APIs are everywhere—working continuously in the background to power the digital experiences that are essential to our modern lives.

![[Pasted image 20250418201914.png]]

---
### **Simple History of APIs**

1. **Starting Point – Business APIs (2000s)**  
    Big companies like **Amazon and eBay** made APIs so others could use their services in new ways—like selling stuff or checking product info online.
    
2. **Social Media Boom (Mid-2000s)**  
    Platforms like **Facebook and Twitter** used APIs to let apps share posts, photos, and user info. This helped social media grow fast.
    
3. **Cloud Power (2006 onward)**  
    **Amazon S3 and EC2** let developers store files and run servers using APIs. This made it easy to build apps without needing physical hardware.
    
4. **Mobile Apps Era (After 2007)**  
    Smartphones became popular, and apps like **Instagram and Twilio** used APIs to connect and work online. APIs became key to mobile app development.
    
5. **Smart Devices (After 2010)**  
    Devices like **Alexa, Nest, and Fitbit** started using APIs to talk to the internet. Now, even everyday things can be smart and connected.
    

---
## 2. How do APIs work?

![[Pasted image 20250418202137.png]]

### 🧠 Think of It Like a Restaurant 🍽️

- **You (the user)** are hungry and go to a restaurant.
    
- **The waiter** is the **API**. You tell the waiter what food you want.
    
- The **waiter takes your order (request)** to the kitchen (the **server**).
    
- The **kitchen prepares the food (data)** and gives it to the waiter.
    
- The **waiter brings it back to you** — that’s your **response**!
    

That’s exactly how APIs work:  
One app asks for something, and another gives the result.

---

### 🔄 How It Actually Works Behind the Scenes

1. **API Client (The app making the request)**  
    It could be a mobile app, website, or software that asks for data — like showing weather, products, or search results.
    
2. **API Request (The order)**  
    The request includes several parts:
    
    - **Endpoint**: The URL where the request goes (like `/articles`).
        
    - **Method**: What to do? (GET = get data, POST = create something, PUT = update, DELETE = remove).
        
    - **Parameters**: Extra details, like “I want articles about sports.”
        
    - **Headers**: Info like what type of data is being sent, or login/authentication info.
        
    - **Body**: The main content — like the text of a blog post you're uploading.
        
3. **API Server (The kitchen)**  
    It receives the request, checks if it’s allowed, understands what’s needed, and fetches or updates data accordingly.
    
4. **API Response (Your food)**  
    The server sends back:
    
    - **Status Code**: Shows what happened (200 = OK, 404 = Not Found, etc.).
        
    - **Headers**: Info about the response.
        
    - **Body**: The actual result — data you asked for, or an error message if something went wrong.


---

### ✅ Real-Life Examples

- **Weather app** uses an API to get today’s weather from a server.
    
- **Login with Google** uses Google’s API to sign you into another app.
    
- **Maps app** gets directions by calling an API with your starting point and destination.

---

### ✅ **Benefits of APIs (Made Simple)**

APIs let different apps, systems, or devices **talk to each other**, which brings a bunch of helpful advantages:

---

### 🔄 1. **Automation**

APIs can do boring, repetitive tasks automatically — like sending emails, updating databases, or running tests — so **humans can focus on smarter work**.

📌 _Example: Instead of manually entering customer data into multiple systems, an API can do it instantly._

---

### 🚀 2. **Faster Innovation**

APIs let developers **reuse existing tools or services** to build new apps faster — no need to start from scratch.

📌 _Example: A weather app doesn’t have to build its own weather system — it just uses a weather API._

---

### 🔐 3. **Improved Security**

APIs often require **authentication** (like API keys or tokens) and **permissions** to protect data. This adds a layer of **security**.

📌 _Example: Only logged-in users can access their private info through a secure API._

---

### 💸 4. **Cost Efficiency**

Instead of building everything in-house, companies can **use third-party APIs** to save time and money.

📌 _Example: A small business can use a payment API like Stripe instead of building its own payment system._

---

### ✨ Bonus Benefits

- 📱 **Better User Experience** – APIs allow apps to be faster, smarter, and more connected.
    
- 🌐 **Integration** – Easily connect different services (like linking your Instagram to Facebook).
    
- 📊 **Scalability** – Businesses can grow quickly by using APIs to handle more tasks or users.
    

---

## 3. What are the different types of API?

![[Pasted image 20250418202721.png]]
### 🔑 **Types of APIs (By Access Level)**

---

### 1. **Private APIs (Internal APIs)**

These are **only used inside a company**. They're used to connect different parts of a business’s own systems and apps.

📌 _Example:_ A social media app might have a private API for login, another for showing the feed, and another for messaging — all working behind the scenes.

✅ **Used by:** Company’s own developers  
❌ **Not available to the public**

---

### 2. **Public APIs (Open APIs)**

These are **available for anyone** to use — including third-party developers. Some are free, others require payment.

📌 _Example:_ A shopping app may use the **Stripe API** to handle payments, instead of building its own payment system.

✅ **Open to developers outside the company**  
💰 **Some are free, others are paid**

---

### 3. **Partner APIs**

These are shared **between trusted business partners** for collaboration. They're **not public**, and access is controlled with **authentication**.

📌 _Example:_ A travel booking site might use a **partner API** to access hotel availability from a hotel chain it works with.

✅ **Used by partners** (not public)  
🔐 **Requires authentication and permission**

---

## 4. What are the most common API architectural styles?

### 1. **REST (Representational State Transfer)**

![[Pasted image 20250418203419.png]]

A **REST API**, also known as a **RESTful API**, is a simple, uniform interface that is used to make data, content, algorithms, media, and other digital resources available through web URLs. REST APIs are the most common APIs used across the web today.

📌 **Most popular style** for web APIs.

- Uses standard HTTP methods like **GET, POST, PUT, DELETE**.
    
- Resources are accessed through URLs called **endpoints** (e.g., `/users`, `/products/123`).
    
- Works well with web and mobile apps.
    

✅ Easy to use  
✅ Widely supported  
❌ May need multiple requests to get all data

---

### 2. **SOAP (Simple Object Access Protocol)**

![[Pasted image 20250418204315.png]]

📌 **Used in older/enterprise systems**.

- Transfers data using **XML**.
    
- Includes **built-in security**, error handling, and strict standards.
    
- Slower and more complex compared to REST.


✅ Very secure  
✅ Good for banking or enterprise systems  
❌ Verbose and harder to work with

---

### 3. **GraphQL**

![[Pasted image 20250418204434.png]]

📌 **Modern and flexible** alternative to REST.

- Clients can **ask for exactly the data they need**, nothing more or less.
    
- Uses a **single endpoint**, unlike REST which has many.
    
- Great for apps on **slow or limited networks** (like mobile).
    

✅ Reduces unnecessary data  
✅ Fewer requests  
❌ More complex to set up and secure

---

### 4. **Webhooks**

![[Pasted image 20250418204618.png]]

📌 Used for **event-driven communication**.

- Instead of the client asking for data, the server **sends data automatically** when an event happens.
    
- Like getting a text message when your package is delivered.
    

✅ Real-time updates  
✅ Lightweight  
❌ Can fail silently if the receiver is down

---

### 5. **gRPC (Google Remote Procedure Call)**

![[Pasted image 20250418205645.png]]

📌 Designed for **fast communication between services**.

- Uses **Protocol Buffers** instead of JSON/XML (very fast and efficient).
    
- Great for **microservices** and systems where speed matters.
    
- Feels like calling a local function but works over a network.
    

✅ Super fast  
✅ Ideal for internal service-to-service communication  
❌ Harder to use in browsers and requires more setup

---

## 5. What are some common API use cases?

---

### 🔄 1. **Connecting Systems Together**

APIs allow different apps and tools to **talk to each other**.  
📌 _Example:_ A CRM automatically sends a welcome email when a new lead is added — by connecting the CRM with an email tool through an API.

---

### ➕ 2. **Adding Features Easily**

Instead of building everything from scratch, developers use APIs to **add features**.  
📌 _Example:_ A food delivery app uses a **map API** to show real-time order tracking.

---

### 📶 3. **Powering IoT Devices**

APIs help smart devices **connect to the internet and each other**.  
📌 _Example:_ A smart thermostat talks to the cloud to adjust room temperature via an API.

---

### 📈 4. **Building Scalable Systems with Microservices**

APIs connect small, separate services that make up a larger app (called **microservices**).  
📌 _Example:_ In a shopping app, one microservice handles payments, another handles orders — and they all talk using **private APIs**.

---

### 💸 5. **Cutting Costs with Automation**

APIs **automate manual work** like sending reports or syncing data between tools.  
📌 _Example:_ Instead of updating data in two apps, an API can do it instantly and automatically.

---

### 🔐 6. **Improving Security and Governance**

APIs support secure workflows and enforce rules.  
📌 _Example:_ **Single Sign-On (SSO)** lets users log in once and access multiple apps — all made possible with APIs.

---

### 🚀 Summary:

APIs are used to:

- **Integrate apps**
    
- **Add features**
    
- **Connect smart devices**
    
- **Scale systems**
    
- **Save time and money**
    
- **Secure and automate processes**


---

## 6. What are some real-world examples of APIs?

#### 🧩 **1. Salesforce API**

- **Use case:** Connects customer data, sales tracking, and support tools.
    
- **Example:** A support tool can pull customer history from Salesforce using an API, so agents have all info instantly.
    

#### 📝 **2. Notion API**

- **Use case:** Automate tasks and integrate with tools like Slack or Google Calendar.
    
- **Example:** Automatically create a Notion page when a new task is assigned in a project management tool.
    

#### 🎮 **3. Discord API**

- **Use case:** Build bots and custom server experiences.
    
- **Example:** A bot that posts welcome messages, auto-moderates chats, or plays music — all done using APIs.
    

#### 📌 **4. Pinterest API**

- **Use case:** Share content or analyze user engagement.
    
- **Example:** A content manager uses the API to auto-upload new blog images to Pinterest boards.
    

#### 🍔 **5. DoorDash API (Drive)**

- **Use case:** Let third-party businesses use DoorDash drivers.
    
- **Example:** A flower shop uses the DoorDash API to auto-book a Dasher for delivery once an order is placed.
    

---

## 7. Other common questions about APIs
### 🌍 **Who Uses APIs?**

- **Developers**: To build apps or services.
    
- **Product Managers & Business Analysts**: To define how systems talk to each other.
    
- **Support Teams**: To automate customer workflows using APIs.
    

---

### 🏢 **Industries That Use APIs**

- **Tech**: Apps, websites, cloud services.
    
- **Finance**: Bank APIs for payments, transactions, fraud detection.
    
- **Healthcare**: Patient data sharing between hospitals and health apps.
    
- **Retail**: Inventory, orders, payments, delivery tracking.
    

---

### 🚀 **What is API-First Strategy?**

> **API-First** = Design APIs **before** building the actual app.

- Makes sure the backend and frontend are separate and scalable.
    
- Encourages reusable, secure, and standardized APIs.
    

---

### 🛠️ **Tools to Build & Manage APIs**

- **Source Control**: GitHub, GitLab, Bitbucket
    
- **CI/CD**: Jenkins, GitHub Actions, CircleCI (automate testing/deployments)
    
- **API Platforms**: Postman, Swagger, Apigee (design, test, manage APIs)
    

---

### 🏗️ **What is API Management?**

It’s about **keeping APIs organized, secure, and efficient**:

- Control who can use the API
    
- Monitor traffic and performance
    
- Test and debug faster
    
- Secure with keys and authentication
    

---

### ⚔️ SOAP vs REST (Quick Comparison)

|Feature|SOAP|REST|
|---|---|---|
|Format|XML only|JSON (mostly), XML possible|
|Complexity|Heavy, strict structure|Lightweight, flexible|
|Use Case|Enterprise (e.g., banks, govt)|Web, mobile apps|
|Built-in Security|Yes (WS-Security)|Needs to be added manually|

---

### 🔄 APIs vs Webhooks

|APIs|Webhooks|
|---|---|
|Request initiated by client|Triggered automatically by events|
|Client asks server for data|Server **sends** data to client|
|Good for: On-demand data pulling|Good for: Real-time notifications|

---

