# Learning_Spark


Spark : Spark is the open source framework. Spark is a in-memory data processing engine.

- Features of spark :
```
                   1. In memory computaion
                   2. Fault tolerance
                   3. Reusability
                   4. Lazy evolution
                   5. Support multiple languages (java,python,scala,R)
                   6. integrated with hadoop
                   7. spark graphx
                   8. real time stream processing
```                
 - 4 diff way to run spark :
 ```
 1. Local
 2. Standalone
 3. Yarn
 4. Mesos
 ```
 1. Local : 
            In local mode spark will run on only one JVM that is only one machine. It has static partition.In local mode you have to mention executor manually. Once you mention it then you can not increase or decrease it.
 
Set configuration in application for local -
```
val conf =  new SparkConf()
			     .setMaster("local[12")
			     .setAppName("Myapp")
			     .set("saprk.executor.memory","3g")
  val sc = new SparkContext(conf)
 ```
            
Types to start shell on local - 
```
> ./bin/spark-shell --master local[12]   i.e 12 cores(task)
> ./bin/spark-shell --master local   -> run executor on only one worker thread but don't do this one thread is not enough
> ./bin/spark-shell --master local[*]  ->  run executor with many worker thread
``` 
Run scala application command - 
```
./bin/spark-submit --name "Myfirstapp" --master local[12] Myapp.jar
```
command will override application configuration.
 
2. Standalone mode - 
                    It's using multiple machine for single app
                    
run scala application command - 
```
> ./bin/spark-submit --name "Myapp" --master spark://host1:port1 Myapp.jar
 ```                    
spark-env.sh conrtain local directory.one of the partition store one  directory.
eg - let's suppose 4 machine 1 is master and 3 is worker and spark master knows there is total 4 workers across the cluster
driver present on worker which communicate with master.master tells to worker hey you launch 1 executor that's why worker need more memory . by default 1 executor will launch on one machine.
if executor jvm crashes worker will restart it and if worker jvm crashes the master will restart it

while running application you can add more master


            




