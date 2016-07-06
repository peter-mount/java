Based on jeanblanchard/java these images contain essential additons not found in the normal JDK/JRE's.

At the current moment in time this consists of the LetsEncrypt CA Certs in the trust store, necessary for ourselves as we use LetsEncrypt ourselves and the standard JDK/JRE's don't support them yet.

There's three images:

* area51/java:jdk-8 The full JDK
* area51/java:jre-8 Just the Java Runtime Environment
* area51/java:serverjre-8 The server JRE

In most instances, you'll want to use area51/java:serverjre-8 for server side applications.

Latest version is running Java 8 update 92 build 14

Note: This image is for Intel/AMD processors (i.e. most docker installations). For the Raspberry PI please see the area51/rpi-java image

