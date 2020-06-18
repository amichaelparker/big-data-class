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

I learned that hdfs commands function much like native Unix terminal commands, which helped make the process easier.

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

From this lesson I learned how to run Java files with input files that have been placed in the hdfs, and output the corresponding output.

## Lesson 3 ICP
I created the necessary files (found in the MatrixMultiplication folder here), and exported the project as a jar. I created the input files and copied them all to the cloudera VM.
I did these commands:
* `hdfs dfs -put M /home/cloudera/input/`
* `hdfs dfs -put N /home/cloudera/input/`
* `hadoop jar MatrixMultiplication.jar MatrixMultiplication /home/cloudera/input /home/cloudera/output`
* `hdfs dfs -ls /home/cloudera/output`
* `hdfs dfs -cat /home/cloudera/output/part-r-00000`

![image](https://i.imgur.com/8V8QTuy.png)

From this I learned how to create a java project from scratch, export a jar file using Maven, and run the Java jar against input files that I had copied to the hdfs.

## Lesson 4 ICP
I downloaded all of the source files, and ran the Cloudera VM. In the terminal, I ran `hive`, and then
I did these commands:
* `create table petrol (distributer_id STRING,distributer_name STRING,amt_IN STRING,amy_OUT STRING,vol_IN INT,vol_OUT INT,year INT) row format delimited fields terminated by ',' stored as textfile;`
* `load data local inpath '/home/cloudera/Downloads/petrol.txt' into table petrol;`
* `SELECT distributer_name,SUM(vol_OUT) FROM petrol GROUP BY distributer_name;`
* `SELECT distributer_id,vol_OUT FROM petrol order by vol_OUT desc limit 10;`
* `SELECT distributer_id,vol_OUT FROM petrol order by vol_OUT limit 10;`
* `SELECT distributer_name,(vol_IN-vol_OUT) > 500 FROM petrol order by distributer_name;`
* `create table olympic (athelete STRING,age INT,country STRING,year STRING,closing STRING,sport STRING,gold INT,silver INT,bronze INT,total INT) row format delimited fields terminated by '\t' stored as textfile;`
* `load data local inpath '/home/cloudera/Downloads/olympic_data.csv' into table olympic;`
* `SELECT country,SUM(total) from olympic where sport = "Swimming" GROUP BY country;`
* `SELECT year,SUM(total) from olympic where country = "India" GROUP BY year;`
* `SELECT country,SUM(total) from olympic GROUP BY country;`
* `SELECT country,SUM(gold) from olympic GROUP BY country;`
* `SELECT country,SUM(total) > 0 from olympic WHERE sport = "Shooting" GROUP BY country;`
* `create table ratings (userId INT,movieId INT,rating INT,timestamp INT) row format delimited fields terminated by ',' stored as textfile;`
* `load data local inpath '/home/cloudera/Downloads/ratings.csv' into table ratings;`
* `create table movies (movieId INT,title STRING,genres STRING) row format delimited fields terminated by ',' stored as textfile;`
* `load data local inpath '/home/cloudera/Downloads/movies.csv' into table movies;`
* `create table users (user_id INT,gender STRING,occupation INT,zip_code INT) row format delimited fields terminated by ',' stored as textfile;`
* `load data local inpath '/home/cloudera/Downloads/users.txt' into table users;`
* `SELECT title,genres from movies WHERE genres RLIKE 'Action*' OR genres RLIKE 'Drama*' GROUP BY title,genres;`
* `SELECT movieId from ratings WHERE rating = 5.0 GROUP BY movieId;`
* `SELECT m.title,r.rating FROM movies m JOIN ratings r ON (m.movieId = r.movieId) WHERE r.rating = 5.0 AND m.genres = "Action" ORDER BY r.rating DESC LIMIT 11;`

Some troubleshooting was necessary here. In order to run the join in hive, I needed to set this setting:
* `SET hive.auto.convert.join=false;`

I got a ton of practice with SQL queries, and learned how much easier the MapReduce process is when done with a tool like Hive.