# big-data-class

## Lesson 1 ICP
First, I downloaded the 2 data files, shakespeare.txt and word_list.txt.
I did these commands:
* `hdfs dfs -put shakespeare.txt /user/cloudera/adam/`
* `hdfs dfs -appendToFile word_list.txt /user/cloudera/adam/shakespeare.txt`
* `hdfs dfs -cat /user/cloudera/adam/shakespeare.txt | head -n 5`
* `hdfs dfs -cat /user/cloudera/adam/shakespeare.txt | tail -n 5`
* `touch localfile`
* I then pasted some lorem ipsum text into localfile
* `hdfs dfs -appendToFile localfile /user/cloudera/adam/shakespeare.txt`

## Lesson 2 ICP
For items 1 and 2, I added the code for the WordCount.jar and exported it. I created the necessary text input files.
I did these commands:
* `hdfs dfs -put wordcount.txt input/`
* `hadoop jar /home/cloudera/adam/WordCount.jar input/wordcount.txt output`
* `hdfs dfs -ls output`
* `hdfs dfs -cat output/part-r-00000`

For item 2, I made a new code file, ACount.jar. It is also under the lesson 2 folder.
* `hadoop jar /home/cloudera/adam/ACount.jar input/wordcount.txt output-a`
* `hdfs dfs -ls output-a`
* `hdfs dfs -cat output-a/part-r-00000`

For the bonus item, I made a new java class, copied in the WordCount file, and edited the Tokenizer to check for primes when writing to the file.
The file is in this repo under 'Lesson 2'. I then ran these commands:
* `hdfs dfs -put numbers.txt input/`
* `hadoop jar /home/cloudera/adam/PrimeCount.jar input/numbers.txt output-num`
* `hdfs dfs -ls output-num`
* `hdfs dfs -cat output-num/part-r-00000`

## Lesson 3 ICP
I created the necessary files (found in the MatrixMultiplication folder here), and exported the project as a jar. I created the input files and copied them all to the cloudera VM.
I did these commands:
* `hdfs dfs -put M /home/cloudera/input/`
* `hdfs dfs -put N /home/cloudera/input/`
* `hadoop jar MatrixMultiplication.jar MatrixMultiplication /home/cloudera/input /home/cloudera/output`
* `hdfs dfs -ls /home/cloudera/output`
* `hdfs dfs -cat /home/cloudera/output/part-r-00000`

![image](https://i.imgur.com/8V8QTuy.png)
