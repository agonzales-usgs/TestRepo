SeedScan 
========
ASL Java SeedScan Doc
========================================

	Order of Operations
	1) SeedScan.java
		a) pull config.xml and schemas/SeedScanConfig.xsd (jaxb schema)
			* Schema file used to verify config file format
		b) initializes ConfigParser.parseConfig(config.xml)
			* Uses JAXB and JAXBSchema to parse config.xml
			* config file is read in as a ConfigT class
			* ConfigT gets/sets 
				(1) 
		c) 
