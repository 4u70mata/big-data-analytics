### The Hadoop Ecosystem
   
##### HDFS Hadoop Distributed File System :  

Hadoop Distributed File System (HDFS) differs from traditional filesystems in that it's typically not directly mounted for user viewing in the conventional sense. Instead, HDFS offers shell commands and a Java API that resemble those of other file systems. Designed to be distributed, scalable, and portable, HDFS is a Java-based filesystem specifically tailored for the Hadoop framework.
Data Blocks

HDFS is designed to support very large files. Applications that are compatible with HDFS are those that deal with large data sets. These applications write their data only once but they read it one or more times and require these reads to be satisfied at streaming speeds. HDFS supports write-once-read-many semantics on files. A typical block size used by HDFS is 64 MB, 128MB, 256MB and so on ... Thus, an HDFS file is chopped up into 64 MB chunks, and if possible, each chunk will reside on a different DataNode.
Theoretical illustration   
<p align="center">
  <img src="assets/graphviz.png" alt="Image Description" width="400">
</p>
HDFS, the Hadoop Distributed File System, consists of two key components: the NameNode and the DataNode. The NameNode holds essential metadata about the filesystem, including file names, permissions, and block locations. It acts as the central authority in HDFS. DataNodes, on the other hand, store the actual data blocks and rely on the NameNode for metadata information. Without the NameNode, DataNodes cannot serve data to clients effectively.  
<p align="center">
  <img src="https://miro.medium.com/v2/resize:fit:1060/1*nDQlParMW3IIlrNjXRjQCQ.png" alt="Image from : https://medium.com/@venkatkarthick15/understanding-hdfs-a-simple-guide-to-how-hadoop-stores-data-51c1a29e1f73" width="400">
</p>
Although the NameNode and DataNode processes can be run on a single machine, HDFS clusters are meant generally to be in an architecture where the NameNode is running on server and thousands of machines running the DataNodes. 
An architecture where the only single point failure is the NameNode, everything aside the NameNode contains all information or metadata about the location of each block and its replicas thus can serve the clien on read/write operations , and block operations such as making sure the replications are built back up in case of DataNode failure.

<p align="center">
  <img src="find some picture of single point failure NameNode Architecture" alt ="Single point Failure Hadoop cluster">
</p>

###### Hadoop 2.x< and High Availability Feature :

This influenced future Hadoop Versions, first hadoop 2.X introduced a solutionto high availability needs by implementing a solution to help recover from the previous NameNode Failure. Through an active-passive set up an additional passive NameNode(s) is added to the active NameNode, and act as a Standby to the avtive Node.In order for the standby node to keep its state synchronized with the active node, they both communicate with a group of separate deamons	called "JournalNodes"(JNs).Any namespace modification performed by the active node is logged to the JN, to enable synchronization before failover occurs, and therefore the delegation of a Standby node to the active state.
A good practice is to run an odd number of JNs 3, 5, 7, ... , in general when running a number N of JNs the system can tolerate at most (N - 1)/2 failures.

<p align="center">
  <img src=" " alt="Active/Passive Configuration for the High Availability (>2.x) hadoop feature">
</p>
Requirements :
	-the machine responsible for running the NameNode ( active/Standby ) should have equivalent hardware, and to what well be used in a non-HA cluster.
	-the JournalNodes machines : these deamons are relatively lightweight, then they may be collocated on machines with other hadoop deamons such as NameNodes, JobTracker, the YARN RessourceManager  


[Thu Apr 18 00:01:22 CEST 2024] TOBECON


