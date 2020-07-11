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

<h3> Iterating through CSV </h3>

```python
>>> csv_f=csv.reader(open('new_csv.txt'))
>>> for row in csv_f :
...     print(row)
... 
['Nishit ', ' 1 ', '2']
['Ramesh ', ' 2 ', '3']
>>> 
```
The elements of rows are interpreted as lists in python for csv files

<h2> Generating CSV files </h2>

```python3
>>> lists=[[1,2,3],[4,5,6],[7,8,9]]
>>> import csv
>>> with open('hosts.csv','w') as file :
...     writer=csv.writer(file)
...     writer.writerows(lists)
... 
>>> 
```
```shell
$ cat hosts.csv
1,2,3
4,5,6
7,8,9
```
`writer=csv.writer()` is used to create a writer .

`writer.writerows()` is used to write all data to the file row by row whereas `writer.writerow()` writes on row at a time.

<h2> Reading CSV files as dictionaries </h2>

For this we use `DictReader()`

```python3
import csv
with open('csv_dict.csv') as file:
	reader=csv.DictReader(file)
	print(type(reader))
	for row in reader:
	
		print('row : {}'.format(str(row)))
		print('Name :{} ,\n rollNumber {} ,\n Branch {}\n'.format(row['Name'],row['RollNum'],row['Branch']))
```
The dictreader creates seperate dictionaries of each row.
And they can be called by using elements of `first row` as the `keys`






