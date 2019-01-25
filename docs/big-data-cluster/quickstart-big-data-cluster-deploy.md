---
title: Guida introduttiva alla distribuzione
titleSuffix: SQL Server 2019 big data clusters
description: Procedura dettagliata di una distribuzione di cluster di big data 2019 Server SQL (anteprima) in Azure Kubernetes Service (AKS).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/17/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 3495d41028f72093b58f546d3da2139ff02b848d
ms.sourcegitcommit: 299b63e04498eba22659970cd077f247c1657931
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898986"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Guida introduttiva: Distribuire il cluster di big data di SQL Server in Azure Kubernetes Service (AKS)

In questa Guida introduttiva si usa uno script di distribuzione di esempio per distribuire cluster di big data 2019 Server SQL (anteprima) per Azure Kubernetes Service (AKS). 

> [!TIP]
> Servizio contenitore di AZURE è solo una delle opzioni per l'hosting di Kubernetes per i cluster di big data. Per altre informazioni sulle altre opzioni di distribuzione nonché come opzioni per personalizzare la distribuzione, vedere [come distribuire i dati di grandi dimensioni di SQL Server di cluster in Kubernetes](deployment-guidance.md).

La distribuzione di cluster di big data predefinita usata in questo esempio è costituito da un'istanza di SQL Master, istanza del pool di uno calcolo, due istanze del pool di dati e due istanze del pool di archiviazione. I dati viene mantenuti usando volumi permanenti Kubernetes che usano le classi di archiviazione predefinito AKS. La configurazione predefinita usata in questa Guida introduttiva è adatta per ambienti di sviluppo/test.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Prerequisiti

- Una sottoscrizione di Azure.
- [Gli strumenti dei big data](deploy-big-data-tools.md):
   - **mssqlctl**
   - **kubectl**
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **Comando di Azure**

## <a name="log-in-to-your-azure-account"></a>Accedere al proprio account Azure

Lo script usa CLI di Azure per automatizzare la creazione di un cluster AKS. Prima di eseguire lo script, è necessario accedere al proprio account Azure con Azure CLI almeno una volta. Eseguire il comando seguente al prompt dei comandi.

```
az login
```

## <a name="download-the-deployment-script"></a>Scaricare lo script di distribuzione

Questa Guida introduttiva consente di automatizzare la creazione del cluster di big data nel servizio contenitore di AZURE usando uno script di python **distribuire-sql-big-data-aks.py**. Se già installato python per **mssqlctl**, dovrebbe essere possibile eseguire lo script in questa Guida introduttiva. 

In un prompt di bash di Linux o Windows PowerShell, eseguire il comando seguente per scaricare lo script di distribuzione da GitHub.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>Eseguire lo script di distribuzione

Usare la procedura seguente per eseguire lo script di distribuzione. Questo script crea un servizio contenitore di AZURE in Azure e quindi distribuire un cluster di big data di SQL Server 2019 al servizio contenitore di AZURE. È inoltre possibile modificare lo script con loro [variabili di ambiente](deployment-guidance.md#env) per creare una distribuzione personalizzata.

1. Eseguire lo script con il comando seguente:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Se si dispone sia python3 python2 nel computer client e nel percorso, è necessario eseguire il comando usando python3: `python3 deploy-sql-big-data-aks.py`.

1. Quando richiesto, immettere le informazioni seguenti:

   | Value | Descrizione |
   |---|---|
   | **ID sottoscrizione di Azure** | L'ID sottoscrizione di Azure da usare per AKS. È possibile elencare tutte le sottoscrizioni e i relativi ID eseguendo `az account list` da un'altra riga di comando. |
   | **Gruppo di risorse di Azure** | Il nome del gruppo di risorse di Azure per creare per il cluster AKS. |
   | **Nome utente di docker** | Il nome utente Docker fornito come parte dell'anteprima pubblica limitata. |
   | **Password di docker** | La password di Docker fornita come parte dell'anteprima pubblica limitata. |
   | **Area di Azure** | L'area di Azure per il nuovo cluster servizio contenitore di AZURE (impostazione predefinita **westus**). |
   | **Dimensioni della macchina** | Il [dimensioni della macchina](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) da usare per i nodi del cluster servizio contenitore di AZURE (impostazione predefinita **Standard_L4s**). |
   | **Nodi di lavoro** | Il numero di nodi di lavoro del cluster servizio contenitore di AZURE (impostazione predefinita **3**). |
   | **Nome del cluster** | Nome del cluster servizio contenitore di AZURE sia il cluster di big data. Solo i caratteri alfanumerici minuscoli e senza spazi, deve essere il nome del cluster. (default **sqlbigdata**). |
   | **Password** | Password per l'istanza master, un gateway HDFS/Spark e un controller (impostazione predefinita **MySQLBigData2019**). |
   | **Utente controller** | Nome utente dell'utente controller (impostazione predefinita: **admin**). |

   > [!IMPORTANT]
   > Il valore predefinito **Standard_L4s** le dimensioni del computer potrebbero non essere disponibili in ogni area di Azure. Se si seleziona una dimensione di macchina diverso, assicurarsi che il numero totale di dischi che possono essere collegati tra i nodi del cluster è maggiore o uguale a 21. Ogni attestazione di volume permanente nel cluster richiede un disco collegato. Cluster di big data richiede attualmente 21 attestazioni di volume permanente. Ad esempio, il [Standard_L4s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#ls-series) dimensioni della macchina supportano 16 dischi collegati, tre nodi significa che è possibile collegare 48 dischi.

   > [!NOTE]
   > Il `sa` account sia un amministratore di sistema nell'istanza master di SQL Server che viene creato durante l'installazione. Dopo aver creato la distribuzione, il `MSSQL_SA_PASSWORD` variabile di ambiente diventa individuabile eseguendo `echo $MSSQL_SA_PASSWORD` nel contenitore istanza master. Per motivi di sicurezza, modificare il `sa` password nell'istanza di master dopo la distribuzione. Per altre informazioni, vedere [modificare la password SA](../linux/quickstart-install-connect-docker.md#sapassword).

1. Lo script verrà avviato mediante la creazione di un cluster AKS usando i parametri specificati. Questo passaggio richiede alcuni minuti.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>Monitorare lo stato

Dopo che lo script crea il cluster AKS, procede per impostare le variabili di ambiente necessarie con le impostazioni specificate in precedenza. Chiama poi **mssqlctl** per distribuire il cluster di big data nel servizio contenitore di AZURE.

La finestra di comando client restituirà lo stato della distribuzione. Durante il processo di distribuzione, verrà visualizzato una serie di messaggi in cui è in attesa il pod controller:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Dopo 10 a 20 minuti, si dovrebbe ricevere una notifica che il pod controller sia in esecuzione:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.222.222.222:30080
```

> [!IMPORTANT]
> L'intera distribuzione può richiedere molto tempo a causa del tempo necessario per scaricare le immagini del contenitore per i componenti del cluster di big data. Tuttavia, non richiederà alcune ore. Se si verificano problemi con la distribuzione, vedere la [risoluzione dei problemi di distribuzione](deployment-guidance.md#troubleshoot) sezione dell'articolo di istruzioni di distribuzione.

## <a name="inspect-the-cluster"></a>Esaminare il cluster

In qualsiasi momento durante la distribuzione, è possibile usare kubectl o il portale di amministrazione Cluster per controllare lo stato e i dettagli relativi al cluster in esecuzione big data.

### <a name="use-kubectl"></a>Usare kubectl

Aprire una nuova finestra di comando da utilizzare **kubectl** durante il processo di distribuzione.

1. Eseguire il comando seguente per ottenere un riepilogo dello stato dell'intero cluster:

   ```
   kubectl get all -n <your-cluster-name>
   ```

1. Controllare i servizi di kubernetes e i relativi endpoint interni ed esterni con quanto segue **kubectl** comando:

   ```
   kubectl get svc -n <your-cluster-name>
   ```

1. È anche possibile esaminare lo stato dei POD kubernetes con il comando seguente:

   ```
   kubectl get pods -n <your-cluster-name>
   ```

1. Scopri ulteriori informazioni su un pod specifico con il comando seguente:

   ```
   kubectl describe pod <pod name> -n <your-cluster-name>
   ```

> [!TIP]
> Per altre informazioni su come monitorare e risolvere i problemi di una distribuzione, vedere la [risoluzione dei problemi di distribuzione](deployment-guidance.md#troubleshoot) sezione dell'articolo di istruzioni di distribuzione.

### <a name="use-the-cluster-administration-portal"></a>Usare il portale di amministrazione del Cluster

Il pod Controller è in esecuzione, è possibile utilizzare anche nel portale di amministrazione Cluster per monitorare la distribuzione. È possibile accedere al portale con l'esterno indirizzo IP e porta numero per il `service-proxy-lb` (ad esempio: **https://\<ip-address\>: 30777/portale**). Le credenziali usate per accedere al portale corrispondano ai valori per **utente Controller** e **Password** specificato nello script di distribuzione.

È possibile ottenere l'indirizzo IP del **service-proxy-lb** servizio eseguendo questo comando in una finestra bash o cmd:

```bash
kubectl get svc service-proxy-lb -n <your-cluster-name>
```

> [!NOTE]
> Nella versione CTP 2.2, si verrà visualizzato un avviso di sicurezza all'accesso alla pagina web, perché i cluster di big data è attualmente in uso certificati SSL generati automaticamente. Inoltre, in CTP 2.2, non è visibile lo stato dell'istanza master di SQL Server.

## <a name="connect-to-the-cluster"></a>Connettersi al cluster

Al termine dello script di distribuzione, l'output invia una notifica di esito positivo:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

Il cluster di big data di SQL Server è stato distribuito nel servizio contenitore di AZURE. È ora possibile usare Studio di Azure Data per connettersi all'istanza master di SQL Server e gli endpoint HDFS/Spark usando Azure Data Studio.

### <a id="master"></a> Istanza master

L'istanza master di SQL Server è un'istanza di SQL Server tradizionale che contiene i database relazionali di SQL Server. I passaggi seguenti descrivono come connettersi all'istanza master usando Azure Data Studio.

1. Dalla riga di comando, trovare l'indirizzo IP dell'istanza master con il comando seguente:

   ```
   kubectl get svc endpoint-master-pool -n <your-cluster-name>
   ```

1. In Azure Data Studio, premere **F1** > **nuova connessione**.

1. Nelle **tipo di connessione**, selezionare **Microsoft SQL Server**.

1. Digitare l'indirizzo IP dell'istanza master di SQL Server nella **nome Server** (ad esempio: **\<Indirizzo IP\>, 31433**).

1. Immettere un account di accesso SQL **nome utente** (`SA`) e **Password** (la password specificata nello script di distribuzione).

1. Modificare la destinazione **nome del Database** a uno dei database relazionali.

   ![Connettersi all'istanza master](./media/quickstart-big-data-cluster-deploy/connect-to-cluster.png)

1. Premere **Connect**e il **Dashboard di Server** dovrebbe essere visualizzato.

### <a id="hdfs"></a> Gateway HDFS/Spark

Il **gateway HDFS/Spark** consente di connettersi per funzionare con il pool di archiviazione HDFS e per eseguire processi Spark. I passaggi seguenti descrivono come connettersi con Azure Data Studio.

1. Dalla riga di comando, trovare l'indirizzo IP del gateway di HDFS/Spark con il comando seguente:

   ```
   kubectl get svc service-security-lb -n <your-cluster-name>
   ```
 
1. In Azure Data Studio, premere **F1** > **nuova connessione**.

1. Nelle **tipo di connessione**, selezionare **cluster di big data di SQL Server**.
   
   > [!TIP]
   > Se non viene visualizzato il **cluster di big data di SQL Server** connessione digitare, assicurarsi di avere installato la [estensione SQL Server 2019](../azure-data-studio/sql-server-2019-extension.md) e che Data Studio di Azure è stato riavviato dopo l'estensione completata l'installazione.

1. Digitare l'indirizzo IP del cluster di big data nelle **nome Server** (non specificare una porta).

1. Immettere `root` per il **utente** e specificare il **Password** per il cluster di big data inserito nello script di distribuzione.

   ![Connettersi al gateway HDFS/Spark](./media/quickstart-big-data-cluster-deploy/connect-to-cluster-hdfs-spark.png)

1. Premere **Connect**e il **Dashboard di Server** dovrebbe essere visualizzato.

## <a name="clean-up"></a>Pulizia

Se si siano testando i cluster di big data di SQL Server in Azure, è necessario eliminare il cluster AKS termine per evitare addebiti imprevisti. Non rimuovere il cluster se si prevede di continuare a usarlo.

> [!WARNING]
> Questa procedura chiude il cluster AKS che rimuove anche il cluster di big data di SQL Server. Se si dispone di qualsiasi database o i dati HDFS che si desidera mantenere, i dati eseguire il backup prima di eliminare il cluster.

Eseguire il comando di Azure per rimuovere il cluster di big data e il servizio contenitore di AZURE in Azure (sostituire `<resource group name>` con il **gruppo di risorse Azure** specificato nello script di distribuzione):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>Passaggi successivi

Lo script di distribuzione configurato Azure Kubernetes Service e inoltre distribuito un cluster di big data di SQL Server 2019. È anche possibile scegliere personalizzare le distribuzioni future tramite le installazioni manuali. Per altre informazioni sul modo i big data più si distribuiscono cluster, nonché come personalizzare le distribuzioni, vedere [come distribuire i dati di grandi dimensioni di SQL Server di cluster in Kubernetes](deployment-guidance.md).

Ora che viene distribuito il cluster di big data di SQL Server, è possibile caricare i dati di esempio ed esplorare le esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione: Caricare i dati di esempio in un cluster di big data di SQL Server 2019](tutorial-load-sample-data.md)