---
title: Gestire SQL Server cluster Big Data con il dashboard del controller
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: Usare un notebook di Azure Data Studio per gestire e risolvere problemi relativi a un cluster Big Data.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 08/29/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5fadb9b069e6f70cb780e6dc69295f63330a683a
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160723"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>Gestire i cluster di Big Data per il dashboard del controller SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Oltre a **azdata** e al notebook di stato del cluster, esiste un altro modo per visualizzare lo stato di un cluster SQL Server Big Data. È ora possibile aggiungere il SQL Server controller del cluster Big data tramite le **connessioni** viewlet. In questo modo è possibile disporre di un dashboard per visualizzare l'integrità del cluster.

![dashboard](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>Prerequisiti

Per avviare il notebook sono necessari i prerequisiti seguenti:

* Versione più recente di [Build Insider per Azure Data Studio Insider](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc)
* Estensione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] installata in Azure Data Studio

Oltre alla versione precedente, è necessario anche SQL Server cluster di Big Data 2019:

* **azdata**
    - [Gestione pacchetti Linux](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli)


## <a name="add-sql-server-big-data-cluster-controller"></a>Aggiungere SQL Server controller del cluster Big Data

1. Fare clic sulla visualizzazione connessioni nel riquadro sinistro.
2. Nella parte inferiore della visualizzazione connessioni fare clic su **SQL Server cluster di Big Data** per espanderlo.
3. Fare clic su **aggiungi SQL Server Big data controller del cluster**. verrà avviata una nuova finestra di dialogo.

## <a name="add-new-controller"></a>Aggiungi nuovo controller

1. Aggiungere il nome del cluster.
2. Aggiungere l'URL del servizio Gestione cluster. Questa operazione è disponibile nella tabella degli endpoint di servizio del dashboard BDC oppure rivolgersi all'amministratore del cluster.
3. Aggiungere il nome utente e la password.

## <a name="launch-controller-dashboard"></a>Avviare il dashboard del controller

1. Quando il controller viene aggiunto correttamente, è possibile visualizzarlo in SQL Server cluster di Big Data.
2. Per avviare il dashboard, fare clic con il pulsante destro delmouse sul controller e scegliere Gestisci.

## <a name="controller-dashboard"></a>Dashboard del controller

1. Nel dashboard del controller sono presenti tre componenti principali:

    - **Barra degli strumenti** nella parte superiore che contiene azioni per il dashboard.
    - **Riquadro** di spostamento a sinistra che consente di modificare le diverse visualizzazioni nel dashboard.
    - **Visualizzazione** che copre la maggior parte della pagina.

2. Nella pagina **Panoramica del cluster di Big Data** è possibile vedere:

    - **Proprietà del cluster** per visualizzare le informazioni sul cluster.
    - **Panoramica dei cluster** per visualizzare una panoramica di alto livello di tutti i componenti del cluster e quelli che non sono integri
    - **Endpoint di servizio** per la copia o l'accesso a servizi diversi all'interno del cluster SQL Server Big Data.

3. Nel **riquadro NAV** è possibile visualizzare l'elenco dei servizi e fare clic su uno per visualizzare ulteriori dettagli sul cluster. Si tratta delle stesse visualizzazioni quando si fa clic su un servizio in **Panoramica cluster.**

4. Ogni visualizzazione in **Dettagli cluster** è costituita dagli stessi componenti dell'interfaccia utente:

    - **Dettagli sullo** stato di integrità che condividono lo stato e lo stato di integrità del componente.
    - **Metriche e log** per visualizzare metriche e log aggiuntivi tramite Grafana e Kibana.

1. Se si visualizza un componente non integro, fare clic su **risoluzione dei problemi** sulla barra degli strumenti per avviare un libro Jupyter contenente un notebook per facilitare la diagnosi del problema.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul controller, vedere la [documentazione del controller](concept-controller.md).