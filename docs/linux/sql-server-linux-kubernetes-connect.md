---
title: Connettersi a SQL Server gruppo di disponibilità AlwaysOn nel cluster Kubernetes
description: Questo articolo illustra come connettersi a un gruppo di disponibilità AlwaysOn
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f05bc51f587723414d3b0a4090fe2b27ad5fb837
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952609"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>Connettersi a SQL Server Always On Availability Group nel Kubernetes

Per connettersi alle istanze di SQL Server in contenitori in un cluster Kubernetes, creare un [servizio di bilanciamento del carico](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer). Il servizio di bilanciamento del carico è un endpoint. Include un indirizzo IP e inoltra le richieste per l'indirizzo IP nel POD in esecuzione l'istanza di SQL Server.

Per connettersi a una replica del gruppo di disponibilità, creare un servizio per i tipi di replica diverse. È possibile visualizzare esempi di servizi per i diversi tipi di repliche [sql-server-samples/gruppo di disponibilità-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

* `ag1-primary` punta alla replica primaria.
* `ag1-secondary` punta a qualsiasi replica secondaria.

Se più di una replica secondaria, Kubernetes indirizza la connessione per le diverse repliche secondo uno schema round-robin.

## <a name="create-a-load-balancer-service"></a>Creare un servizio di bilanciamento del carico

Per creare servizi di bilanciamento carico per l'enclosure principale e le repliche, copiare [ `ag1-services.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) dalla [sql-server-samples](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file) e aggiornarlo per il gruppo di disponibilità.

Il comando seguente applica la configurazione dal `.yaml` file al cluster:

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>Ottenere l'indirizzo IP per il servizio di bilanciamento del carico

Per ottenere l'indirizzo IP di bilanciamento del carico per il servizio di bilanciamento del carico, eseguire

```kubectl
kubectl get services
```

Identificare l'indirizzo IP del servizio che si desidera connettersi.

## <a name="connect-to-primary-replica"></a>Connettersi alla replica primaria

Per connettersi alla replica primaria con l'autenticazione di SQL, usare il `sa` account, il valore per `sapassword` dal segreto creato e questo indirizzo IP.

Ad esempio:

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>Passaggi successivi

[Gestire il gruppo di disponibilità SQL Server in cluster Kubernetes](sql-server-linux-kubernetes-manage.md)

[Gruppo di disponibilità SQL Server in cluster Kubernetes](sql-server-ag-kubernetes.md)
