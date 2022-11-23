> Difference between Flask, Django and Tornado?

> What is the g object in Flask? How does it differ from the session object?

Flask’s g object is used as a global namespace for holding any data during the application context. g object is not appropriate for storing the data between requests. The letter g, in a sense, stands for global.

In situations, when you need to keep global variables during an application context, then rather than creating your global variable, it is best to use the g object as each request in Flask has a separate g object. Flask’s g object saves us from accidental modifications of self-defined global variables.

> What is the application context in Flask?

The application context in Flask relates to the idea of a complete request/response cycle. It keeps a track of application-level data during a request or a CLI command. We make use of g and current_app proxies to achieve the same.

There are situations when it is difficult to directly import the Flask app, such as in the case of a Flask extension or a Blueprint. Moreover, introducing applications may raise the problem of circular imports.

Flask pushes the application context with each request. Therefore, during a request, functions have access to g and current_app to overcome the problem highlighted above.


> In what ways can you connect to a database in Flask?

Flask works with most of the RDBMSs, such as PostgreSQL, SQLite, and MySQL. However, to connect with databases, we must make use of the Flask-SQLAlchemy extension.

It makes database interaction and management easy during development without the need to write raw SQL queries. Moreover, raw SQL queries are prone to SQL injection attacks. For working with No-SQL data stores such as MongoDB, we can make use of the Flask-MongoEngine extension.

> How to create a RESTful application in Flask?

Flask-API
Flask-RESTful
Flask-RESTX
Connexion
However, we need to evaluate these extensions and see which one is more appropriate based on our project requirements and constraints.

> How to debug a Flask Application?

Flask comes with a development server, and the development server has a Debug Mode. The Debug mode can be set to true when we call the run method of the Flask Application object.

Given below is an example.
```python
from flask import Flask 
app = Flask(__name__)
app.run(host='127.0.0.1', debug=True)
```
However, we need to disable the debug mode before deploying the application on production to avoid full stack trace display in the browser. Such a stack trace can reveal a lot of essential details and is prone to exploitation by bad actors.

Further, we can make use of the Flask-DebugToolbar extension for easy debugging in the browser. We can also make use of Python’s pdb module and the debugging statement import pdb;pdb.set_trace() to support the debugging process.
