---
title: Connettersi a un gruppo di disponibilità Always On di SQL Server in un cluster Kubernetes
description: Questo articolo illustra come connettersi a un gruppo di disponibilità Always On
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f05bc51f587723414d3b0a4090fe2b27ad5fb837
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952609"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>Connettersi a un gruppo di disponibilità Always On di SQL Server in Kubernetes

Per connettersi a istanze di SQL Server in contenitori in un cluster Kubernetes, creare [un servizio di bilanciamento del carico](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer). Il servizio di bilanciamento del carico è un endpoint che contiene un indirizzo IP e inoltra le richieste per l'indirizzo IP al pod che esegue l'istanza di SQL Server.

Per connettersi a una replica del gruppo di disponibilità, creare un servizio per tipi di replica diversi. È possibile vedere esempi di servizi per diversi tipi di repliche in [sql-server-samples/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

* `ag1-primary` punta alla replica primaria.
* `ag1-secondary` punta a una qualsiasi replica secondaria.

Se sono presenti più repliche secondarie, Kubernetes instrada la connessione alle diverse repliche secondo il metodo round robin.

## <a name="create-a-load-balancer-service"></a>Creare un servizio di bilanciamento del carico

Per creare servizi di bilanciamento del carico per il database primario e le repliche, copiare [`ag1-services.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) da [sql-server-samples](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file) e aggiornarlo per il gruppo di disponibilità in uso.

Il comando seguente applica la configurazione dal file `.yaml` al cluster:

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>Ottenere l'indirizzo IP per il servizio di bilanciamento del carico

Per ottenere l'indirizzo IP per il servizio di bilanciamento del carico, eseguire

```kubectl
kubectl get services
```

Identificare l'indirizzo IP del servizio a cui ci si vuole connettere.

## <a name="connect-to-primary-replica"></a>Connettersi alla replica primaria

Per connettersi alla replica primaria con l'autenticazione SQL, usare l'account `sa`, il valore di `sapassword` nel segreto creato in precedenza e questo indirizzo IP.

Esempio:

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>Passaggi successivi

[Gestire un gruppo di disponibilità di SQL Server in un cluster Kubernetes](sql-server-linux-kubernetes-manage.md)

[Gruppo di disponibilità di SQL Server nel cluster Kubernetes](sql-server-ag-kubernetes.md)
