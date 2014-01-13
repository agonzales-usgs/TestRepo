seedscan
========
ASL Java SeedScan Doc
========================================

	Fixes
	1) Logger errors
		* log4j:WARN No appenders could be found for logger (asl.seedscan.SeedScan).
		* log4j:WARN Please initialize the log4j system properly.
		* FIX: mv log4j.properties ~/Documents/seedscan/src/

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
					(a) passwd: asldev
					(b) uri: jdbc:postgresql://136.177.123.35:5432/dataq_dev
					(c) uname: devwrite
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
			* Gets task command/data
			* Inserts metric data into metricDB
		6) loops through config scans
			* looks for duplicates
			* configures Scan() object
				* setPathPattern(scanCfg.getPath())
				* setDatalessDir(scanCfg.getDatalessDir())
				* setEventsDir(scanCfg.getEventsDir())
				* setPlotsDir(scanCfg.getPlotsDir())
				* setDaysToScan(scanCfg.getDaysToScan())
			* Filters network, station, location, channel
			* Loops through metrics
				* initializes MetricWrapper()
				* adds metric argument (ArgumentT()) name and value to wrapper
				* metrics are in the MetricT() class format
					* gets/sets className
					* gets metric argument from List<ArgumentT()>
					* ArgumentT() gets/sets name and value
				* adds metric wrapper to scan object
				* adds scanCfg name and scan object to scans HashTable<String, Scan>
		7) For each day scan for channel files, 
			* only process if they have not been scanned
			* process if changes have occurred to file since last scan
			* do for each scan type, don't rescan data for each type
				* launch processes for each scan and use the same data set for each
			* MetaServer() initialized
				* metaServer = new MetaServer(scan.getDatalessDir())
			* create Thread readerThread = new Thread(reader)
				* reader = MetricReader()
				* reads metrics from metric database
		






