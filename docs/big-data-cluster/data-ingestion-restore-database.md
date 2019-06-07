---
title: Ripristinare un database
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come ripristinare un database nell'istanza master di un cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 541aa292453b80eb92691061de3f2f9be2c7fd6a
ms.sourcegitcommit: 32dce314bb66c03043a93ccf6e972af455349377
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744001"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>Ripristinare un database nell'istanza master del cluster dei big data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come ripristinare un database esistente nell'istanza master di un cluster di big data di SQL Server 2019 (anteprima). Il metodo consigliato è usare una copia di backup, e il ripristino approccio.

## <a name="backup-your-existing-database"></a>Eseguire il backup del database esistente

In primo luogo, il backup del database di SQL Server esistente da SQL Server in Windows o Linux. Usare le tecniche standard di backup con Transact-SQL o con uno strumento come SQL Server Management Studio (SSMS).

Questo articolo illustra come ripristinare il database AdventureWorks, ma è possibile usare qualsiasi backup del database. 

> [!TIP]
> È possibile scaricare il backup di AdventureWorks [qui](https://www.microsoft.com/download/details.aspx?id=49502).

## <a name="copy-the-backup-file"></a>Copiare il file di backup

Copiare il file di backup nel contenitore di SQL Server nel pod istanza master del cluster Kubernetes.

```bash
kubectl cp <path to .bak file> mssql-master-pool-0:/tmp -c mssql-server -n <name of your big data cluster>
```

Esempio:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-master-pool-0:/tmp -c mssql-server -n clustertest
```

Verificare quindi che il file di backup è stato copiato nel contenitore di pod.

```bash
kubectl exec -it mssql-master-pool-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

Esempio:

```bash
kubectl exec -it mssql-master-pool-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>Ripristinare il file di backup

Successivamente, ripristinare il backup del database per istanza master di SQL Server.  Se si sta ripristinando un backup di database che è stato creato in Windows, è necessario ottenere i nomi dei file.  In Azure Data Studio, connettersi all'istanza master ed eseguire questo script SQL:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

Esempio:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![Elenco di file di backup](media/restore-database/database-restore-file-list.png)

A questo punto, ripristinare il database. Lo script seguente è riportato un esempio. Sostituire i nomi o i percorsi in base alle esigenze a seconda del backup del database.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>Configurare l'accesso HDFS e pool di dati

A questo punto, per l'istanza master di SQL Server al pool di dati di accesso e HDFS, eseguire le procedure di pool archiviati pool e l'archiviazione dei dati. Eseguire gli script di Transact-SQL seguenti nel database appena ripristinato:

```sql
USE AdventureWorks2016CTP3
GO
-- Create the SqlDataPool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
  CREATE EXTERNAL DATA SOURCE SqlDataPool
  WITH (LOCATION = 'sqldatapool://controller-svc:8080/datapools/default');

-- Create the SqlStoragePool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   CREATE EXTERNAL DATA SOURCE SqlStoragePool
   WITH (LOCATION = 'sqlhdfs://controller-svc:8080/default');
GO
```

> [!NOTE]
> È necessario eseguire questi script di installazione solo per i database ripristinati da versioni precedenti di SQL Server. Se si crea un nuovo database nell'istanza master di SQL Server, pool e l'archiviazione del pool store procedure dati sono già configurate per l'utente.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data di SQL Server, vedere Panoramica riportata di seguito:

- [Quali sono i cluster di SQL Server 2019 dei big Data?](big-data-cluster-overview.md)
