
1) Remove the <!DOCTYPE jboss-web PUBLIC "-//JBoss//DTD Web Application 2.2//EN" "http://www.jboss.org/j2ee/dtd/jboss-web.dtd"> dtd in jboss-web.xml.
2) Added the jsp-config tag in web.xml.

<jsp-config>
..................
<taglib>
............
</taglib>
......................
</jsp-config>

3) change the dtd in jboss.xml(jar) <jboss xmlns:xs="http://www.jboss.org/j2ee/schema"
    xs:schemaLocation="http://www.jboss.org/j2ee/schema/jboss_5_0.xsd"
    version="5.0">
4) Remove the configuration bean in in jboss.xml and chanmge the sequence.

<message-driven>
         
          <!--   <configuration-bean>Standard Message Driven Bean</configuration-bean> -->
          <destination-jndi-name>queue/testQueue</destination-jndi-name>
         <ejb-name>BookOrderReceiverBean</ejb-name>
       </message-driven>

5) created the queue in  deply folder(TestQ-service.xml).

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<server>
    <mbean xmbean-dd="xmdesc/Queue-xmbean.xml" name="jboss.messaging.destination:service=Queue,name=queue/TestQ" code="org.jboss.jms.server.destination.QueueService">
        <attribute name="JNDIName">queue/testQueue</attribute>
        <depends optional-attribute-name="ServerPeer">jboss.messaging:service=ServerPeer</depends>
        <depends>jboss.messaging:service=PostOffice</depends>
    </mbean>
</server>

6) created the datasource in deploy folder.(mysql-ds.xml)

<?xml version="1.0" encoding="UTF-8"?>

<!-- The Hypersonic embedded database JCA connection factory config -->

<!-- See http://www.jboss.org/community/wiki/Multiple1PC for information about local-tx-datasource -->
<!-- $Id: hsqldb-ds.xml 88948 2009-05-15 14:09:08Z jesper.pedersen $ -->
<datasources>
    <local-tx-datasource>
        <jndi-name>libra</jndi-name>
        <connection-url>jdbc:mysql://192.168.1.125/libra</connection-url>
 
        <driver-class>com.mysql.jdbc.Driver</driver-class>
        <user-name>root</user-name>
        <password>root</password>
 
        <min-pool-size>5</min-pool-size>
        <max-pool-size>100</max-pool-size>
        <query-timeout>60</query-timeout>
        <exception-sorter-class-name>org.jboss.resource.adapter.jdbc.vendor.OracleExceptionSorter
        </exception-sorter-class-name>
 
        <metadata>
            <type-mapping>mysql</type-mapping>
        </metadata>
    </local-tx-datasource>
 
</datasources>

7) Start the server all profile



