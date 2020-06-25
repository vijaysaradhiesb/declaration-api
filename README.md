# declaration-api
declaration-api


CREATE TABLE EXTERNAL_SYSTEM_MAPPED_PROP
(
	EXTERNAL_PROPERTY_MAP_ITEM_ID IDENTITY PRIMARY KEY NOT NULL,
	EXTERNAL_SYSTEM VARCHAR(255) NOT NULL,
	REF_DATA_TABLE VARCHAR(255) NOT NULL,
	REF_DATA_CODE VARCHAR(255) NOT NULL,
	EXT_SYS_PROPERTY_VALUE VARCHAR(255) NOT NULL,
	EXT_SYS_PROPERTY_PATH VARCHAR(255),
	MULTI_DEFAULT_VALUE TINYINT,
	TABLE_DEFAULT_VALUE TINYINT,
	ICE_TO_EXT_ONLY TINYINT,
	EXT_TO_ICE_ONLY TINYINT
);

INSERT INTO EXTERNAL_SYSTEM_MAPPED_PROP (EXTERNAL_SYSTEM, REF_DATA_TABLE, REF_DATA_CODE, EXT_SYS_PROPERTY_VALUE, EXT_SYS_PROPERTY_PATH, MULTI_DEFAULT_VALUE, TABLE_DEFAULT_VALUE, ICE_TO_EXT_ONLY, EXT_TO_ICE_ONLY) VALUES ('ABC', 'TITLE', 'MR', 'Mr', null, 0, 0, null, null);
INSERT INTO EXTERNAL_SYSTEM_MAPPED_PROP (EXTERNAL_SYSTEM, REF_DATA_TABLE, REF_DATA_CODE, EXT_SYS_PROPERTY_VALUE, EXT_SYS_PROPERTY_PATH, MULTI_DEFAULT_VALUE, TABLE_DEFAULT_VALUE, ICE_TO_EXT_ONLY, EXT_TO_ICE_ONLY) VALUES ('ABC', 'TITLE', 'MRS', 'Mrs', null, 0, 0, null, null);



H2 library:

<dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <version>1.4.188</version>
            <scope>test</scope>
        </dependency>
	
	

	
	<osgi:service id="dataSourceService" ref="internalXADataSource" interface="javax.sql.XADataSource">
        <service-properties>
            <entry key="integ.xads.name" value="${xads1.osgi.name}"/>
            <entry key="integ.xads.default" value="${xads1.osgi.default:false}"/>

            <entry key="aries.xa.name" value="${xads1.tm.uniqueResourceName}"/>
            <entry key="aries.xa.poolMinSize" value="${xads1.ds.minPoolSize}"/>
            <entry key="aries.xa.poolMaxSize" value="${xads1.ds.maxPoolSize}"/>
            <entry key="aries.xa.connectionMadIdleMinutes" value="${xads1.ds.connectionMadIdleMinutes:0}"/>
            <entry key="aries.xa.connectionMaxWaitMilliseconds" value="${xads1.ds.connectionMaxWaitMilliseconds:5000}"/>
            <entry key="aries.xa.backgroundValidation" value="${xads1.ds.backgroundValidation:true}"/>
            <entry key="aries.xa.backgroundValidationMilliseconds" value="${xads1.ds.backgroundValidationMilliseconds:15000}"/>
            <entry key="aries.xa.exceptionSorter" value="${xads1.ds.exception.sorter:none}"/>
            <entry key="aries.xa.transaction" value="xa"/>
        </service-properties>
    </osgi:service>
