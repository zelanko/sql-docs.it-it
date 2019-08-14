---
title: Ripristinare un database
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come ripristinare un database nell'istanza master di un cluster Big Data di SQL Server 2019 (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 49cc2cbb4ede2326bf774b5f39968ad4b00ed991
ms.sourcegitcommit: 316c25fe7465b35884f72928e91c11eea69984d5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2019
ms.locfileid: "68969483"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>Ripristinare un database nell'istanza master di un cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come ripristinare un database esistente nell'istanza master di un cluster Big Data di SQL Server 2019 (anteprima). Il metodo consigliato prevede l'uso di un approccio di tipo: backup, copia e ripristino.

## <a name="backup-your-existing-database"></a>Eseguire il backup di un database esistente

Come prima operazione, eseguire il backup di un database SQL Server esistente da SQL Server in Windows o in Linux. Usare tecniche di backup standard con Transact-SQL o con uno strumento come SQL Server Management Studio (SSMS).

Questo articolo descrive come ripristinare il database AdventureWorks, ma è possibile usare qualsiasi backup di database. 

> [!TIP]
> È possibile scaricare il backup di AdventureWorks [qui](https://www.microsoft.com/download/details.aspx?id=49502).

## <a name="copy-the-backup-file"></a>Copiare il file di backup

Copiare il file di backup nel contenitore SQL Server disponibile nel pod dell'istanza master del cluster Kubernetes.

```bash
kubectl cp <path to .bak file> master-0:/tmp -c mssql-server -n <name of your big data cluster>
```

Esempio:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n clustertest
```

Verificare quindi che il file di backup sia stato copiato nel contenitore pod.

```bash
kubectl exec -it master-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

Esempio:

```bash
kubectl exec -it master-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>Ripristinare il file di backup

Ripristinare quindi il backup del database in un'istanza master di SQL Server.  Se si ripristina un backup di database creato in Windows, sarà necessario ottenere i nomi dei file.  In Azure Data Studio connettersi all'istanza master ed eseguire lo script SQL seguente:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

Esempio:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![Elenco dei file di backup](media/restore-database/database-restore-file-list.png)

Ripristinare ora il database. Di seguito è riportato uno script di esempio. Sostituire i nomi o i percorsi in base alle esigenze, a seconda del backup di database selezionato.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>Configurare il pool di dati e l'accesso HDFS

Per consentire all'istanza master di SQL Server di accedere ai pool di dati e al gateway HDFS, eseguire ora le stored procedure del pool di dati e del pool di archiviazione. Eseguire gli script Transact-SQL seguenti sul database appena ripristinato:

```sql
USE AdventureWorks2016CTP3
GO
-- Create the SqlDataPool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
  CREATE EXTERNAL DATA SOURCE SqlDataPool
  WITH (LOCATION = 'sqldatapool://controller-svc/default');

-- Create the SqlStoragePool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   CREATE EXTERNAL DATA SOURCE SqlStoragePool
   WITH (LOCATION = 'sqlhdfs://controller-svc/default');
GO
```

> [!NOTE]
> Sarà necessario eseguire questi script di installazione solo sui database ripristinati da versioni precedenti di SQL Server. Se si crea un nuovo database nell'istanza master di SQL Server, le stored procedure del pool di dati e del pool di archiviazione sono già configurate.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server, vedere l'articolo di panoramica seguente:

- [Che cosa sono i cluster Big Data di SQL Server 2019?](big-data-cluster-overview.md)
