---
title: Configurazione di PolyBase e sicurezza per Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: d9fa25f4b6369db64c96d21a0591a1f8c214d61a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "64775246"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>Configurazione di PolyBase e sicurezza per Hadoop

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo include informazioni di riferimento per varie impostazioni di configurazione che influiscono sulla connettività di PolyBase con Hadoop. Per una procedura dettagliata su come usare PolyBase con Hadoop, vedere [Configurare PolyBase per l'accesso a dati esterni in Hadoop](polybase-configure-hadoop.md).

## <a id="rpcprotection"></a> Impostazione Hadoop.RPC.Protection

Un modo comune per proteggere la comunicazione in un cluster Hadoop è modificare la configurazione di hadoop.rpc.protection impostandola su "Privacy" o "Integrity". Per impostazione predefinita, PolyBase presuppone che la configurazione sia impostata su "Authenticate". Per eseguire l'override di questa impostazione predefinita, aggiungere la proprietà seguente al file core-site.xml. La modifica di questa configurazione consente il trasferimento sicuro dei dati tra i nodi Hadoop nonché la connessione SSL a SQL Server.

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

Per usare 'Privacy' o 'Integrity' per hadoop.rpc.protection, è necessario usare almeno SQL Server 2016 SP1 CU7, SQL Server 2016 SP2 o SQL Server 2017 CU3.

## <a name="example-xml-files-for-cdh-5x-cluster"></a>File XML di esempio per cluster CDH 5.X

File yarn-site.xml con i parametri di configurazione yarn.application.classpath e mapreduce.application.classpath.

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

Se si sceglie di suddividere le due impostazioni di configurazione nei file mapred-site.xml e yarn-site.xml, i file saranno come indicato di seguito:

**yarn-site.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

**mapred-site.xml**

Si noti che è stata aggiunta la proprietà mapreduce.application.classpath. In CDH 5.x i valori di configurazione usano la stessa convenzione di denominazione di Ambari.

```xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
   <property>
     <name>mapred.min.split.size</name>
       <value>1073741824</value>
   </property>
   <property>
     <name>mapreduce.app-submission.cross-platform</name>
     <value>true</value>
   </property>
<property>
     <name>mapreduce.application.classpath</name>
     <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
   </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
     <name>mapreduce.jobhistory.principal</name>
     <value></value>
   </property>
   <property>
     <name>mapreduce.jobhistory.address</name>
     <value></value>
   </property>
-->
</configuration>
```

## <a name="kerberos-configuration"></a>Configurazione di Kerberos  

Si noti che se PolyBase esegue l'autenticazione in un cluster protetto con Kerberos, il parametro hadoop.rpc.protection deve essere impostato su 'Authenticate' per impostazione predefinita. La comunicazione dei dati tra i nodi Hadoop rimane non crittografata. Per usare le impostazioni 'Privacy' o 'Integrity' per hadoop.rpc.protection, aggiornare il file core-site.xml sul server PolyBase. Per altre informazioni, vedere la sezione precedente [Connessione a un cluster Hadoop con l'impostazione hadoop.rpc.protection](#rpcprotection).

Per connettersi a un cluster Hadoop protetto con Kerberos tramite MIT KDC:

1. Trovare la directory di configurazione Hadoop nel percorso di installazione di SQL Server. In genere il percorso è:  

   ```  
   C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\PolyBase\Hadoop\conf  
   ```  

2. Trovare il valore di configurazione lato Hadoop delle chiavi di configurazione elencate nella tabella. Nel computer Hadoop trovare i file nella directory di configurazione Hadoop.  
   
3. Copiare i valori di configurazione nella proprietà del valore nei file corrispondenti sul computer SQL Server.  
   
   |**#**|**File di configurazione**|**Chiave di configurazione**|**Azione**|  
   |------------|----------------|---------------------|----------|   
   |1|core-site.xml|polybase.kerberos.kdchost|Specificare il nome host KDC. Ad esempio: kerberos.area-di-autenticazione.com.|  
   |2|core-site.xml|polybase.kerberos.realm|Specificare l'area di autenticazione Kerberos. Esempio: AREA-DI-AUTENTICAZIONE.COM|  
   |3|core-site.xml|hadoop.security.authentication|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Esempio: KERBEROS<br></br>**Nota sulla sicurezza:** è necessario scrivere KERBEROS in maiuscolo. Se si usano lettere minuscole, potrebbe non essere disponibile.|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Ad esempio: hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Ad esempio: mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Esempio: 10.193.26.174:10020|  
   |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Ad esempio: yarn/_HOST@YOUR-REALM.COM|  

4. Creare un oggetto credenziali con ambito database per specificare le informazioni di autenticazione per ogni utente di Hadoop. Vedere [Oggetti T-SQL PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md).  

## <a name="next-steps"></a>Passaggi successivi  

Per ulteriori informazioni, vedere gli articoli seguenti:

[Configurare PolyBase per l'accesso a dati esterni in Hadoop](polybase-configure-hadoop.md)
[Panoramica di PolyBase](../../relational-databases/polybase/polybase-guide.md)
