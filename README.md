# STOCK

To run the Project:
uvicorn main:app --reload


#These are my Notes for Reference to Follow steps to create  project
FOR dependency use requirements.txt
pip install -r requirements.txt

create virtual env:
py -m venv env
activate using:
.\env\Scripts\activate

app.get("/") means get request defined below which returns json


Using POSTMAN for request
http://127.0.0.1:8000/stock
KEY IS symbol VALUE is VB(anything)


Create folder templatee
layout.html
dashboard.html


home.html will extend layout.html


Now to support it we need to import jinja2 template.
After importing we need to say where this templates exists below API()


I have used SemanticUI for styling
In getting started recepies section 
Component script with link 
and in getting started Including in HTML Section: copy only script



now in recipies 
Table script

In script above of table: Add Input Script(2 times) 1 for P/E 2 for Divident yield 
add check box for filtering


now in Semantic page (modules) checkbox

now button for filter change to primary(for blue colour)


Now structure of DB
I have used SQLalchemy
go to SQL( relational) db in fastapi docs

database.py
sqlalchemy copy paste stocks.db


copy models of SQL Alchemy
create models.py and paste thr
modify accordingly 
now search in docs create_all 
copy paste that in starting of main.py...need to import engine,models i.e from models.py
import SessionLocal, engine
check db now

sqlite3 stocks.db
.schema
select * from stocks;
insert into stocks (symbol) values('AAPL')
check using select * from stocks;

now take all component and wirethem together
1)Pyndantic-To define structure of http request
2) Dependency injection
3)background task to fetch data

we want user to give stock symbol and get data
we use padantic


For Dependency Injection we need to add try catch method and import Depends 

mention db inside try catch like 
def get_db():
	try:
		db = SessionLocal()
		yield db
	finally:
		db.close()


at create stock
	db.add(stock)
	db.commit()
this will add data to db when we post in postmanagent

backgrnd task - To add bckgrnd task(background_tasks.add_task(fetch_stock_data, stock.id))..create new func fetch bckgrnd task func..

def fetch_stock_data(id: int):

    db = SessionLocal()

    stock = db.query(Stock).filter(Stock.id == id).first()

    
    stock.forward_pe = 10


    db.add(stock)
    db.commit()

then post stock

USE Async infront of Function WITH BACKGROUND TASK 

For real data have yfinance import it..
modify accordingly inside function

we will get all data from yfinance
