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

The **URL (Uniform Resource Locator)** tells the client **where** to send the request.

Think of a URL as the complete address needed to reach a specific resource on a server.

Example:

```text
https://api.company.com/predict
```

Let's break it down:

```text
https://api.company.com/predict
|       |               |
|       |               |-- Path / Endpoint
|       |
|       |-- Domain Name
|
|-- Protocol
```

### Protocol

The **protocol** defines **how** the client and server communicate.

Examples:

- `http://`
- `https://`

In production, APIs almost always use **HTTPS** because it encrypts data during transmission.

### Domain Name

A **domain name** is the human-readable name of a server on the internet.

Examples:

```text
google.com
openai.com
api.company.com
```

Computers actually communicate using **IP addresses** such as:

```text
142.250.183.46
```

A **DNS (Domain Name System)** converts the domain name into the corresponding IP address so the request reaches the correct server.

> **Mental model**
>
> A domain name is like a person's name in your phone contacts.
> An IP address is like their phone number.
> DNS is the contact list that looks up the number for you.

### Path (Endpoint)

The **path**, often called an **API endpoint**, identifies the specific resource or functionality on the server.

Examples:

```text
/predict
/models
/users
/health
/login
```

The same server can expose many different endpoints.

For example:

```text
https://api.company.com/models
https://api.company.com/predict
https://api.company.com/login
```

All three requests go to the **same server** (`api.company.com`), but each endpoint performs a different task.

### URL vs Domain Name

These two terms are often confused.

| Domain Name | URL |
| --- | --- |
| Identifies the server | Identifies the complete resource |
| Example: `api.company.com` | Example: `https://api.company.com/predict` |
| Does not include protocol or endpoint | Includes protocol, domain, and path |

A URL contains several parts, and the **domain name is only one of them**.

### Path Parameters

Path parameters identify a specific resource.

```text
GET /users/42
GET /models/resnet50
```

Here:

- `42` identifies a particular user.
- `resnet50` identifies a specific model.

### Query Parameters

Query parameters provide additional options without changing the resource itself.

```text
GET /models?type=vision&limit=10
```

Here:

- `type=vision` filters the results.
- `limit=10` limits the number of returned models.

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

CRUD is an acronym for the four basic operations that most applications perform on data:

| CRUD | Meaning | Example |
| --- | --- | --- |
| **Create** | Add new data | Create a new model configuration |
| **Read** | Retrieve existing data | Get model details |
| **Update** | Modify existing data | Change model settings |
| **Delete** | Remove existing data | Delete a model |

Think of CRUD as describing **what you want to do** with a resource.

HTTP methods are the standard way we express these operations over the web.

The mapping looks like this:

| CRUD operation | HTTP method | Example |
| --- | --- | --- |
| Create | `POST` | Create a new model config |
| Read | `GET` | Read model details |
| Update (replace) | `PUT` | Replace model config |
| Update (partial) | `PATCH` | Change one setting |
| Delete | `DELETE` | Remove a model |

> **Mental model**
>
> **CRUD describes the operation. HTTP methods are how that operation is communicated to the server.**

For example:

```text
POST   /models      -> Create a model
GET    /models/42   -> Read model 42
PUT    /models/42   -> Replace model 42
PATCH  /models/42   -> Update part of model 42
DELETE /models/42   -> Delete model 42
```

You'll see CRUD in almost every backend interview because most APIs are built around these four operations.


## CRUD Mapping

HTTP methods often map to **CRUD** operations:

| CRUD operation | HTTP method | Example |
| --- | --- | --- |
| Create | `POST` | Create a new model config |
| Read | `GET` | Read model details |
| Update / replace | `PUT` | Replace model config |
| Update / modify | `PATCH` | Change one setting |
| Delete | `DELETE` | Remove a model |

You will see this mapping often when designing APIs.

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
