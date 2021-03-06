---
title: Monitorare il cluster con il dashboard Grafana
titleSuffix: SQL Server Big Data Clusters
description: Monitoraggio del cluster con il dashboard Grafana nel cluster Big Data di SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d258ac514cd998fd121c87a8d6da4a2694878c3e
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378394"
---
# <a name="monitor-cluster-with-azdata-and-grafana-dashboard"></a>Monitorare il cluster con azdata e il dashboard Grafana

Questo articolo descrive come monitorare un'applicazione in un cluster Big Data di SQL Server.

## <a name="prerequisites"></a>Prerequisiti

- [Cluster Big Data di SQL Server 2019](deployment-guidance.md)
- [Utilità della riga di comando azdata](deploy-install-azdata.md)

## <a name="capabilities"></a>Capabilities

In SQL Server 2019 è possibile creare, eliminare, descrivere, inizializzare, elencare, eseguire e aggiornare l'applicazione. La tabella seguente descrive i comandi per la distribuzione di applicazioni che è possibile usare con **azdata** .

|Comando |Descrizione |
|:---|:---|
|`azdata bdc endpoint list` | Elenca gli endpoint per il cluster di Big Data. |


È possibile usare l'esempio seguente per elencare l'endpoint del **dashboard Grafana** :

```bash
azdata bdc endpoint list --endpoint-name metricsui 
```

L'output indicherà l'endpoint che è possibile usare, il nome utente e la password del cluster per eseguire l'accesso. 

![Dashboard Grafana](media/big-data-cluster-monitor-apps/grafana-dashboard-endpoint.png)

I valori `nodeMetricsUrl` e `sqlMetricsUrl` forniscono un collegamento a un dashboard Grafana per il monitoraggio delle metriche dei nodi Kubernetes e delle metriche dei servizi dei cluster Big Data:

![Dashboard Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)



## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
