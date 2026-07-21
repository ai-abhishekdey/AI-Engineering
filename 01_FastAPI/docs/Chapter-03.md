# Chapter 03: How Do Clients and Servers Communicate?

## Objective

By the end of this chapter, you should understand:

- why computers need a **communication protocol**,
- what **HTTP** is,
- what **HTTPS** adds,
- why every FastAPI application depends on HTTP.

## The Big Question

In the previous chapter, we learned that a **client** sends a request to a **server**.

But how do two different computers understand each other?

They need a shared set of rules.

That shared set of rules is called a **protocol**.

> **Mental model**
>
> A protocol is a common language that computers agree to use.

## What Is a Protocol?

Imagine two people trying to communicate.

- One speaks only English.
- The other speaks only Japanese.

Both people may be intelligent, but they cannot understand each other without a shared language.

Computers have the same problem.

A browser, mobile app, and server may all be built with different technologies, but they can still communicate if they follow the same protocol.

## What Is HTTP?

**HTTP** stands for **HyperText Transfer Protocol**.

Despite the name, HTTP is not only for web pages anymore. It is used to transfer many kinds of data:

- web pages,
- images,
- audio,
- video,
- JSON data,
- AI requests,
- AI responses.

Whenever your browser talks to an AI application, it is usually using **HTTP**.

## HTTP Is a Conversation

Think of HTTP as a structured conversation between a client and a server.

The client asks:

> Can you classify this image?

The server responds:

> It is a Golden Retriever. Confidence: 98%.

HTTP does not define what your AI model does. It defines how the client and server exchange messages.

## Request and Response

Every HTTP interaction follows the same pattern:

```text
Client
  |
  v
HTTP Request
  |
  v
Server processes request
  |
  v
HTTP Response
  |
  v
Client
```

The client starts the conversation. The server sends the response.

> **Key pattern**
>
> Request -> Processing -> Response

You will see this pattern everywhere in backend engineering.

## AI Example

Suppose a user uploads an image for object detection.

```text
Browser uploads image
        |
        v
HTTP Request
        |
        v
AI Application
        |
        v
Object Detection Model
        |
        v
HTTP Response
        |
        v
Detected objects shown in browser
```

The AI task can change:

- Image Classification
- OCR
- Speech Recognition
- RAG
- AI Chat

But the communication pattern stays the same.

## Why HTTPS?

If HTTP already allows computers to communicate, why do we need **HTTPS**?

Think of sending a message on a postcard.

- Anyone handling the postcard can read it.
- Someone might even modify it.

Now imagine putting the same message inside a sealed envelope.

- People can still deliver it.
- But they cannot read or change what is inside.

> **Simple analogy**
>
> HTTP is like a postcard. HTTPS is like a sealed envelope.

## What Is HTTPS?

**HTTPS** stands for **HyperText Transfer Protocol Secure**.

It is HTTP protected by encryption.

```text
HTTP  = data sent in plain text
HTTPS = HTTP + encryption
```

With HTTPS, the data is encrypted before it leaves the user's device. Only the intended server can read it.

This matters especially for AI applications because users may upload sensitive data:

- medical images,
- voice recordings,
- financial documents,
- identity documents,
- login credentials.

## What HTTPS Protects

HTTPS provides three important protections:

| Protection | Meaning |
| --- | --- |
| Confidentiality | Others cannot read the data. |
| Integrity | Data cannot be modified during transmission. |
| Authentication | The client can verify it is communicating with the correct server. |

> **Important**
>
> HTTPS is not a completely different idea from HTTP. It is HTTP made secure using encryption.

## Where FastAPI Fits

FastAPI is **not** a communication protocol.

FastAPI is a Python framework for building applications that:

- receive HTTP requests,
- run your application logic,
- call models or services,
- send HTTP responses.

In development, you may access your app using **HTTP**.

In production, applications are usually exposed through **HTTPS** to protect user data.

## Chapter Summary

- Computers communicate using **protocols**.
- **HTTP** defines how clients and servers exchange requests and responses.
- Every HTTP interaction follows: **Request -> Processing -> Response**.
- **HTTPS** is HTTP protected by encryption.
- FastAPI helps you build applications that receive HTTP requests and return HTTP responses.

## Next Chapter

Now that we know clients and servers communicate using HTTP, the next question is:

> **What exactly is inside an HTTP request?**
