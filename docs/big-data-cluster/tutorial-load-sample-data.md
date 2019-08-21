---
title: Caricare dati di esempio
titleSuffix: SQL Server big data clusters
description: Questa esercitazione illustra come caricare dati di esempio in un cluster Big Data di SQL Server. I dati di esempio includono dati relazionali presenti nell'istanza master di SQL Server e dati HDFS presenti nel pool di archiviazione. Questi dati supportano altre esercitazioni disponibili in questa sezione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 405df2c66917dc5e5b350aaaa0769bede6ccf6c9
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653281"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>Esercitazione: Caricare dati di esempio in un cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come usare uno script per caricare dati di esempio in un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Questi dati di esempio vengono usati anche da molte altre esercitazioni disponibili nella documentazione.

> [!TIP]
> È possibile trovare altri esempi per [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] nel repository GitHub [SQL-Server-Samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) . Si trovano nel percorso **sql-server-samples/samples/features/sql-big-data-cluster/** .

## <a name="prerequisites"></a>Prerequisiti

- [Un cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**
 
## <a id="sampledata"></a> Caricare dati di esempio

Questa procedura usa uno script di bootstrap per scaricare un backup del database di SQL Server e caricare i dati nel cluster Big Data. Per semplicità d'uso, questa procedura è stata suddivisa nelle sezioni [Windows](#windows) e [Linux](#linux).

## <a id="windows"></a> Windows

Questa procedura descrive come usare un client Windows per caricare i dati di esempio nel cluster Big Data.

1. Aprire un nuovo prompt dei comandi di Windows.

   > [!IMPORTANT]
   > Non usare Windows PowerShell per questa procedura. In PowerShell, lo script avrà esito negativo perché userà la versione PowerShell di **curl**.

1. Usare **curl** per scaricare lo script di bootstrap per i dati di esempio.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Scaricare lo script Transact-SQL **bootstrap-sample-db.sql**, che viene chiamato dallo script di bootstrap.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. Lo script di bootstrap richiede i seguenti parametri posizionali per il cluster Big Data:

   | Parametro | Descrizione |
   |---|---|
   | <CLUSTER_NAMESPACE> | Nome assegnato al cluster Big Data. |
   | <SQL_MASTER_IP> | Indirizzo IP dell'istanza master. |
   | <SQL_MASTER_SA_PASSWORD> | Password SA per l'istanza master. |
   | <KNOX_IP> | Indirizzo IP del gateway HDFS/Spark. |
   | <KNOX_PASSWORD> | Password del gateway HDFS/Spark. |

   > [!TIP]
   > Usare [kubectl](cluster-troubleshooting-commands.md) per trovare gli indirizzi IP per l'istanza master di SQL Server e Knox. Eseguire `kubectl get svc -n <your-big-data-cluster-name>` e osservare gli indirizzi EXTERNAL-IP per l'istanza master (**master-svc-external**) e Knox (**gateway-svc-external**). Il nome predefinito di un cluster è **mssql-cluster**.

1. Eseguire lo script di bootstrap.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

Questa procedura descrive come usare un client Linux per caricare i dati di esempio nel cluster Big Data.

1. Scaricare lo script di bootstrap e assegnare ad esso le autorizzazioni eseguibili.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Scaricare lo script Transact-SQL **bootstrap-sample-db.sql**, che viene chiamato dallo script di bootstrap.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. Lo script di bootstrap richiede i seguenti parametri posizionali per il cluster Big Data:

   | Parametro | Descrizione |
   |---|---|
   | <CLUSTER_NAMESPACE> | Nome assegnato al cluster Big Data. |
   | <SQL_MASTER_IP> | Indirizzo IP dell'istanza master. |
   | <SQL_MASTER_SA_PASSWORD> | Password SA per l'istanza master. |
   | <KNOX_IP> | Indirizzo IP del gateway HDFS/Spark. |
   | <KNOX_PASSWORD> | Password del gateway HDFS/Spark. |

   > [!TIP]
   > Usare [kubectl](cluster-troubleshooting-commands.md) per trovare gli indirizzi IP per l'istanza master di SQL Server e Knox. Eseguire `kubectl get svc -n <your-big-data-cluster-name>` e osservare gli indirizzi EXTERNAL-IP per l'istanza master (**master-svc-external**) e Knox (**gateway-svc-external**). Il nome predefinito di un cluster è **mssql-cluster**.

1. Eseguire lo script di bootstrap.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>Passaggi successivi

Al termine dell'esecuzione dello script di bootstrap, nel cluster Big Data sono contenuti i database di esempio e i dati HDFS. Le esercitazioni seguenti usano i dati di esempio per illustrare le funzionalità dei cluster Big Data:

Virtualizzazione dei dati:

- [Esercitazione: Eseguire query su dati HDFS in un cluster Big Data di SQL Server ](tutorial-query-hdfs-storage-pool.md)
- [Esercitazione: Eseguire query su dati Oracle da un cluster Big Data di SQL Server ](tutorial-query-oracle.md)

Inserimento dati:

- [Esercitazione: Inserire dati in un pool di dati di SQL Server con Transact-SQL](tutorial-data-pool-ingest-sql.md)
- [Esercitazione: Inserire dati in un pool di dati di SQL Server con processi Spark](tutorial-data-pool-ingest-spark.md)

Notebook:

- [Esercitazione: Eseguire un notebook di esempio in un cluster Big Data di SQL Server 2019](tutorial-notebook-spark.md)
