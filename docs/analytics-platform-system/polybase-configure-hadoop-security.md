---
title: Configurare la sicurezza PolyBase Hadoop nel sistema di piattaforma Analitica | Microsoft Docs
description: Viene illustrato come configurare PolyBase in Parallel Data Warehouse per la connessione a esterna Hadoop.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/26/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c916fef2b70333c2d5bc89fec5c86d61482cdba7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678609"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>Configurazione di PolyBase e sicurezza per Hadoop

Questo articolo fornisce un riferimento per varie impostazioni di configurazione che influiscono sulla connettività di PolyBase APS per Hadoop. Per una procedura dettagliata sulle novità di PolyBase, vedere [What ' s PolyBase](configure-polybase-connectivity-to-external-data.md).

> [!NOTE]
> Sui punti di accesso, sono necessarie modifiche nel file XML in tutti i nodi di calcolo e di controllo.
> 
> Prestare particolare attenzione quando si modificano i file XML nei punti di accesso. Qualsiasi tag mancanti o i caratteri indesiderati possono invalidare il file xml che impediscono il usablilty della funzionalità.
> File di configurazione Hadoop si trovano nel percorso seguente:  
> ```  
> C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf 
> ``` 
> Qualsiasi modifica ai file xml richiede un riavvio del servizio per essere efficace.

## <a id="rpcprotection"></a> Impostazione Hadoop.RPC.Protection

Un modo comune per proteggere la comunicazione in un cluster Hadoop è modificare la configurazione di hadoop.rpc.protection impostandola su "Privacy" o "Integrity". Per impostazione predefinita, PolyBase presuppone che la configurazione sia impostata su "Authenticate". Per eseguire l'override di questa impostazione predefinita, aggiungere la proprietà seguente al file core-site.xml. La modifica di questa configurazione consente il trasferimento sicuro dei dati tra i nodi Hadoop nonché la connessione SSL a SQL Server.

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

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

Se si sceglie di suddividere le due impostazioni di configurazione in yarn-Site. XML e mapred-Site. XML, i file sarà il seguente:

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

Si noti che è stata aggiunta la proprietà mapreduce.application.classpath. In CDH 5.x, troverai i valori di configurazione con la stessa convenzione di denominazione in Ambari.

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

Per connettersi a un Hadoop protetto con Kerberos tramite MIT KDC sono necessarie le seguenti modifiche in tutti i punti di accesso cluster nodi di calcolo e del nodo di controllo:

1. Trovare le directory di configurazione Hadoop nel percorso di installazione di punti di accesso. In genere il percorso è:  

   ```  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf  
   ```  

2. Trovare il valore di configurazione lato Hadoop delle chiavi di configurazione elencate nella tabella. Nel computer Hadoop trovare i file nella directory di configurazione Hadoop.  
   
3. Copiare i valori di configurazione nella proprietà del valore nei file corrispondenti sul computer SQL Server.  
   
   |**#**|**File di configurazione**|**Chiave di configurazione**|**Azione**|  
   |------------|----------------|---------------------|----------|   
   |1|core-site.xml|polybase.kerberos.kdchost|Specificare il nome host KDC. Ad esempio: kerberos.area-di-autenticazione.com.|  
   |2|core-site.xml|polybase.kerberos.realm|Specificare l'area di autenticazione Kerberos. Ad esempio: AREA-DI-AUTENTICAZIONE.COM|  
   |3|core-site.xml|hadoop.security.authentication|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Ad esempio:  KERBEROS<br></br>**Nota sulla sicurezza:** è necessario scrivere KERBEROS in maiuscolo. Se si usano lettere minuscole, potrebbe non essere disponibile.|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Ad esempio: hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Ad esempio: mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Ad esempio: 10.193.26.174:10020|  
   |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Trovare la configurazione lato Hadoop e copiarla nel computer SQL Server. Ad esempio: yarn/_HOST@YOUR-REALM.COM|  

**core-site.xml**
```xml
<property>
  <name>polybase.kerberos.realm</name>
  <value></value>
</property>
<property>
  <name>polybase.kerberos.kdchost</name>
  <value></value>
</property>
<property>
    <name>hadoop.security.authentication</name>
    <value>KERBEROS</value>
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.namenode.kerberos.principal</name>
  <value></value> 
</property>
```

**mapred-site.xml**
```xml
<property>
  <name>mapreduce.jobhistory.principal</name>
  <value></value>
</property>
<property>
  <name>mapreduce.jobhistory.address</name>
  <value></value>
</property>
```

**yarn-site.xml**
```xml
<property>
  <name>yarn.resourcemanager.principal</name>
  <value></value>
</property>
```

4. Creare un oggetto credenziali con ambito database per specificare le informazioni di autenticazione per ogni utente di Hadoop. Vedere [Oggetti T-SQL PolyBase](../relational-databases/polybase/polybase-t-sql-objects.md).

## <a id="encryptionzone"></a> Programma di installazione di Hadoop crittografia zona
Se si usa Hadoop zona crittografia modificare core-Site. XML e hdfs-Site. XML come indicato di seguito. Specificare l'indirizzo ip in cui il servizio KMS è in esecuzione con il numero di porta corrispondente. La porta predefinita per KMS in CDH è 16000.

**core-site.xml**
```xml
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value> 
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.encryption.key.provider.uri</name>
  <value>kms://http@<ip address>:16000/kms</value>
</property>
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value>
  </property>
```