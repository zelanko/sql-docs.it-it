---
title: Installare strumenti Big Data
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare gli strumenti usati con i cluster Big Data di SQL Server 2019 (anteprima).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 757209ff89fd40dcc737b65d3b19f2a7d4ef247b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419463"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Installare SQL Server 2019 Big Data Tools

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive gli strumenti client che devono essere installati per la creazione, la gestione e l'uso di SQL Server 2019 cluster di Big Data (anteprima). Nella sezione seguente viene fornito un elenco di strumenti e collegamenti alle istruzioni di installazione. Prima di distribuire un cluster di Big Data, configurare gli strumenti contrassegnati come necessari in Windows o Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Strumenti cluster per Big Data

La tabella seguente elenca gli strumenti comuni del cluster Big Data e come installarli:

| Strumento | Obbligatoria | Descrizione | Installazione |
|---|---|---|---|
| **Python** | Yes | Python è un linguaggio di programmazione di alto livello interpretato e orientato a oggetti con semantica dinamica. Molte parti di cluster Big Data per SQL Server usano Python. | [Installare Python](#python)|
| **azdata** | Yes | Strumento da riga di comando per l'installazione e la gestione di un cluster Big Data. | [Installazione](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | Yes | Strumento da riga di comando per il monitoraggio del cluster Kuberentes sottostante ([altre informazioni](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio (Insider)** | Yes | Strumento grafico multipiattaforma per l'esecuzione di query SQL Server ([altre informazioni](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)). | [Installazione](https://aka.ms/azdata-insiders) |
| **Estensione SQL Server 2019** | Yes | Estensione per Azure Data Studio che supporta la connessione al cluster di Big Data. Fornisce anche una data Virtualization Wizard. | [Installazione](../azure-data-studio/sql-server-2019-extension.md) |
| **Interfaccia** della riga di comando di Azure <sup>2</sup> | Per AKS | Interfaccia della riga di comando moderna per la gestione dei servizi di Azure. Usato con le distribuzioni del cluster AKS Big Data ([altre informazioni](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Installazione](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Facoltativo | Interfaccia della riga di comando moderna per eseguire query SQL Server ([altre informazioni](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Per alcuni script | Strumento da riga di comando legacy per eseguire query SQL Server ([altre informazioni](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | Per alcuni script | Strumento da riga di comando per il trasferimento di dati con URL. | [Windows](https://curl.haxx.se/windows/) \| Linux: installare il pacchetto CURL |

<sup>1</sup> è necessario usare kubectl versione 1,10 o successiva. Inoltre, la versione di kubectl deve essere più o meno una versione secondaria del cluster Kubernetes. Se si vuole installare una versione specifica nel client di kubectl, vedere [Install kubectl Binary by curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (in Windows 10, usare cmd. exe e non Windows PowerShell per eseguire curl). 

> [!TIP]
> Per usare kubectl con un cluster distribuito in precedenza in Azure Kubernetes Service (AKS), è necessario impostare il contesto del cluster con il comando dell'interfaccia della riga di comando di Azure seguente:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> è necessario usare l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva. Eseguire `az --version` per trovare la versione, se necessario.

<sup>3</sup> se si esegue Windows 10, **curl** si trova già nel percorso quando viene eseguito da un prompt dei comandi. Per le altre versioni di Windows, scaricare **curl** usando il collegamento e posizionarlo nel percorso.

## <a name="which-tools-are-required"></a>Quali sono gli strumenti necessari?

Nella tabella precedente sono disponibili tutti gli strumenti comuni utilizzati con i cluster Big Data. Gli strumenti necessari dipendono dallo scenario. Tuttavia, in generale, gli strumenti seguenti sono più importanti per la gestione, la connessione e l'esecuzione di query sul cluster:

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Estensione SQL Server 2019**

Gli strumenti rimanenti sono necessari solo in determinati scenari. L'interfaccia della riga di comando di **Azure** può essere usata per gestire i servizi di Azure associati alle distribuzioni AKS. **MSSQL-CLI** è uno strumento facoltativo ma utile che consente di connettersi all'istanza di SQL Server master nel cluster ed eseguire query dalla riga di comando. E **SQLCMD** e **curl** sono necessari se si prevede di installare dati di esempio con lo script github.

### <a id="python"></a>Installare Python offline

1. In un computer con accesso a Internet, scaricare uno dei file compressi seguenti contenenti Python:

   | Sistema operativo | Scarica |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copiare il file compresso nel computer di destinazione ed estrarlo in una cartella di propria scelta.

1. Solo per Windows, eseguire `installLocalPythonPackages.bat` da tale cartella e passare il percorso completo della stessa cartella come parametro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato gli strumenti, distribuire un cluster SQL Server 2019 Big Data in Kubernetes nel cloud o in locale. Per ulteriori informazioni, vedere gli articoli seguenti relativi alla distribuzione:

- [Avvio rapido: Distribuire SQL Server cluster Big Data in Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
- [Come distribuire cluster di Big Data SQL Server in Kubernetes](deployment-guidance.md)

Per altre informazioni sui cluster di Big Data, vedere [che cosa sono i cluster SQL Server 2019 Big Data?](big-data-cluster-overview.md).
