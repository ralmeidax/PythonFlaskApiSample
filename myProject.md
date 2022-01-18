# Testando outro exemplo acima com restx

## 1) Criar pasta do projeto

~~~shell
mkdir 06-FlaskApiRestX
cd 06-FlaskApiRestX
~~~



## 2) Criar e ativar máquina virtual

~~~shell
python3 -m venv venv
. venv/bin/activate
~~~



## 3) Instalar as bibliotecas necessárias

### 3.1) Flask

~~~shell
python3 -m pip install Flask
~~~



### 3.2) Flask_RestX

~~~shell
python3 -m pip install flask_restx
~~~



## 4) Estrutura de diretórios

- app.py
- src
  - controllers
    - books.py
  - server
    - instance.py



### 4.1) 📂 server/instance.py

~~~python
from flask import Flask
from flask_restx import Api

class Server():
    def __init__(self, ):
        self.app = Flask(__name__)
        self.api = Api(self.app,
            version='1.0',
            title='Sample Book Api',
            description='A simple book API',
            doc='/docs'
        )
    
    def run(self, ):
        self.app.run(
            debug=True
        )

server = Server()
~~~



### 4.2) 📂 controller/books.py

~~~python
from flask import Flask
from flask_restx import Api, Resource

from src.server.instance import server

app, api = server.app, server.api

books_db = [
    {'id':0, 'title':'war and peace'},
    {'id':1, 'title':'Clean code'},
]

@api.route('/books')
class BookList(Resource):
    def get(self, ):
        return books_db
    
     def post(self, ):
        response = api.payload
        books_db.append(response)
        return books_db
~~~



### 4.3) 📂 app.py

~~~python
from src.server.instance import server

from src.controllers.books import *

server.run()
~~~



### 