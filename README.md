# sql-injection-hack
This is simple flask app to show how you can use sql injecttion in simple table with users and password

```
from flask import Flask, jsonify, request
import psycopg2
# import requests
app = Flask('app')


@app.route('/', methods=['GET', 'POST'])
def hello_world():
    rows = []
    print("test")
    # if request.args.get('email') and request.args.get('password'):
    if request.form['email'] and request.form['password']:
        name = request.form['email']
        print(name)
        con = psycopg2.connect(database="",
                               user="",
                               password="",
                               host="",
                               port="5432")
        print("Database opened successfully")
        cur = con.cursor()

        login = request.form['email']
        password = request.form['password']
        print("SELECT * from USERS where email=" + login + " and password=" +
              password + "")
        cur.execute("SELECT * from USERS where email=" + login +
                    " and password=" + password + "")
        rows = cur.fetchall()
        print(rows)

    return jsonify({'data': rows})
    # return '<h1>Hello, World!</h1>'


app.run(host='0.0.0.0', port=8080)

    
    
```
