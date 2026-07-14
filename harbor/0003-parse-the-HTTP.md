# Harbor Journal 003

**Date:** July 14, 2026

## Today's Goal

Continue the implementation of Harbor by taking the first step toward understanding HTTP requests instead of only reading and displaying them.

## What Was Done

Today's work focused on parsing the first line of an HTTP request.

The request line is now extracted and interpreted, allowing Harbor to identify:

* HTTP Method
* Requested Path
* HTTP Version

For example, the request:

```text
GET /posts HTTP/1.1
```

is now interpreted as:

```text
Method: GET
Path: /posts
Version: HTTP/1.1
```

The HTTP response was also improved by calculating the `Content-Length` automatically instead of using a hardcoded value.

## Project Organization

Today Harbor received its first internal module.

The request parsing logic was moved from `main.rs` into a dedicated `request.rs` module.

This was the first architectural separation of the project.

The goal was not simply to reduce the size of `main.rs`, but to separate responsibilities clearly.

Current responsibility split:

* `main.rs` is responsible for the application flow.
* `request.rs` is responsible for interpreting the request line.

This follows Harbor's philosophy of introducing abstractions only when they solve a real problem.

## Learning

Today's session introduced several important Rust concepts:

* Modules
* Public functions (`pub`)
* Tuples as return values
* Tuple destructuring
* Function signatures
* Borrowed string slices (`&str`)
* Iterators
* `lines()`
* `split_whitespace()`

One particularly interesting discovery was how Rust allows functions to return tuples naturally, making it possible to return multiple related values without creating unnecessary structures.

Another important lesson was understanding that those returned values are not copies, but borrowed slices pointing directly into the original request buffer.

## Architecture Decisions

The first module separation reinforced one of Harbor's core principles:

> Separate code by responsibility, not by file size.

Modules should only be introduced when they represent a clear concept within the application.

Keeping the project simple and understandable remains more important than aggressively reducing the number of lines in each file.

## Next Step

The next milestone will be expanding Harbor's HTTP parser.

Instead of extracting only the request line, Harbor will begin understanding the remaining HTTP headers, creating the foundation for a complete `Request` structure.

## Thoughts

Today's work felt like an important transition.

Yesterday Harbor learned how to receive data.

Today it began to understand what that data means.

That small difference represents the beginning of Harbor's own HTTP parser, one of the core pieces of the entire project.
