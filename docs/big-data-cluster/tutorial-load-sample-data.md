---
title: Caricare dati di esempio
titleSuffix: SQL Server big data clusters
description: Questa esercitazione illustra come caricare dati di esempio in un cluster SQL Server Big Data. I dati di esempio includono dati relazionali nell'istanza SQL Server master. Include anche i dati di HDFS nel pool di archiviazione. Questi dati supportano altre esercitazioni in questa sezione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b35eccece4df47cb483932386cf6a38e45d2dc8
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419282"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>Esercitazione: Caricare i dati di esempio in un cluster SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come usare uno script per caricare dati di esempio in un cluster SQL Server 2019 Big Data (anteprima). Molte delle altre esercitazioni nella documentazione utilizzano questi dati di esempio.

> [!TIP]
> È possibile trovare esempi aggiuntivi per SQL Server 2019 Big Data cluster (anteprima) nel repository GitHub [SQL-Server-Samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) . Si trovano in **SQL-Server-Samples/Samples/features/SQL-Big-Data-cluster/** Path.

## <a name="prerequisites"></a>Prerequisiti

- [Un cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**

## <a id="sampledata"></a>Carica dati di esempio

La procedura seguente usa uno script bootstrap per scaricare un backup del database di SQL Server e caricare i dati nel cluster Big Data. Per semplicità d'uso, questi passaggi sono stati suddivisi in sezioni di [Windows](#windows) e [Linux](#linux) .

## <a id="windows"></a> Windows

I passaggi seguenti descrivono come usare un client Windows per caricare i dati di esempio nel cluster Big Data.

1. Aprire un nuovo prompt dei comandi di Windows.

   > [!IMPORTANT]
   > Non usare Windows PowerShell per questi passaggi. In PowerShell, lo script avrà esito negativo perché utilizzerà la versione di PowerShell di **curl**.

1. Usare **curl** per scaricare lo script bootstrap per i dati di esempio.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Scaricare lo script Transact-SQL **bootstrap-Sample-DB. SQL** . Questo script viene chiamato dallo script bootstrap.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. Lo script bootstrap richiede i seguenti parametri posizionali per il cluster Big Data:

   | Parametro | Descrizione |
   |---|---|
   | <CLUSTER_NAMESPACE> | Nome assegnato al cluster Big Data. |
   | <SQL_MASTER_IP> | Indirizzo IP dell'istanza master. |
   | <SQL_MASTER_SA_PASSWORD> | Password SA per l'istanza master. |
   | <KNOX_IP> | Indirizzo IP del gateway HDFS/Spark. |
   | <KNOX_PASSWORD> | Password per il gateway HDFS/Spark. |

   > [!TIP]
   > Usare [kubectl](cluster-troubleshooting-commands.md) per trovare gli indirizzi IP per l'istanza master di SQL Server e Knox. Eseguire `kubectl get svc -n <your-big-data-cluster-name>` ed esaminare gli indirizzi IP esterni per l'istanza master (**Master-SVC-External**) e Knox (**gateway-SVC-External**). Il nome predefinito di un cluster è **MSSQL-cluster**.

1. Eseguire lo script bootstrap.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

I passaggi seguenti descrivono come usare un client Linux per caricare i dati di esempio nel cluster Big Data.

1. Scaricare lo script bootstrap e assegnarvi le autorizzazioni eseguibili.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Scaricare lo script Transact-SQL **bootstrap-Sample-DB. SQL** . Questo script viene chiamato dallo script bootstrap.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. Lo script bootstrap richiede i seguenti parametri posizionali per il cluster Big Data:

   | Parametro | Descrizione |
   |---|---|
   | <CLUSTER_NAMESPACE> | Nome assegnato al cluster Big Data. |
   | <SQL_MASTER_IP> | Indirizzo IP dell'istanza master. |
   | <SQL_MASTER_SA_PASSWORD> | Password SA per l'istanza master. |
   | <KNOX_IP> | Indirizzo IP del gateway HDFS/Spark. |
   | <KNOX_PASSWORD> | Password per il gateway HDFS/Spark. |

   > [!TIP]
   > Usare [kubectl](cluster-troubleshooting-commands.md) per trovare gli indirizzi IP per l'istanza master di SQL Server e Knox. Eseguire `kubectl get svc -n <your-big-data-cluster-name>` ed esaminare gli indirizzi IP esterni per l'istanza master (**Master-SVC-External**) e Knox (**gateway-SVC-External**). Il nome predefinito di un cluster è **MSSQL-cluster**.

1. Eseguire lo script bootstrap.

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>Passaggi successivi

Dopo l'esecuzione dello script di bootstrap, il cluster di Big Data include i database di esempio e i dati HDFS. Le esercitazioni seguenti usano i dati di esempio per illustrare le funzionalità del cluster Big Data:

Virtualizzazione dei dati:

- [Esercitazione: Eseguire query su HDFS in un cluster SQL Server Big Data](tutorial-query-hdfs-storage-pool.md)
- [Esercitazione: Eseguire query su Oracle da un cluster di Big Data SQL Server](tutorial-query-oracle.md)

Inserimento dati:

- [Esercitazione: Inserire dati in un pool di dati SQL Server con Transact-SQL](tutorial-data-pool-ingest-sql.md)
- [Esercitazione: Inserire dati in un pool di dati SQL Server con processi Spark](tutorial-data-pool-ingest-spark.md)

Notebook

- [Esercitazione: Eseguire un notebook di esempio in un cluster SQL Server 2019 Big Data](tutorial-notebook-spark.md)