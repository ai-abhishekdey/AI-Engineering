# Chapter 02: How Does Your Request Reach the AI Model?

## Objective

By the end of this chapter, you should understand:

- what happens when a user clicks **Predict**,
- the difference between a **client** and a **server**,
- why the model usually runs on the server.

> **Core idea**
>
> In a production AI application, the user does not talk directly to the model. The user's device talks to a server, and the server talks to the model.

## The Big Question

Imagine you built an **image classification application**.

A user opens the app, uploads an image, and clicks **Predict**.

A few seconds later, the prediction appears.

What happened during those few seconds?

## 1. Two Computers Are Talking

When a user uses an AI application, two sides are usually involved:

- the user's device,
- the AI server.

Think of it like ordering food at a restaurant.

- You do not walk into the kitchen.
- You tell the waiter what you want.
- The waiter talks to the chef.
- The chef prepares the food.
- The waiter brings the result back to you.

In the same way, the user does not directly access the AI model.

```text
User's Device
      |
      v
Internet
      |
      v
AI Server
```

> **Key idea**
>
> The user's device and the AI server communicate through the Internet.

## 2. Client and Server

The two most important words here are **client** and **server**.

### Client

A **client** is anything that asks for a service.

Examples:

- web browser,
- mobile app,
- desktop application,
- another backend service,
- another AI service.

### Server

A **server** is anything that provides a service.

Examples:

- AI application,
- authentication service,
- database server,
- file server.

> **Mental model**
>
> The **client asks**. The **server answers**.

## 3. What Happens When You Click Predict?

Here is the basic flow:

```text
User clicks Predict
        |
        v
Browser sends request
        |
        v
Internet carries request
        |
        v
AI server receives request
        |
        v
Model makes prediction
        |
        v
Server sends response
        |
        v
Browser displays result
```

The important point is simple:

> **The browser usually does not run your model. The server does.**

## 4. Why Does the Server Run the Model?

Beginners often ask:

> **Why not run the model directly inside the browser?**

Sometimes this is possible, but most production AI systems run models on servers because:

- models can be **large**,
- inference may need **GPUs** or powerful CPUs,
- server-side execution is easier to **secure**,
- many users can share the same deployed model,
- updates can happen in one place instead of every user's device.

This gives the team more control over performance, security, and reliability.

## Chapter Summary

- A **client** requests a service.
- A **server** provides a service.
- In AI applications, the model usually lives on the **server**.
- When a user clicks **Predict**, the client sends a request to the server.
- The server calls the model and sends the result back.
- The Internet enables this communication.

## Next Chapter

Now we know **who is talking**:

- client,
- server.

Next, we need to understand **how they communicate**.

That brings us to **HTTP**.
