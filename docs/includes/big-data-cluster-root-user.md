---
author: MikeRayMSFT
ms.prod: sql
ms.technology: big-data-cluster
ms.topic: include
ms.date: 06/22/2020
ms.author: mikeray
ms.openlocfilehash: b72f8044638adbf75049392fae32447a8a749a6d
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85215126"
---
A partire da SQL Server 2019 CU5, quando si distribuisce un nuovo cluster con l'autenticazione di base, tutti gli endpoint, incluso il gateway, usano `AZDATA_USERNAME` e `AZDATA_PASSWORD`. Gli endpoint nei cluster aggiornati a CU5 continuano a usare `root` come nome utente per la connessione all'endpoint del gateway. Questa modifica non si applica alle distribuzioni che usano l'autenticazione Active Directory. Vedere [Credenziali per l'accesso ai servizi tramite l'endpoint del gateway](../big-data-cluster/release-notes-big-data-cluster.md#credentials-for-accessing-services-through-gateway-endpoint) nelle note sulla versione.