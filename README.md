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
