# REST API

**REST** or RESTful API design (Representational State Transfer) is designed to take advantage of existing protocols. While REST can be used over nearly any protocol, it usually takes advantage of HTTP when used for Web APIs. 

If you don't know what API's are read them about [here.](https://github.com/Hardikb19/IECSE-Dev-Winter-19/wiki/Understanding-APIs)

There are some protocols that need to be followed while making **REST API's** -

1. Each operation uses its own HTTP method:

```

GET - getting the information
POST - creation
PUT - update (modification)
DELETE - removal

```

All these methods (operations) are generally called [CRUD.](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)

2. All resources in REST are entities. They can be independent like:

```

GET /members - get all members
GET /member/123 - get a particular member with id = 123

```
3. Information is transferred using some light-weight representation of the data like **XML** or **JSON**.

4. The most important of this design is the [Client-Server](https://www.geeksforgeeks.org/client-server-model/) model, where we separate the user interface from the backend.

Further Reading - https://www.mulesoft.com/resources/api/what-is-rest-api-design

# Flask and Python


[Check it out here.](https://pythonprogramminglanguage.com/flask-hello-world/)

This is the most basic flask application.

```python
from flask import Flask # Here we import the flask package into our python application.

app = Flask(__name__) # Defines an instance of a flask application.

@app.route('/') # This an example of a decorator, which adds extra functionality to the index function.
def index():
    return 'Hello World from Python Flask!' 

app.run(host='0.0.0.0', port=5000) # Runs the application on localhost at port 5000
```

Now if you run this python script and go to `localhost:5000/` in your browser you can see the above text that we return from our function.

To run this script 
```
python3 app.py
```

Decorators are very powerful and useful tool in Python since it allows programmers to modify the behaviour of function or class. Decorators allow us to wrap another function in order to extend the behaviour of the wrapped function, without permanently modifying it.

`@app.route('/')`

This line is a decorator when we go to _localhost:5000/_ we are routed to this function `def index():`, so basically we added some functionality without editing or changing our main function.

### Routing 

Any web application can have multiple routes. In flask, it's mapping a given URL to a python function.

```python
@app.route('/hello')
def helloIndex():
    return 'Hello World from a different route!'
```

Here the route is `('/hello')` and it is mapped to a function that is `def helloIndex():`

# Requests in Flask 

# POST requests, JSON and Data Transfer

> Further to Read : [HTTP Methods, GET & POST](https://www.tutorialspoint.com/http/http_methods.htm).

Simply put, the **GET** method is used to retrieve information from the given server whereas a **POST** request is used to send data to the server. \
We have been dealing with simple GET requests up till now. But for our future mobile app to change dynamically we would like to interact with the server using a combination of GET & POST requests, whatever the situation demands.

A simple example would be if wanted to take user feedback, we would need to transfer feedback data to the server. We would use a POST request to transfer the form data to the server.

## POST requests in Flask

```python

from flask import Flask # Import Flask

app = Flask(__name__) # Initialize Flask App

@app.route('/' , methods=['POST']) # Decorator, wrapping function homepage 
def homepage():
    return "My First POST Request"

if __name__ == '__main__':
    app.run( host='0.0.0.0' , port=5000 ) # The Flask App will run on localhost, at port 5000
```
As simple as that, an additional parameter "methods" defining the methods list. \
We can also have a **hybrid mechanism** where the same route can receive GET & POST requests. To ascertain whether the current request is a GET or a POST request we make use of the module **request**.

```python
from flask import Flask, request # Import Flask

app = Flask(__name__) # Initialize Flask App

@app.route('/' , methods=['POST','GET']) # Decorator, wrapping function homepage 
def homepage():
    if request.method == "POST":
        return "My First POST Request"
    else:
        return "My First GET Request"

app.run( host='0.0.0.0' , port=5000 ) # The Flask App will run on localhost, at port 5000
```

## JSON

The data transferred to and from the client and server can only be text. \
JSON is text, and we can convert any JavaScript object into JSON, and send JSON to the server.
We can also convert any JSON received from the server into JavaScript objects. \
This way we can work with the data as JavaScript objects, with no complicated parsing and translations.

The following example shows how to use JSON to store information related to books based on their topic and edition,
```javascript
{
   "book": [
	
      {
         "id":"01",
         "language": "Java",
         "edition": "third",
         "author": "Herbert Schildt"
      },
	
      {
         "id":"07",
         "language": "C++",
         "edition": "second",
         "author": "E.Balagurusamy"
      }
   ]
}
```
Since the JSON format is text only, it can easily be sent to and from a server, and used as a data format by any programming language.
JavaScript has a built-in function to convert a string, written in JSON format, into native JavaScript objects:
JSON.parse()
So, if you receive data from a server, in JSON format, you can use it like any other JavaScript object.

Find out more about them [here](https://www.tutorialspoint.com/json/json_overview.htm).

## Data Transfer to and from server

### TO
To convert Dictionaries in Python to transferable JSON strings and vice versa we make use of the **json** module in Python.
```python
import json
data = { "data" : 1 }
_data = json.dumps(data)

data = '{ "data" : 1 }'
_data = json.loads(data)
```
\
For a POST request, we receive a json object using the **request** module. 
```python
from flask import Flask, request # Import Flask

app = Flask(__name__) # Initialize Flask App

@app.route('/' , methods=['POST']) # Decorator, wrapping function homepage 
def homepage():
    content = request.json
    return content["data"]

app.run( host='0.0.0.0' , port=5000 ) # The Flask App will run on localhost, at port 5000
```

We can test it using Postman,
1) We set the Content-Type header to application/json
![](https://i.imgur.com/DiQyAwU.png)
2) We write the textual data in json format
![](https://i.imgur.com/23BYdrk.png)
3) When we make the request we see that the above python code works
![](https://i.imgur.com/N104tkr.png)

### FROM

To respond in json format we use the Response object, along with [HTTP Status Codes](https://www.tutorialspoint.com/http/http_status_codes.htm)

```python
from flask import Flask, request, Response # Import Flask

app = Flask(__name__) # Initialize Flask App

@app.route('/' , methods=['POST']) # Decorator, wrapping function homepage 
def homepage():
    content = request.json
    if "data" in content: # check if key exists in dictionary
        return Response( "{\"did_we_receive\":\"true\"}" , status = 200 , mimetype='application/json' )
    else:
        return Response( "{\"did_we_receive\":\"false\"}" , status = 200 , mimetype='application/json' )        

app.run( host='0.0.0.0' , port=5000 ) # The Flask App will run on localhost, at port 5000
```

If we test the above code in Postman,
![](https://i.imgur.com/yg2sktB.png)
we get the response,
![](https://i.imgur.com/r9LwUCe.png)
and if we try sending an empty object
![](https://i.imgur.com/lZprU8r.png)
we get,
![](https://i.imgur.com/lHKTp9s.png)

## Debug

The additional parameter **debug** is used to start the app in debugger mode. Among many things, in the Debugger Mode you would not need to restart the app every time you make some changes. You are welcome to explore more about the Flask Debugger if you're interested.

**Additional Links**

* [Flask HTTP Methods](https://www.tutorialspoint.com/flask/flask_http_methods.htm)
* [JSON](https://www.tutorialspoint.com/json)
* [Postman](https://www.guru99.com/postman-tutorial.html)
* [Flask Request and Response](http://flask.pocoo.org/docs/1.0/api/#flask.request)
* [Python Dictionaries & JSONs](https://www.w3schools.com/python/python_json.asp)

# Node.JS

The basics of backend development remain the same like building REST API's, using JSON for data transfer and Postman for API testing. 
For Node just go through the videos and understand the syntax of the language and build some applcations which would give you a better idea. 

[Node.JS Basics](https://www.youtube.com/watch?v=fBNz5xF-Kx4)
[Express](https://www.youtube.com/watch?v=L72fhGm1tfE)


