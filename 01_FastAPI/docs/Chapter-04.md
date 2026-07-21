# Chapter 04: What Exactly Is an HTTP Request?

## Objective

By the end of this chapter, you should understand:

- the structure of an **HTTP request**,
- the purpose of **method**, **URL**, **headers**, and **body**,
- where text, files, and metadata are placed,
- how AI applications use HTTP requests.

## The Big Question

In the previous chapter, we learned that clients communicate with servers using **HTTP requests**.

But what exactly is inside an HTTP request?

It is not just random data sent over the internet. It is a structured message that both the client and server understand.

> **Mental model**
>
> An HTTP request is a structured message sent from a client to a server.

## Courier Form Analogy

Think of an HTTP request like filling out a courier form.

Before a package can be delivered, the courier needs to know:

- what action you want,
- where the package should go,
- any special instructions,
- what is inside the package.

An HTTP request works in a similar way.

```text
HTTP Request
|
|-- Method
|-- URL
|-- Headers
|-- Body
```

Each part has a specific job.

## 1. Method

The **method** tells the server what action the client wants to perform.

Common HTTP methods:

| Method | Meaning | Common use |
| --- | --- | --- |
| `GET` | Retrieve data | Get model list or health status |
| `POST` | Send new data | Run prediction or create a resource |
| `PUT` | Replace data | Replace full configuration |
| `PATCH` | Partially update data | Update one setting |
| `DELETE` | Remove data | Delete a model or API key |

Examples:

```text
GET /models
POST /predict
DELETE /users/42
```

> **Simple way to remember**
>
> The method is the **verb** of the request.


## 2. URL

The **URL (Uniform Resource Locator)** tells the client **where to send the request**.

Think of a URL as the complete address used to reach a specific resource or functionality on a server.

Example:

```text
https://api.company.com/predict
```

Breaking it down:

```text
https://api.company.com/predict
│       │   │       │    │
│       │   │       │    └── Path / Endpoint
│       │   │       └─────── Top-Level Domain (TLD)
│       │   └─────────────── Main Domain
│       └─────────────────── Subdomain
└─────────────────────────── Protocol
```

### Protocol

The **protocol** defines how the client and server communicate.

Examples:

```text
http://
https://
```

Production APIs almost always use **HTTPS** because it protects data while it travels between the client and server.

---

### Domain Name

A **domain name** is the human-readable name used to identify a server or service on the Internet.

Consider:

```text
www.company.com
```

It can be broken down as:

```text
www  .  company  .  com
 │         │          │
 │         │          └── Top-Level Domain (TLD)
 │         │
 │         └───────────── Main / Second-Level Domain
 │
 └─────────────────────── Subdomain
```

* `com` → Top-Level Domain (TLD)
* `company` → Main or second-level domain
* `www` → Subdomain

`www` traditionally stands for **World Wide Web**, but it is not mandatory.

For example:

```text
www.company.com
company.com
```

Both can be configured to serve the company's website.

Different subdomains can also be used for different services:

```text
www.company.com       → Website
api.company.com       → API
docs.company.com      → Documentation
```

Here, `www`, `api`, and `docs` are all **subdomains**.

> **Mental Model**
>
> `company.com` = Main domain
> `www.company.com` = Website subdomain
> `api.company.com` = API subdomain

---

### Domain Name and IP Address

Computers ultimately communicate using **IP addresses**, such as:

```text
142.250.183.46
```

Remembering IP addresses would be inconvenient, so we use human-readable domain names instead.

A system called **DNS (Domain Name System)** translates the domain name into its corresponding IP address.

```text
api.company.com
       │
       ▼
      DNS
       │
       ▼
IP Address
       │
       ▼
Server
```

> **Analogy**
>
> A **domain name** is like a person's name in your phone contacts.
>
> An **IP address** is their phone number.
>
> **DNS** is the contact list that finds the phone number for you.

---

### URL vs Domain Name

A **domain name is only one part of a URL**.

For example:

```text
https://api.company.com/predict
└───────────┬────────────────┘
            URL

        api.company.com
        └──────┬──────┘
           Domain Name
```

| Domain Name                       | URL                                                |
| --------------------------------- | -------------------------------------------------- |
| Identifies a server or service    | Complete address of a resource                     |
| `api.company.com`                 | `https://api.company.com/predict`                  |
| Does not include protocol or path | Can include protocol, domain, path, and parameters |

> **Mental Model**
>
> **URL = Complete Address**
>
> **Domain Name = Server/Service Address**
>
> **Path = Specific Resource or Functionality**

---

### Path / Endpoint

The **path** identifies a specific resource or functionality available on the server.

Examples:

```text
/predict
/models
/users
/health
/login
```

The same domain can expose many different API endpoints:

```text
https://api.company.com/models
https://api.company.com/predict
https://api.company.com/login
```

All requests go to the same API domain:

```text
api.company.com
```

but the **path tells the application what resource or functionality the client wants to access**.

---

### Path Parameters

Path parameters identify a **specific resource**.

```text
GET /users/42
GET /models/resnet50
```

Here:

```text
42         → Specific user
resnet50   → Specific model
```

For example:

```text
/users/42
```

can be understood as:

> Give me the user whose ID is `42`.

---

### Query Parameters

Query parameters provide **additional options, filters, or controls** for a request.

They appear after `?` in the URL.

Example:

```text
GET /models?type=vision&limit=10
```

Here:

```text
type=vision   → Return only vision models
limit=10      → Return at most 10 results
```

Multiple query parameters are separated using `&`.

> **Mental Model**
>
> **Path Parameter → Which specific resource?**
>
> **Query Parameter → How should I filter or customize the result?**

For example:

```text
GET /models/resnet50?version=2
```

```text
/models/resnet50
        │
        └── Specific resource

version=2
    │
    └── Additional option
```


## 3. Headers

**Headers** provide extra information about the request.

They usually do not contain the main data. They describe the request.

Common headers:

```text
Content-Type: application/json
Authorization: Bearer <token>
Accept: application/json
```

What they mean:

| Header | Purpose |
| --- | --- |
| `Content-Type` | Tells the server the format of the request body. |
| `Authorization` | Sends authentication information. |
| `Accept` | Tells the server what response format the client wants. |

> **Mental model**
>
> Headers are like labels attached to a package.

## 4. Body

The **body** contains the actual data sent to the server.

For AI applications, this is often the most important part of the request.

Examples:

### Chatbot

```json
{
  "message": "What is machine learning?"
}
```

### Image Classification

```text
image.jpg
```

### Speech Recognition

```text
audio.wav
```

### OCR

```text
invoice.pdf
```

Without a body, there is often nothing for the AI model to process.

> **Important**
>
> The body is not always JSON. It can also contain images, audio, video, PDFs, binary data, or form data.

## Full HTTP Request Example

Here is a simplified request to an AI prediction endpoint:

```text
POST /predict HTTP/1.1
Host: api.company.com
Content-Type: application/json
Authorization: Bearer <token>

{
  "image_url": "dog.jpg"
}
```

What each part means:

- `POST` tells the server that data is being sent.
- `/predict` tells the server which endpoint should handle it.
- `Content-Type` tells the server the body is JSON.
- `Authorization` sends the access token.
- The body contains the input needed for prediction.

## AI Request Examples

| AI task | Method | Body |
| --- | --- | --- |
| Chatbot | `POST` | Prompt or conversation |
| Image Classification | `POST` | Image or image URL |
| Speech Recognition | `POST` | Audio file |
| OCR | `POST` | PDF or image |
| Health Check | `GET` | No body |
| List Models | `GET` | No body |

AI inference usually uses `POST` because the client needs to send input data to the server.

## What Is CRUD?

When working with APIs, you'll frequently hear the term **CRUD**.

CRUD represents the four basic operations applications perform on resources:

* **Create** → Add something new
* **Read** → Retrieve something
* **Update** → Modify something
* **Delete** → Remove something

HTTP methods are commonly used to perform these CRUD operations through an API:

| CRUD Operation       | HTTP Method | Example                          |
| -------------------- | ----------- | -------------------------------- |
| **Create**           | `POST`      | Create a new model configuration |
| **Read**             | `GET`       | Retrieve model details           |
| **Update (replace)** | `PUT`       | Replace a model configuration    |
| **Update (partial)** | `PATCH`     | Change one model setting         |
| **Delete**           | `DELETE`    | Remove a model                   |

For example:

```text
POST   /models       → Create a model
GET    /models/42    → Read model 42
PUT    /models/42    → Replace model 42
PATCH  /models/42    → Update part of model 42
DELETE /models/42    → Delete model 42
```

> **Mental Model**
>
> **CRUD describes what operation you want to perform.**
>
> **HTTP methods describe how you communicate that operation to the server.**

CRUD is a fundamental backend concept because most APIs ultimately involve creating, reading, updating, or deleting resources.

## Common Misconceptions

### "The body always contains JSON."

No. The body can contain:

- JSON,
- images,
- audio,
- video,
- PDFs,
- binary files,
- form data.

### "GET requests usually need a body."

Usually, they do not.

`GET` requests normally send information through the URL and query parameters.

### "Headers contain the main data."

No.

Headers describe the request. The body usually carries the main payload.

## Chapter Summary

- Every HTTP request has a defined structure.
- The four main parts are **method**, **URL**, **headers**, and **body**.
- The method tells the server what action to perform.
- The URL identifies the endpoint or resource.
- Headers provide metadata about the request.
- The body carries the data for processing.
- AI applications use these same parts to send text, images, audio, documents, and prediction inputs.

## Next Chapter

Now that we understand HTTP requests, the next question is:

> **How should we design APIs that are intuitive, consistent, and easy to use?**
