# Assignment 1 for Business Intellegence Course

### 1) List the all files that this program generates.

Running the file generates:
* price_list.csv 
* price_list.txt
* prices.png
* avg_price.txt

### 2) Describe which types of files this program generates and attach the contents of each file together with its name to your solution.

See above(q1).

### 3) What is the output of this program?

The output is the calculated average price derived from the data: 
`3307228.119047619`

### 4) Describe in natural language -- line-by-line of code -- what the Python script is doing.

`We first define a multiline github url variable. 

We then use a function to return and save the basename as a variable to be used as a filename later.

Then we contruct a full pathname out of the partial pathnames.

After that we call our download method to download and write a file from our previous url variable.

Then we save a file name as a variable to be used later.

The next line involves using os.getcwd to obtain our current directory and then using the same function as earlier to contruct a full path.

We now plug in our input and output paths to our "generate_csv" function. This reads our generated txt file created earlier and then makes some changes to the seperators and titles. Then we plot this data into a csv file. The generator function also has some addition logic if the OS being used is a window. 

Now we read from our csv file and generate a list of tubles using the zip method. This is then saved as a variable. 

Now we calculate the average price using this variable we just saved. First using the zip method again and then the statistic.mean. 

We also using the variable when we print it and finally use it with a .scatter to generate and save a scatter plot file using this condensed data.`


### 5) Write (code) a function in the assignment_1.py file, which plots a histogram of the price data, with -- say -- 7 bins in the histogram.

See histo.png


### 6) Write (text) a sentence into the assignment_1.py about the result of the histogram.

![histo.png](https://github.com/grimetone/BI/tree/master/Assignment1/histo.png)