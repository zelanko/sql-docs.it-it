---
title: Installare strumenti Big Data
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare gli strumenti usati [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] con (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 84c7181bfd7c0ee014b382052bb6493d68251331
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153616"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Installare gli strumenti per Big Data di SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive gli strumenti client da installare per la creazione, la gestione e l'uso [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] di (anteprima). La sezione seguente contiene un elenco di strumenti e collegamenti alle istruzioni di installazione. Prima di distribuire un cluster Big Data, configurare gli strumenti indicati come obbligatori in Windows o Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Strumenti per cluster Big Data

La tabella seguente elenca gli strumenti comuni per i cluster Big Data e indica come installarli:

| Strumento | Obbligatoria | Descrizione | Installazione |
|---|---|---|---|
| **Python** | Yes | Python è un linguaggio di programmazione di alto livello interpretato e orientato a oggetti con semantica dinamica. Molte parti dei cluster Big Data per SQL Server usano Python. | [Installare Python](#python)|
| **azdata** | Yes | Strumento da riga di comando per l'installazione e la gestione di un cluster Big Data. | [Installazione](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | Yes | Strumento da riga di comando per il monitoraggio del cluster Kuberentes sottostante ([altre informazioni](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio-SQL Server 2019 versione finale candidata (RC)** | Yes | Strumento grafico multipiattaforma per l'esecuzione di query SQL Server. | [Installazione](#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc) |
| **Estensione di SQL Server 2019** | Yes | Estensione per Azure Data Studio che supporta la connessione al cluster Big Data. Fornisce anche una procedura guidata di virtualizzazione dei dati. | [Installazione](../azure-data-studio/sql-server-2019-extension.md) |
| **Interfaccia della riga di comando di Azure**<sup>2</sup> | Per il servizio Azure Kubernetes | Interfaccia della riga di comando moderna per la gestione dei servizi di Azure. Viene usata con distribuzioni di cluster Big Data nel servizio Azure Kubernetes ([altre informazioni](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Installazione](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Facoltativo | Interfaccia della riga di comando moderna per l'esecuzione di query su SQL Server ([altre informazioni](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Per alcuni script | Strumento da riga di comando legacy per l'esecuzione di query su SQL Server ([altre informazioni](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | Per alcuni script | Strumento da riga di comando per il trasferimento di dati con URL. | [Windows](https://curl.haxx.se/windows/) \| Linux: installare il pacchetto curl |

<sup>1</sup> È necessario usare kubectl 1.10 o versioni successive. Inoltre, la versione di kubectl deve essere più o meno una versione secondaria del cluster Kubernetes. Se si vuole installare una versione specifica nel client kubectl, vedere [Installare il file binario di kubectl tramite curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl). In Windows 10 usare cmd.exe e non Windows PowerShell per eseguire curl.

> [!TIP]
> Per usare kubectl con un cluster distribuito in precedenza nel servizio Azure Kubernetes, è necessario impostare il contesto del cluster con il comando dell'interfaccia della riga di comando di Azure seguente:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> È necessario usare l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive. Eseguire `az --version` per trovare la versione, se necessario.

<sup>3</sup> Se si esegue Windows 10, **curl** si trova già in PATH quando viene eseguito da un prompt dei comandi. Per le altre versioni di Windows, scaricare **curl** usando il collegamento e inserirlo in PATH.

## <a name="which-tools-are-required"></a>Strumenti necessari

La tabella precedente contiene tutti gli strumenti comuni usati con i cluster Big Data. Gli strumenti effettivamente necessari dipendono dallo scenario. Tuttavia, in generale gli strumenti seguenti sono più importanti per la gestione del cluster, la connessione al cluster e l'esecuzione di query sul cluster:

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Estensione di SQL Server 2019**

Gli strumenti rimanenti sono necessari solo in determinati scenari. È possibile usare l'**interfaccia della riga di comando di Azure** per gestire i servizi di Azure associati alle distribuzioni nel servizio Azure Kubernetes. **mssql-cli** è uno strumento facoltativo ma utile che permette di connettersi all'istanza master di SQL Server nel cluster ed eseguire query dalla riga di comando. **sqlcmd** e **curl** sono obbligatori se si prevede di installare dati di esempio con lo script GitHub.

### <a id="python"></a> Installare Python offline

1. In un computer con accesso a Internet, scaricare uno dei file compressi seguenti contenenti Python:

   | Sistema operativo | Scarica |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copiare il file compresso nel computer di destinazione ed estrarlo nella cartella desiderata.

1. Solo per Windows, eseguire `installLocalPythonPackages.bat` dalla cartella di installazione e passare il percorso completo della cartella come parametro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc"></a>Scaricare e installare Azure Data Studio SQL Server 2019 versione finale candidata (RC)

Azure Data Studio SQL Server 2019 RC fornisce funzionalità e funzionalità specifiche per SQL Server 2019 RC.

Per le normali versioni di produzione di Azure Data Studio, seguire le istruzioni disponibili in [scaricare e installare Azure Data Studio](../azure-data-studio/download.md).

|Piattaforma|Scarica|Data di rilascio| Versione |
|:---|:---|:---|:---|
|Windows|[Programma di installazione utente (scelta consigliata)](https://go.microsoft.com/fwlink/?linkid=2102435)<br>[Programma di installazione di sistema](https://go.microsoft.com/fwlink/?linkid=2102523)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2102524)|27 agosto 2019 |RC 1.11.0-insider|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2102436)|27 agosto 2019 |RC 1.11.0-insider|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2102526)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)|27 agosto 2019 |RC 1.11.0-insider|

Per informazioni dettagliate sulla versione più recente, vedere le [note sulla versione](../big-data-cluster/release-notes-big-data-cluster.md).

### <a name="get-azure-data-studio-for-windows"></a>Ottenere Azure Data Studio per Windows

Questa versione di [!INCLUDE[name-sos](../includes/name-sos-short.md)] include un'esperienza di installazione Windows standard e un file ZIP.

Il *programma di installazione utente* è consigliato perché non richiede privilegi di amministratore, il che semplifica sia le installazioni che gli aggiornamenti. Il programma di installazione utente non richiede privilegi di amministratore perché il percorso si trova nella cartella AppData locale (LOCALAPPDATA) dell'utente. Il programma di installazione utente fornisce anche un'esperienza di aggiornamento in background più fluida. Per altre informazioni, vedere l'articolo sulla [Configurazione utente per Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).

**Programma di installazione utente** (scelta consigliata)

1. Scaricare ed eseguire il [programma di installazione *utente* di [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Windows](https://go.microsoft.com/fwlink/?linkid=2102435).
2. Avviare l'app [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Programma di installazione di sistema**

1. Scaricare ed eseguire il [programma di installazione *di sistema* di [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Windows](https://go.microsoft.com/fwlink/?linkid=2102523).
2. Avviare l'app [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**.zip file**

1. Scaricare lo [ZIP di [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Windows](https://go.microsoft.com/fwlink/?linkid=2102524).
2. Individuare il file scaricato ed estrarlo.
3. Eseguire `\azuredatastudio-windows\azuredatastudio.exe`

### <a name="get-azure-data-studio-for-macos"></a>Ottenere Azure Data Studio per macOS

1. Scaricare [[!INCLUDE[name-sos](../includes/name-sos-short.md)] per macOS](https://go.microsoft.com/fwlink/?linkid=2102436).
2. Per espandere il contenuto del file ZIP, fare doppio clic su di esso.
3. Per rendere [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponibile nel *Launchpad*, trascinare *Azure Data Studio.app* nella cartella *Applicazioni*.

### <a name="get-azure-data-studio-for-linux"></a>Ottenere Azure Data Studio per Linux

1. Scaricare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per Linux usando uno dei programmi di installazione o l'archivio tar.gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2102526)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)
1. Per estrarre il file e avviare [!INCLUDE[name-sos](../includes/name-sos-short.md)], aprire una nuova finestra del terminale e digitare i comandi seguenti:

   **Installazione Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **Installazione RPM:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **Installazione tar.gz:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > In Debian, Redhat e Ubuntu, potrebbero mancare alcune dipendenze. Per installarle, a seconda della versione di Linux, utilizzare i comandi seguenti:
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **RedHat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

### <a name="supported-operating-systems"></a>Sistemi operativi supportati

[!INCLUDE[name-sos](../includes/name-sos-short.md)] è supportato in Windows, macOS e Linux, sulle piattaforme seguenti:

#### <a name="windows"></a>Windows

- Windows 10 (64 bit)
- Windows 8.1 (64 bit)
- Windows 8 (64 bit)
- Windows 7 (SP1) (64 bit) - Richiede [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2 (64 bit)
- Windows Server 2012 (64 bit)
- Windows Server 2008 R2 (64 bit)

#### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato gli strumenti, distribuire un cluster Big Data di SQL Server 2019 in Kubernetes nel cloud o in locale. Per altre informazioni, vedere gli articoli sulla distribuzione seguenti:

- [Avvio rapido: Distribuire un cluster Big Data di SQL Server nel servizio Azure Kubernetes](quickstart-big-data-cluster-deploy.md)
- [Come eseguire la [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] distribuzione in Kubernetes](deployment-guidance.md)

Per ulteriori informazioni sui cluster di Big Data, vedere [che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md).
