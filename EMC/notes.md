/opt/storageos/ecsportal/conf/application.conf ===> change ecs.minimum.node.requirement=1 for single node.

Node & Docker & Stat Project
Login docker 
sudo -i dockobj   //normal docker 
sudo viprexec "sudo docker ps"
sudo docker exec -it object-telegraf bash -l -c "export TERM=xterm && bash"    //specfic docker
Restart docker
sudo docker restart object-telegraf  //telegraf
Grafana
https://10.243.6.138/grafana/d/xoeEHoBmk/metering?orgId=1
UserName: emcservice Password: ChangeMe
Node Locked
solution/workaround could be used when the admin user gets locked in "any one" of the ECS nodes.
·       Login to the working node as "admin" user
·       SSH to the "locked" node as emc
·       Execute the command "sudo ssh master" in the "locked" node
·       Now you're logged in as "root" user in the "locked" node
·       Execute the command "/sbin/pam_tally2 --reset --user admin"
·       The "admin" failed count will be reset to zero.


If you hit account locked
ssh admin@10.249.249.11
from there ssh admin@10.243.6.135
sudo viprexec "pam_tally2 --user=admin --reset"
that should reset account locking on all the nodes
List all nodes
sudo getrackinfo
telegraf


etc/confd/templates/telegraf.conf.tmpl
cat /data/telegraf/conf/telegraf.conf | grep -A2 -B4 mm_
/var/log/telegraf.log     (Reloading Telegraf config)
sudo docker restart object-telegraf 

from(bucket: "monitoring_last") |> range($range) |> group(by:["_measurement"]) |> distinct(column:"_measurement") |> group(none:true) 

/opt/emc/caspian/fabric/agent/services/object/telegraf/log
/var/log

[outputs.influxdb]]
 urls = ["http://169.254.123.4:8086"]
 database = "monitoring_main"
 retention_policy = "default"
 namepass = ["mm_*"]
 [outputs.influxdb.tagpass]
   tag = [ "dashboard" ]

0: add log for a class
cona 10.243.6.136
/opt/st**/conf
vi metering-log*
/addit
<Logger name="com.emc.storageos.data.statclient.metrics.InfluxMetricsStore" level="DEBUG" additivity="false">
           <AppenderRef ref="asyncR"/>
       </Logger>
       
tail -f /opt/storages/logs/metering.log | grep "StatisticNullGroup"
   
1: build jar  //after scr 
	./gradlew  :metering:jar
	./gradlew  :blobsvc:jar
	./gradlew  :journalparser:jar
	./gradlew -a --parallel --configure-on-demand :metering:jar
	./gradlew :shared:compileProto :shared:jar :metering:jar

2: cp jar and conf file to nodes
	scp datasvc/metering/build/libs/storageos-metering.jar admin@10.243.6.135:/tmp
	(if scp: /tmp/storageos-metering.jar: Permission denied --> sudo rm -rf /tmp/*.jar)
	
	scp datasvc/metering/src/conf/metering-conf.xml admin@10.243.6.135:/tmp
	
	sudo viprapplypatch MACHINES /tmp/storageos-metering.jar
	sudo viprapplypatch MACHINES /tmp/metering-conf.xml 

3: patch to all nodes /after patch the nodes will NOT be restart autometicly.
	sudo getrackinfo -c MACHINES
	sudo viprapplypatch MACHINES /tmp/storageos-metering.jar
	sudo viprapplypatch MACHINES /tmp/metering-conf.xml

4: login the nodes
	sudo dockobj
	sudo viprexec "sudo docker ps"
    sudo viprexec 'sudo docker restart object-telegraf'(-c flag runs the command inside the object container)
	sudo viprexec -c 'kill -9 `pidof metering`'   (only restart metering )
	
	sudo viprexec -c 'grep restarting /var/log/messages | grep metering | tail -2' (check whether metering service restarted)


5: checkout the date of the files
	ls -lh /opt/storageos/conf/metering-conf.xml 
	ls -lh /opt/storageos/lib/storageos-metering.jar

6: check the DT initalize whether is good

7: check the stat https://10.243.6.138:4443/stat/#

8: go to cline 10.243.6.145 //client node
    cd /mnt/137    
    echo "put a new object to the namespace" > f1
    (put a new object to the namepsace)

9: tail -f metering.log | grep Customer (In a node which excute MA, /opt/storages/logs)
   tail -f metering.log | grep IGORN (In a node which excute MA, /opt/storages/logs)
   tail -f metering.log | grep "ustomer\|IGNORE\|Exception
   cat metering.log | grep mm_Customer

10: viprexec -c 'rm -rf /opt/storageos/logs/statistics;rm /opt/storageos/logs/statistics.json;rm /opt/storageos/logs/statisticsHistory.json; kill -9 `pidof stat`' 
viprexec -c 'rm -rf /opt/storageos/logs/statistics;rm /opt/storageos/logs/statistics.json; ;rm /opt/storageos/logs/statistics.json1;rm /opt/storageos/logs/statisticsHistory.json;' 
 sudo viprexec -c 'zgrep "CalculatorForBucket" /opt/storageos/logs/metering.log.20190311* tail -5'
 
11: kill -9 'pidof metering'
12: viprexec -c 'kill -9 `pidof metering`'

13: How to know the opertion of putting a new object execut in which node?

14: cona 10.243.6.137
	
15: 
viprexec -f MACHINES -c -i ' cd /etc/init.d; ./storageos-dataservice restart; sleep 60' (restart whole system)

16:
viprexec -c 'kill -9 `pidof stat`'

17:
sudo docker ps (container)
sudo docker ps -a 
sduo docker images (list all images)


18: cona 10.243.6.135; ssh root@192.168.219.1;ps -ef | grep installer # should not see many lines installer process.

19:
udo docker ps
Get the container id
sudo docker inspect containerId
There will be a folder mapping


OBMeteringCollectorTaskScanner

./cf_client --user emcservice --password ChangeMe --name com.emc.ecs.metering.reconstruction.reconstruct_metering_data_run_number --set --value 36 --reason "test recons"

./cf_client --user emcservice --password ChangeMe --name com.emc.ecs.metering.reconstruction.reconstruct_metering_data --set --value true --reason "test recons"

zgrep "run OBMeteringCollectorTask taskKey" blobsvc-metering-reconstruction.log


from(bucket: "monitoring_last") |> range($range) |> group(by:["_measurement"]) |> distinct(column:"_measurement") |> group(none:true)

curl http://10.243.6.135:9101/diagnostic/DumpOwnershipInfo | grep "MA_0"

curl -G 'http://10.243.6.138:8086/query?pretty=true' --data-urlencode "db=monitoring_last" --data-urlencode "q=SHOW MEASUREMENTS "




shift + g   end of the file, gg to first
? last from end of the file
ctrl + b
./cf_client --user root --password ChangeMe --list --name com.emc.ecs.metering.monitoring.publisher.bucket.topn

./cf_client --user emcservice --password ChangeMe --set --name com.emc.ecs.metering.monitoring.publisher.bucket.topn --value 10 --reason test

http://10.243.6.135:9101/urn:storageos:OwnershipInfo:cf12d408-90ed-416c-a7ea-6835926ac53a_00000000-0000-0000-0000-000000000000_MA_0_128_0:/MT2AGG_RECORD?type=BUCKET_FINAL_STAT
Depoly to VM cluster
Make sure the jars in the cluster is samer version with your branch
Find current branch commit number
build the branch changes getting jars
dump to cluster
run

git reset --hard origin/master
-Djava.rmi.server.hostname=127.0.0.1 -Dspring.profiles.active=vtfprofile -Dvirtual.cache.zipfiles=true -Dvirtual.cache.classdata=true -Dvirtual.cache.resources=true -Xmx4096m -XX:MaxPermSize=256m -Duser.timezone=UTC -Demc.storageos.FabricAPI.useStandardSecurityProviders="" -Dproduct.home="/home/fan/storage/runtime" -Dapple.awt.UIElement=true -Djava.net.preferIPv4Stack=true -Dspring.profiles.active=vtfprofile -Dlog4j.configurationFile=/home/fan/storage/runtime/templates/vtf-log4j2.xml -DisThreadContextMapInheritable=true -Dvtf.devel=true


Bronze Cluster Details :kissing_heart: Bronze - A -> 10.243.85.95 - 98 Bronze - B -> 10.243.85.105 - 108 Bronze - C -> 10.243.85.115 - 118 Branch* : bugfix-bronze-apr4


rm -rf /home/fan/.gradle/caches/modules-2/modules-2.lock

https://10.243.85.95:4443/stat/#
sudo viprexec -c 'grep entryList opt/storageos/logs/metering.log'
scp datasvc/metering/build/libs/storageos-metering.jar admin@10.243.85.95:/tmp
sudo viprexec -c 'grep bucketMetricsForBucket opt/storageos/logs/metering.log'
sudo viprexec -c 'grep DumpToMA0Started opt/storageos/logs/metering.log'
sudo viprexec -c 'grep MeteringTopConsumerPublisher.sendToPublisher opt/storageos/logs/metering.log'
sudo viprexec -c 'grep handleTOPNBytesUsageStatsPublisher opt/storageos/logs/metering.log'
sudo viprexec -c 'grep BYTESHandleTOPN opt/storageos/logs/metering.log'
sudo viprexec -c 'grep OBJECTHandleTOPN opt/storageos/logs/metering.log'
sudo viprexec -c 'grep constructResponse opt/storageos/logs/metering.log'
sudo viprexec -c 'grep PublisherUpdateQueues opt/storageos/logs/metering.log'
sudo viprexec -c 'grep topBucketsByBytesUsed.add opt/storageos/logs/metering.log'
sudo viprexec -c 'greptopBucketsByObjectCount.add opt/storageos/logs/metering.log'
sudo viprexec -c 'grep publishSize opt/storageos/logs/metering.log'
sudo viprexec -c 'grep consumingSpaceStatClientSET opt/storageos/logs/metering.log'
sudo viprexec -c 'grep rootTotalObjectsGroup.set opt/storageos/logs/metering.log'
sudo viprexec -c 'grep topBucketsByBytesUsed!=null opt/storageos/logs/metering.log'
sudo viprexec -c 'grep publisherStats.set opt/storageos/logs/metering.log'
sudo viprexec -c 'grep totalObjectsNumberStatClient.set opt/storageos/logs/metering.log'
sudo viprexec -c 'grep otalObjectsNumberStatClient.set opt/storageos/logs/metering.log'
I have followed the external monitoring wiki to set up enternal monitoring. All commands have passed. However didn't the mm_topn_bucket_by_obj_size and mm_topn_bucket_by_obj_count table in influxDB. We can guarantee the stat client setting was successful. By default will the stats data dump to monitoring_main? For TopN buckets change PR, we are struggling to setup External Monitoring. We spent a week on it but could not progress. Is it possible for you to fetch my code and test using your external monitoring when you are available?



### VTF
./gradlew runtime:copyConfs
-Dvtf.devel=true
