val textFile=sc.textFile("file:///home/wordcount.txt");
val counts=textFile.flatmap(_.split("")).map((_,1)).reduceBykey(_ + _)




                


