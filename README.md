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

1 worker node have multiple executor. 1 worker start 2 executor for 2 different application not for same. if u want to start 2 executor for same application then add one more worker
- standalone mode setting :
```
1. app submited will run FIFO mode by default
2.spark.cores.max : maximum amount of cpu cores to req for the application from across the cluster
3.spark.executor.memory : memory for each executor
```
standalone for single app - 

![spark-standalone-single app](https://user-images.githubusercontent.com/53288566/72234482-4211a880-35f3-11ea-8b6a-a083b08be069.png)

standalone for multiple app - 

3. Yarn Mode :
		Yarn is them resource manager. Here master machine run as resource manager and slave machine in hadoop cluster run as a node manager. 1 resource manager and multiple node manager. Node manager shares live resource info to resource manager. for eg about memory,core.
   	client machine submit the application to resource manager then resource manager find the node manager which is free. if it find any node free it will allocate it as application master then application master ask to resoutrce manager i need 2 more container then resource manager will give 2 container i.e node manager in key value pair. then that 2 container register back with application master now your application is running. now application master can directly communicate with client machine.if resource manager crashes then application master keeps running bit if resource manager crashes then application master not negotiate new container or resource in runtime.
![spark-yarn mode](https://user-images.githubusercontent.com/53288566/72234278-35408500-35f2-11ea-828e-854f3337ca28.png)





            




