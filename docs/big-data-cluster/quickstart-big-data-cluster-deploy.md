---
title: Script di distribuzione
titleSuffix: SQL Server big data clusters
description: Procedura dettagliata per la distribuzione di cluster di SQL Server 2019 Big Data (anteprima) in Azure Kubernetes Service (AKS).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ff1ec3672fbcf101d98ad30913742186dea574d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419398"
---
# <a name="deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Distribuire SQL Server cluster Big Data in Azure Kubernetes Service (AKS)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

In questa esercitazione si userà uno script di distribuzione di esempio per distribuire SQL Server 2019 cluster Big Data (anteprima) in Azure Kubernetes Service (AKS). 

> [!TIP]
> AKS è una sola opzione per ospitare Kubernetes per il cluster Big Data. Per informazioni sulle altre opzioni di distribuzione e su come personalizzare le opzioni di distribuzione, vedere [How to deploy SQL Server Big Data Clusters on Kubernetes](deployment-guidance.md).

La distribuzione predefinita del cluster Big Data usata in questa sezione è costituita da un'istanza di SQL Master, un'istanza del pool di calcolo, due istanze del pool di dati e due istanze del pool di archiviazione. I dati vengono salvati in modo permanente usando i volumi permanenti Kubernetes che usano le classi di archiviazione predefinite AKS. La configurazione predefinita usata in questa esercitazione è adatta per ambienti di sviluppo/test.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Prerequisiti

- Una sottoscrizione di Azure.
- [Strumenti per Big Data](deploy-big-data-tools.md):
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **Estensione SQL Server 2019**
   - **Interfaccia della riga di comando di Azure**

## <a name="log-in-to-your-azure-account"></a>Accedere al proprio account Azure

Lo script usa l'interfaccia della riga di comando di Azure per automatizzare la creazione di un cluster AKS. Prima di eseguire lo script, è necessario accedere al proprio account Azure con l'interfaccia della riga di comando di Azure almeno una volta. Eseguire il comando seguente da un prompt dei comandi.

```
az login
```

## <a name="download-the-deployment-script"></a>Scaricare lo script di distribuzione

Questa esercitazione automatizza la creazione del cluster Big Data su AKS usando uno script Python **deploy-SQL-Big-Data-AKS.py**. Se è già stato installato Python per **azdata**, sarà possibile eseguire lo script correttamente in questa esercitazione. 

In un prompt di Windows PowerShell o Linux Bash eseguire il comando seguente per scaricare lo script di distribuzione da GitHub.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>Eseguire lo script di distribuzione

Usare la procedura seguente per eseguire lo script di distribuzione. Questo script creerà un servizio AKS in Azure e quindi distribuirà un cluster SQL Server 2019 Big Data a AKS. È anche possibile modificare lo script con altre [variabili di ambiente](deployment-guidance.md#configfile) per creare una distribuzione personalizzata.

1. Eseguire lo script con il comando seguente:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Se si dispone sia di Python3 che di python2 nel computer client e nel percorso, è necessario eseguire il comando usando python3: `python3 deploy-sql-big-data-aks.py`.

1. Quando richiesto, immettere le informazioni seguenti:

   | Value | Descrizione |
   |---|---|
   | **ID sottoscrizione di Azure** | ID sottoscrizione di Azure da usare per AKS. È possibile elencare tutte le sottoscrizioni e i relativi ID `az account list` eseguendo da un'altra riga di comando. |
   | **Gruppo di risorse di Azure** | Nome del gruppo di risorse di Azure da creare per il cluster AKS. |
   | **Area di Azure** | Area di Azure per il nuovo cluster AKS (valore predefinito westus). |
   | **Dimensioni del computer** | [Dimensioni del computer](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) da usare per i nodi nel cluster AKS (impostazione predefinita **Standard_L8s**). |
   | **Nodi di lavoro** | Il numero di nodi del ruolo di lavoro nel cluster AKS (valore predefinito **1**). |
   | **Nome del cluster** | Il nome del cluster AKS e del cluster Big Data. Il nome del cluster Big Data deve contenere solo caratteri alfanumerici minuscoli e non spazi. (valore predefinito **sqlbigdata**). |
   | **Password** | Password per il controller, il gateway HDFS/Spark e l'istanza master (valore predefinito **MySQLBigData2019**). |
   | **Utente controller** | Nome utente per l'utente del controller (impostazione predefinita: **admin**). |

I seguenti parametri sono necessari per i partecipanti al programma SQL Server 2019 Big Data cluster early adopter: **Nome utente Docker**e **password Docker**. A partire dalla versione CTP 3,2 non sono più necessari.

   > [!IMPORTANT]
   > Le dimensioni predefinite del computer **Standard_L8s** potrebbero non essere disponibili in ogni area di Azure. Se si selezionano dimensioni diverse del computer, assicurarsi che il numero totale di dischi che possono essere collegati tra i nodi del cluster sia maggiore o uguale a 24. Ogni attestazione di volume permanente nel cluster richiede un disco collegato. Attualmente, Big Data cluster richiede 24 attestazioni del volume permanenti. Ad esempio, la dimensione del computer [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) supporta 32 dischi collegati, quindi è possibile valutare Big Data cluster con un singolo nodo della dimensione del computer.

   > [!NOTE]
   > L' `sa` account è un amministratore di sistema nell'istanza di SQL Server master che viene creata durante l'installazione. Dopo aver creato la distribuzione `MSSQL_SA_PASSWORD` , la variabile `echo $MSSQL_SA_PASSWORD` di ambiente può essere individuata eseguendo nel contenitore dell'istanza master. Per motivi di sicurezza, modificare `sa` la password nell'istanza master dopo la distribuzione. Per ulteriori informazioni, vedere [Change the sa password](../linux/quickstart-install-connect-docker.md#sapassword).

1. Lo script inizierà creando un cluster AKS usando i parametri specificati. Questo passaggio richiede alcuni minuti.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>Monitorare lo stato

Dopo aver creato il cluster AKS, lo script continua a impostare le variabili di ambiente necessarie con le impostazioni specificate in precedenza. Chiama quindi **azdata** per distribuire il cluster Big Data su AKS.

Nella finestra di comando client viene restituito lo stato di distribuzione. Durante il processo di distribuzione, verrà visualizzata una serie di messaggi in cui è in attesa del Pod del controller:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Dopo 10 o 20 minuti, è necessario ricevere una notifica che indica che il pod del controller è in esecuzione:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> L'intera distribuzione può richiedere molto tempo a causa del tempo necessario per scaricare le immagini del contenitore per i componenti del cluster Big Data. Tuttavia, non deve richiedere diverse ore. Se si verificano problemi con la distribuzione, vedere [monitoraggio e risoluzione dei problemi SQL Server cluster di Big Data](cluster-troubleshooting-commands.md).

## <a name="inspect-the-cluster"></a>Esaminare il cluster

In qualsiasi momento durante la distribuzione, è possibile usare **kubectl** o **azdata** per controllare lo stato e i dettagli sul cluster Big data in esecuzione.

### <a name="use-kubectl"></a>Usare kubectl

Aprire una nuova finestra di comando per usare **kubectl** durante il processo di distribuzione.

1. Eseguire il comando seguente per ottenere un riepilogo dello stato dell'intero cluster:

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Se il nome del cluster Big Data non è stato modificato, per impostazione predefinita lo script è **sqlbigdata**.

1. Esaminare i servizi kubernetes e i relativi endpoint interni ed esterni con il comando **kubectl** seguente:

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. È anche possibile controllare lo stato dei Pod kubernetes con il comando seguente:

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. Trovare altre informazioni su un pod specifico con il comando seguente:

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> Per informazioni dettagliate su come monitorare e risolvere i problemi relativi a una distribuzione, vedere [monitoraggio e risoluzione dei problemi SQL Server cluster di Big Data](cluster-troubleshooting-commands.md).

## <a name="connect-to-the-cluster"></a>Connettersi al cluster

Al termine dell'esecuzione dello script di distribuzione, l'output invia una notifica di esito positivo:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

Il cluster SQL Server Big Data viene ora distribuito in AKS. È ora possibile usare Azure Data Studio per connettersi al cluster. Per altre informazioni, vedere [connettersi a un cluster SQL Server Big data con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="clean-up"></a>Eseguire la pulizia

Se si sta testando SQL Server Big Data cluster in Azure, è necessario eliminare il cluster AKS al termine per evitare addebiti imprevisti. Non rimuovere il cluster se si intende continuare a usarlo.

> [!WARNING]
> La procedura seguente consente di eliminare il cluster AKS che rimuove anche il cluster SQL Server Big Data. Se si dispone di un database o di dati HDFS che si desidera memorizzare, prima di eliminare il cluster è necessario eseguire il backup dei dati.

Eseguire il comando dell'interfaccia della riga di comando di Azure seguente per rimuovere il cluster Big Data e il `<resource group name>` servizio AKS in Azure (sostituire con il **gruppo di risorse di Azure** specificato nello script di distribuzione):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>Passaggi successivi

Lo script di distribuzione ha configurato il servizio Azure Kubernetes ed è stato anche distribuito un cluster SQL Server 2019 Big Data. È anche possibile scegliere di personalizzare le distribuzioni future tramite installazioni manuali. Per altre informazioni sul modo in cui vengono distribuiti Big Data cluster e su come personalizzare le distribuzioni, vedere [How to deploy SQL Server Big Data Clusters on Kubernetes](deployment-guidance.md).

Ora che è stato distribuito il cluster SQL Server Big Data, è possibile caricare i dati di esempio ed esplorare le esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione: Caricare i dati di esempio in un cluster SQL Server 2019 Big Data](tutorial-load-sample-data.md)