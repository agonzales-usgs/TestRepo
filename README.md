seedscan
========
ASL Java SeedScan Doc
========================================

	Order of Operations
	1) SeedScan.java
		a) pull config.xml and schemas/SeedScanConfig.xsd (jaxb schema)
			* Schema file used to verify config file format
		b) initializes ConfigParser.parseConfig(config.xml)
			* Uses JAXB and JAXBSchema to parse config.xml
			* config file is read in as a ConfigT() class
			* ConfigT() gets/sets 
				(1) lockfile
				(2) DatabaseT() -> gets/sets uri, uname, passwd
				(3) ScansT() -> gets list of scans
				(4) MetaserverT() -> gets/sets remoteUri
				(5) StationListT() -> gets station list
		c) initializes MetricDatabase() for reading/writing to DB
			* Gets metric data/value
			* Inserts metric data
		d) initializes MetricReader() for reading database
			* Extends TaskThread() -> creates LinkedBlockingQueue()
			* Adds tasks to queue 
				* Task<T>() -> sets command and data
