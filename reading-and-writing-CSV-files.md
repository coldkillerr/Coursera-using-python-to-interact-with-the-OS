<h1> Reading and Writing CSV files </h1>

<h2> What is CSV ?</h2>

CSV or comma separated values is a very common data format used to store data
as segment of text separated by commas.
In the Python standard library, you'll find classes and modules for
working with many of these data formats, including CSV and HTML. 

Module for manipulating CSV files is : `csv`

<h2> Reading CSV Files </h2>

<h3> Creating instance of csv class </h3>

```python3
>>> f=open('new_csv.txt','w')
>>> csv_f=csv.reader(f)
>>> 
```



