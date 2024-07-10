# Writing a RESTful API Client in Go

It is common practice for products to list their own set of client libraries for developers to incorporate into their projects. 
A RESTful API client library provides a set of tools and functions that allow applications to interact with a RESTful API, facilitating tasks such as sending requests, handling responses, and managing authentication.

The objective of this series is to document the process of building a RESTful API client library from scratch. 
Sometimes, official client libraries are not available or are outdated, which can hinder development efforts. 
In this series of blogs, I will share my implementation of a client library for a fitness application called Strava.

While many practices discussed may not represent the perfect way of implementing things, this is a learning experience for everyone involved. 
This project will be developed in Go, and I hope it serves as a valuable resource for those looking to understand the intricacies of building 
their own API client libraries.

You can check the full repository here! [GoStrava](https://github.com/guisaez/gostrava)

Are you ready? Let's start!

### Creating a Client

```go
type Client struct {
    // Base URL user for API request
    BaseURL *url.URL

    // HTTP Client used to communicate with the server
    httpClient *http.Client
}
```