#### Resource
A resource is a thing or a type of information that can be accessed through URLs. The URLs used to access resources are accompanied by a method that specify how to interact with the resources. These include the following:
- GET: Read
- POST: Create
- PUT: Update
- Delete: Remove
#### Endpoint
An endpoint includes the whole path to a resource. It consists of the following parts:
- The **base path** refers to the common path of the API. For example, `https://apiserver.com`
- The **end path** refers to the resource itself. For example, `/home`
- The part of an endpoint after the `?` contains query string parameters for the endpoint. For example, `?limit=5&format=json`. Query strings can contain multiple parameters, separated by `&`
#### Method
A method specifies how an endpoint interacts with a resource. Common methods include the following:
- GET: Read
- POST: Create
- PUT: Update
- Delete: Remove
#### Request
A request can best be described as one computer asking another for a resource. In the case of REST APIs, a request is sent from a client computer to a server via HTTP.
#### Response
A response is what the server sends to the client on the back of a request made by the client. Simply put, it includes the resource requested by the client.
#### Status code
A status code is a three-digit number that a server sends back to tell you what happened to your request. Every HTTP response is returned with a status code. At a high level, status codes include the following:
- 200: Success
- 300: Redirect
- 400: Bad request
- 500: Server error