# Pyspark


#Project : Word Count and Word Cloud using Pyspark

#Usage Word Count: 
1. To run the program we have used jupyter notebook : " Spark.ipynb "
2. We ran each cell from the start to prevent any errors.
3. We used the data from tweets. 
4. Collected data with respective characters such as @ or those having numbers greater than 10 etc.


#Usage Word Cloud:
1. To run the program we have used jupyter notebook : " Spark.ipynb "
2. We ran each cell from the start to prevent any errors.
3. We used the data from tweets. 
4. For the world Cloud we have used the matplot library .
5. We set the required background and respective features to get the desired word cloud. 
6. We ran the code with different color parameters. 


#Dependency :
1. Python 3.6 or greater
2. Spark with the library pyspark
3. numpy
4. pandas
5. matplotlib
6. worcloud


#Refrences:
1. Google, Python respositary, Spark, Youtube.
2. Assistance from Ma'am when we had errors while running the Word Cloud code.

#Code Explanation

findspark.init(), you can ensure that Spark is properly configured and available for use in your Python environment before starting to work with Spark APIs and functionality.

findspark.init('C:/spark3') initializes Spark by specifying the path to the Spark installation directory. In this case, it sets the path to 'C:/spark3', which is the directory where Spark is installed on the local system.

from pyspark.sql import SparkSession imports the SparkSession class from the pyspark.sql module. SparkSession is the entry point for using Spark's SQL functionality.

spark = SparkSession.builder.getOrCreate() creates a SparkSession object named spark. The SparkSession.builder is a builder pattern used to configure and create the SparkSession object. The getOrCreate() method either retrieves an existing SparkSession or creates a new one if it doesn't already exist.

sc = spark.sparkContext, sc is a variable that represents the SparkContext object associated with the SparkSession object spark. sc is the variable referring to it 

in_text = sc.textFile('tweets.txt') reads the content of a text file named 'tweets.txt' and creates an RDD (Resilient Distributed Dataset) named in_text using the textFile() method provided by the SparkContext object sc.

in_text.collect() displays the content of text files.

counts = in_text.flatMap(lambda x: x.split(' ')) \
    .filter(lambda x: x.startswith('@')) \
    .map(lambda x: (x, 1)) \
    .reduceByKey(lambda x, y: x+y)

The flatMap() function is used to generate a new RDD with each word as a separate element

filter() function retains only those elements in the RDD that satisfy the given condition.

map(lambda x: (x, 1)): This transformation transforms each word into a key-value pair, where the word itself becomes the key, and the value is set to 1.

reduceByKey(lambda x, y: x+y): This action performs a reduction operation on the key-value pairs, grouping the words by key (word) and summing up their corresponding values.

We are storing the final result in counts 


wordcloud = WordCloud(background_color='black', width=800, height=400, font_path="./arial.ttf").generate_from_frequencies(counts_dict)
plt.figure(figsize=(10, 6))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.show()

setting up the font and dimensions for generating the word cloud 
