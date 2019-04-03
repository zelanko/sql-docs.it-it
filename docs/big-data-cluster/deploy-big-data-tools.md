---
title: Installare strumenti Big Data
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare gli strumenti utilizzati con i cluster di big data di SQL Server 2019 (anteprima).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: dc53bdfb71efeafd55752686ff136355bc79bd34
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860482"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Installare strumenti di SQL Server 2019 big data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo vengono descritti gli strumenti client che devono essere installati per la creazione, la gestione, e tramite SQL Server 2019 dei big data cluster (anteprima). La sezione seguente fornisce un elenco di strumenti e i collegamenti alle istruzioni di installazione. Prima di distribuire un cluster di big data, configurare gli strumenti contrassegnato come obbligatorio in Windows o Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Strumenti di cluster di big data

La tabella seguente elenca i comuni strumenti di cluster di big data e come installarli:

| Strumento | Obbligatorio | Descrizione | Installazione |
|---|---|---|---|
| **mssqlctl** | Yes | Strumento da riga di comando per l'installazione e la gestione di un cluster di big data. | [Installazione](deploy-install-mssqlctl.md) |
| **kubectl**<sup>1</sup> | Yes | Strumento da riga di comando per il monitoraggio del cluster sottostante Kuberentes ([altre informazioni](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio** | Yes | Lo strumento con interfaccia grafico multipiattaforma per l'esecuzione di query SQL Server ([altre informazioni](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)). | [Installazione](../azure-data-studio/download.md) |
| **Estensione di SQL Server 2019** | Yes | Estensione di Studio di dati di Azure che supporta la connessione al cluster di big data. Fornisce inoltre una procedura guidata la virtualizzazione dei dati. | [Installazione](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | Per AKS | Interfaccia della riga di comando moderna per la gestione dei servizi di Azure. Utilizzato con le distribuzioni di cluster AKS dei big data ([altre informazioni](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Installazione](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Facoltativo | Interfaccia della riga di comando moderna per le query di SQL Server ([altre informazioni](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Per alcuni alfabeti | Strumento da riga di comando legacy per le query di SQL Server ([altre informazioni](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | Per alcuni alfabeti | Strumento da riga di comando per il trasferimento dei dati con gli URL. | [Windows](https://curl.haxx.se/windows/) \| Linux: pacchetto di installazione curl |

<sup>1</sup> è necessario usare kubectl 1.10 o versione successiva. Inoltre, la versione di kubectl deve essere più o meno una versione secondaria del cluster Kubernetes. Se si vuole installare una versione specifica nel client kubectl, vedere [installare kubectl binari tramite curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (in Windows 10, usare cmd.exe e non Windows PowerShell per eseguire curl). 

> [!TIP]
> Per usare kubectl con un cluster distribuito in precedenza in Azure Kubernetes Service (AKS), è necessario impostare il contesto del cluster con il comando di Azure:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> è necessario usare il comando di Azure versione 2.0.4 o versioni successive. Eseguire `az --version` per trovare la versione, se necessario.

<sup>3</sup> se si eseguono in Windows 10 **curl** è già presente nel percorso durante l'esecuzione da un prompt dei comandi. Per altre versioni di Windows, scaricare **curl** usando il collegamento e posizionarlo nel percorso.

## <a name="which-tools-are-required"></a>Quali strumenti sono necessari?

Nella tabella precedente vengono tutti gli strumenti comuni che vengono usati con i cluster di big data. Quali strumenti sono necessari dipende dallo scenario. Ma in generale, gli strumenti seguenti sono importanti per la gestione, la connessione a e l'esecuzione di query del cluster:

- **mssqlctl**
- **Kubectl**
- **Azure Data Studio**
- **Estensione di SQL Server 2019**

Gli altri strumenti sono necessarie solo in determinati scenari. **Interfaccia della riga di comando Azure** può essere utilizzato per gestire servizi di Azure associati alla distribuzione di AKS. **MSSQL-cli** è uno strumento facoltativo ma utile che consente di connettersi all'istanza master di SQL Server nel cluster ed eseguire query dalla riga di comando. E **sqlcmd** e **curl** sono necessarie se si prevede di installare dati di esempio con lo script di GitHub.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato gli strumenti, distribuire un cluster di big data di SQL Server 2019 Kubernetes nel Cloud o in locale. Per altre informazioni, vedere gli articoli di distribuzione seguenti:

- [Avvio rapido: Distribuire il cluster di big data di SQL Server in Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
- [Come distribuire i cluster di big data di SQL Server in Kubernetes](deployment-guidance.md)

Per altre informazioni sui cluster di big data, vedi [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
