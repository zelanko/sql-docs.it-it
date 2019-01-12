---
title: Caricare dati di esempio
titleSuffix: SQL Server 2019 big data clusters
description: Questa esercitazione illustra come caricare i dati di esempio in un cluster di big data di SQL Server. I dati di esempio includono i dati relazionali nell'istanza master di SQL Server. Include anche dati di HDFS nel pool di archiviazione. Questo tipo di dati supporta altre esercitazioni in questa sezione.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/13/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a89b1bec266f590d6e96365436fe5339b9152f92
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241481"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-2019-big-data-cluster"></a>Esercitazione: Caricare i dati di esempio in un cluster di big data di SQL Server 2019

Questa esercitazione illustra come usare uno script per caricare i dati di esempio in un cluster di big data di SQL Server 2019 (anteprima). Molte delle altre esercitazioni nella documentazione di usare i dati di esempio.

> [!TIP]
> È possibile trovare esempi aggiuntivi per il cluster di big data 2019 Server SQL (anteprima) nei [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) repository GitHub. Cui sono inclusi i **sql-server-samples/samples/features/sql-big-data-cluster/** percorso.

## <a name="prerequisites"></a>Prerequisiti

- [Un cluster di big data distribuita](deployment-guidance.md)
- [Strumenti dei big Data](deploy-big-data-tools.md)
   - **mssqlctl**
   - **Kubectl**
   - **sqlcmd**
   - **CURL**

## <a id="sampledata"></a> Caricare dati di esempio

La procedura seguente usa uno script di bootstrap per scaricare un backup del database di SQL Server e caricare i dati in cluster i big Data. Per semplicità d'uso, questi passaggi sono stati suddivisi in [Windows](#windows) e [Linux](#linux) sezioni.

## <a id="windows"></a> Windows

I passaggi seguenti descrivono come usare un client Windows per caricare i dati di esempio del cluster di big data.

1. Aprire un nuovo prompt dei comandi di Windows.

   > [!IMPORTANT]
   > Non utilizzare Windows PowerShell per questi passaggi. In PowerShell, lo script avrà esito negativo perché utilizzerà la versione di PowerShell di **curl**.

1. Uso **curl** per scaricare lo script di bootstrap per i dati di esempio.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Scaricare il **bootstrap-esempio-db.sql** script Transact-SQL. Questo script viene chiamato dallo script di bootstrap.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. Lo script di bootstrap richiede i seguenti parametri posizionali per il cluster di big data:

   | Parametro | Descrizione |
   |---|---|
   | &LT; CLUSTER_NAMESPACE &GT; | Il nome è stato assegnato il cluster di big data. |
   | &LT; SQL_MASTER_IP &GT; | L'indirizzo IP dell'istanza master. |
   | &LT; SQL_MASTER_SA_PASSWORD &GT; | La password dell'amministratore di sistema per l'istanza master. |
   | &LT; KNOX_IP &GT; | L'indirizzo IP del Gateway HDFS/Spark. |
   | &LT; KNOX_PASSWORD &GT; | La password per il Gateway HDFS/Spark. |

   > [!TIP]
   > Uso [kubectl](cluster-troubleshooting-commands.md) per trovare gli indirizzi IP per l'istanza master di SQL Server e Knox. Eseguire `kubectl get svc -n <your-cluster-name>` ed esaminare gli indirizzi di EXTERNAL-IP per l'istanza master (**endpoint-master-pool**) e Knox (**servizio-sicurezza-lb** o **servizio-sicurezza-nodeport**).

1. Eseguire lo script di bootstrap.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

I passaggi seguenti descrivono come usare un client Linux per caricare i dati di esempio del cluster di big data.

1. Scaricare lo script di bootstrap e assegnarvi autorizzazioni di esecuzione.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Scaricare il **bootstrap-esempio-db.sql** script Transact-SQL. Questo script viene chiamato dallo script di bootstrap.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. Lo script di bootstrap richiede i seguenti parametri posizionali per il cluster di big data:

   | Parametro | Descrizione |
   |---|---|
   | &LT; CLUSTER_NAMESPACE &GT; | Il nome è stato assegnato il cluster di big data. |
   | &LT; SQL_MASTER_IP &GT; | L'indirizzo IP dell'istanza master. |
   | &LT; SQL_MASTER_SA_PASSWORD &GT; | La password dell'amministratore di sistema per l'istanza master. |
   | &LT; KNOX_IP &GT; | L'indirizzo IP del Gateway HDFS/Spark. |
   | &LT; KNOX_PASSWORD &GT; | La password per il Gateway HDFS/Spark. |

   > [!TIP]
   > Uso [kubectl](cluster-troubleshooting-commands.md) per trovare gli indirizzi IP per l'istanza master di SQL Server e Knox. Eseguire `kubectl get svc -n <your-cluster-name>` ed esaminare gli indirizzi di EXTERNAL-IP per l'istanza master (**endpoint-master-pool**) e Knox (**servizio-sicurezza-lb** o **servizio-sicurezza-nodeport**).

1. Eseguire lo script di bootstrap.

   ```bash
   ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver eseguito lo script di bootstrap, il cluster di big data con il database di esempio e dati di HDFS. Per iniziare a esplorare dati e i cluster di big data, vedere la [esercitazioni](tutorial-query-hdfs-storage-pool.md) in questa sezione.