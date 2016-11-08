# Cassandra Monitor Tango Device Server

The CassandraMonitor device server is a Tango device server (see [tango-controls website](http://www.tango-controls.org)), able to monitor what's happening on a given Apache Cassandra node.
The goal is to benefit from the Tango Controls features to be able to identify the current state of Cassandra nodes and to allow interested Tango clients to react according to the current state (triggering alarms, notifying Tango clients) for instance.
Another goal is to use the Tango archiving capabilities (like HDB++) to monitor interesting Cassandra metrics.
The device server is written in JAVA and is using JMX internally to access Cassandra metrics.
This project was orginally developped as part of the [Tango HDB++ project](http://www.tango-controls.org/community/projects/hdbplus) (Cassandra version) but could be used independently to monitor any Cassandra node from a TANGO Control System.

## Getting Started

To compile this device server, follow the following steps:
```
git clone https://github.com/tango-controls/CassandraMonitor.git
cd CassandraMonitor
pogo CassandraMonitor.xmi
```
* in Pogo, click on the floppy disk icon or go to the File Menu and click on Generate.
* In the Generation Preference Window dialog, unselect the "Code files" check box and select Linux Makefile checkbox.
* Click on OK
* Click on OK on the next dialog too. After this, the Makefile should have been generated.

To generate the jar file:
```
mkdir bin
export CLASSPATH=<path/to/JTango.jar>
make jar
```
To run a test instance of the device server (named test), you can execute the following instructions:
```
export CLASSPATH=<path/to/JTango.jar>:cassandramonitor-1.0.jar
make run
```
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

A configured Tango Control System is required to be able to run this device server.
Pogo, the Tango-Controls device server code generator must be installed to be able to generate the Makefile from the xmi file.
Java must be installed on the machine this device server will be running on.
The Cassandra nodes this device server will monitor must be configured to allow JMX access from the machine where CassandraMonitor device server will be running. Please refer to Apache Cassandra documentation to know how to configure JMX. This is configured in cassandra-env.sh configuration file.

For the moment, CassandraMonitor has been developed and tested with Cassandra version 2.2.4 and 2.2.6.
It might work with other versions but there is no warranty since there might be incompatible changes in the Cassandra JMX interface.

### Installing

An instance of the CassandraMonitor device server must be defined in the Tango database of your choice, if you are using a database. You can use Jive Server Wizard (from the tools menu) or use the Create server entry from jive's Edit menu to define the instance and declare new devices. The device server can be started without Tango database too. Please refer to the Tango-Controls documentation for these steps.

Please refer to the Tango-Controls documentation to learn in details how to declare a new device server.
To compile this device server, one solution is to use POGO (the Tango-Controls device server code generator) to generate a new Makefile for your Tango configuration as described in the Getting Started above section.

Node property must be created for your devices. You can use jive to create this property. This Node property defines the hostname of the Cassandra node the CassandraMonitor device will talk to.
If you have configured JMX with authentication, you will have to define JMXUser and JMXPassword device properties.
If a Cassandra node is configured to listen on a JMX port different than the default one (7199), JMXPort device property must be defined.

Java must be installed on the machine where the device server will be running and the CLASSPATH environment variable must be set to point to JTango.jar and cassandramonitor generated jar.
TANGO_HOST environment variable must be defined to be able to communicate with the Tango Database server (if you are using a Tango database).

To start the device server, run the following command (replacing \<instance\> with the device server instance name you declared:
```
java org.tango.cassandramonitor/CassandraMonitor  <instance_name>

```

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/tango-controls/CassandraMonitor/tags). 

## Authors

* [Reynald Bourtembourg] (https://github.com/bourtemb)
* [Pascal Verdier] (https://github.com/Pascal-Verdier)

See also the list of [contributors](https://github.com/tango-controls/CassandraMonitor/contributors) who participated in this project.

## License

This project is licensed under the GPL License - see the [LICENSE.md](LICENSE) file for details.

## Related links

* [Tango-Controls](http://www.tango-controls.org)
* [Tango HDB++ project](http://www.tango-controls.org/community/projects/hdbplus)

## Acknowledgments

* Billie Thompson * - [PurpleBooth](https://github.com/PurpleBooth) for the [README](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2) and [CONTRIBUTING](https://gist.github.com/PurpleBooth/b24679402957c63ec426) templates.


