# Android and Desktop app to generate class layout
A java based multi threaded application to generate class layout for students and teachers in a particular course.

The repository contains an android app that connects to the java based server. Once logged in the person can select the seat s/he wishes to have. Teacher is a java application with GUI built using Swing library, that requests the server for class allotment data, it returns the student details with the seat numbers.


### Java Server

Server.java creates a server using socket programming. It uses multi threading to deal with heavy traffic by assigning each client to a different thread. The thread takes input from client app and saves it for further request in a synchronized list. 

On request by teacher, it makes a query to the database, and sends the data to Teacher via network. Database being local to server is important as heavy lifting work is done on remote server and both client and teacher are just providing or receiving data.

To start the server:
```
$ javac Server.java
$ java Server
```


### Client Android Application

The application is connected to wifi on which the server is hosted. User logs in by providing name and roll number, then selects the seat and logs out. The Android application makes it feasible for client to access server from anywhere, and hence is good for students.

**Code and apk is present in the Folder Android App PRoject**

### Teacher Application

Teacher is a desktop application with GUI created using Java's swing library. The teacher on request gets the data from server, data so received is sorted using **MergeSort and ForkJoin Principle**. The application then generates the layout. Project has three types of teachers:

* **Teacher A**: S/He creates the layout without the use of threads. The method is slowest and hence can be used to compare the advantages of multi-threading over single threaded applications.

* **Teacher B**: S/He uses ForkJoinPool to create a thread pool that is tasked with rendering of Layout. Each thread is rendering one Row of the layout and Divide and Conquer approach is used to divide task among threads. 

* **Teacher C**: S/He uses **ExecutorService** to create a thread pool.  Each thread is rendering one Row of the layout and Divide and Conquer approach is used to divide task among threads. 

It also compares the time taken to render the Layout by the three teachers and difference is easily visible for large layouts.

To generate layout:
```
$ javac TeacherA.java
$ java TeacherA
```
