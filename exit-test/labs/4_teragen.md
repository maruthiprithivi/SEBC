## <center> Challenge 4 - HDFS Testing

* Create the Issue `Exit-test: Test HDFS`
* Assign yourself and label it `started`
* As user `groot`, use `teragen` to generate a 5 GB dataset
  * Write the output to 40 files
  * Set the block size to 64 MB
  * Set the mapper container size to 1 GiB
  * Name the target directory `tgen`
  * Use the `time` command to capture job duration
  ```
  sudo -u hdfs hdfs dfs -mkdir /user/hulk \
  && sudo -u hdfs hdfs dfs -mkdir /user/thanos \
  && sudo -u hdfs hdfs dfs -mkdir /user/groot \
  && sudo -u hdfs hdfs dfs -setfacl -m default:user:hulk:rwx /user/hulk \
  && sudo -u hdfs hdfs dfs -setfacl -m default:user:thanos:rwx /user/thanos \
  && sudo -u hdfs hdfs dfs -setfacl -m default:user:groot:rwx /user/groot \
  && sudo -u hdfs hdfs dfs -setfacl -m default:user:groot:rwx /user
  ```
* Put the following in `challenges/labs/4_teragen.md`
  * The full `teragen` command and output **Did not run completely**
    `time hadoop jar /opt/cloudera/parcels/CDH-5.11.2-1.cdh5.11.2.p0.4/jars/hadoop-examples.jar teragen -Ddfs.block.size=67108864 -Dmapreduce.map.memory.mb=1024 -Dmapred.map.tasks=40 53687091 user/groot/tgen`

    ```
    [groot@ip-172-31-16-139 ~]$ time hadoop jar /opt/cloudera/parcels/CDH-5.11.2-1.cdh5.11.2.p0.4/jars/hadoop-examples.jar teragen -Ddfs.block.size=67108864 -Dmapreduce.map.memory.mb=512 -Dmapred.map.tasks=8 53687091 user/groot/tgen
18/05/18 05:39:11 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-16-139.ap-southeast-1.compute.internal/172.31.16.139:8032
18/05/18 05:39:11 INFO terasort.TeraGen: Generating 53687091 using 8
18/05/18 05:39:11 INFO mapreduce.JobSubmitter: number of splits:8
18/05/18 05:39:11 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
18/05/18 05:39:11 INFO Configuration.deprecation: dfs.block.size is deprecated. Instead, use dfs.blocksize
18/05/18 05:39:12 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1526620909125_0004
18/05/18 05:39:12 INFO impl.YarnClientImpl: Submitted application application_1526620909125_0004
18/05/18 05:39:12 INFO mapreduce.Job: The url to track the job: http://ip-172-31-16-139.ap-southeast-1.compute.internal:8088/proxy/application_1526620909125_0004/
18/05/18 05:39:12 INFO mapreduce.Job: Running job: job_1526620909125_0004
^C
real	2m45.124s
user	0m5.839s
sys	0m0.386s
    ```
  * The result of the `time` command

  * The command and output of `hdfs dfs -ls /user/groot/tgen`

  * The command and output of `hadoop fsck -blocks /user/groot`
* Push this work to GitHub and label the Issue `review`
* Assign the issue to the instructor
