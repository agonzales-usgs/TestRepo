seedscan
========
ASL Java SeedScan Doc
========================================

	Order of Operations
	a) SeedScan.java
		1) pull config.xml and schemas/SeedScanConfig.xsd (jaxb schema)
			* Schema file used to verify config file format
		2) initializes ConfigParser.parseConfig(config.xml)
			* Uses JAXB and JAXBSchema to parse config.xml
			* config file is read in as a ConfigT() class
			* ConfigT() gets/sets 
				(1) lockfile
				(2) DatabaseT() -> gets/sets uri, uname, passwd
				(3) ScansT() -> gets list of scans
				(4) MetaserverT() -> gets/sets remoteUri
				(5) StationListT() -> gets station list
		3) initializes MetricDatabase() for reading/writing to DB
			* Gets metric data/value
			* Inserts metric data
		4) initializes MetricReader() for reading database extends TaskThread()
			* Extends TaskThread() -> creates LinkedBlockingQueue()
			* Adds tasks to queue 
				* Task<T>() -> sets command and data
			* Runs tasks on multiple threads
			* Performs tasks to get metric ID, data, value
				* MetricContext<T>() sets ID extends QueryContext<T>()
				* MetricValueIdentifier(): ID contains name, station, channel
		5) initializes MetricInjectory() for injecting into database extends TaskThread()	
