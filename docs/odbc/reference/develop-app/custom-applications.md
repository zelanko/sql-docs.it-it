---
title: Applicazioni personalizzate - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df00a748ee4d5e3a63b32c95449417a1057b58e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305282"
---
# <a name="custom-applications"></a>Applicazioni personalizzate
Le applicazioni personalizzate eseguono in genere un'attività specifica per alcuni DBS. Ad esempio, un'applicazione potrebbe recuperare dati da un singolo DBMS e generare un report oppure trasferire dati tra più DBMS. Ciò che queste applicazioni hanno in comune è che questi DBS sono noti prima che l'applicazione è scritta ed è improbabile che cambi nel corso della vita dell'applicazione.  
  
 L'applicazione personalizzata richiede pertanto poca o nessuna interoperabilità. Lo sviluppatore dell'applicazione può scegliere un singolo driver per ogni DBMS e codice direttamente a tali driver. L'applicazione può contenere in modo sicuro codice specifico del driver per sfruttare le funzionalità di tali driver e potrebbe anche effettuare chiamate all'API di database nativo per utilizzare funzionalità non supportate da ODBC.  
  
 La principale preoccupazione di interoperabilità della maggior parte delle applicazioni personalizzate è se i DBSMO di destinazione cambieranno in futuro. In tal caso, questo processo può essere semplificato scrivendo codice più interoperabile per iniziare. Tuttavia, tale cambiamento di DBSMO è raro e generalmente comporta una grande quantità di lavoro. Per questo motivo, gli sviluppatori di applicazioni personalizzate raramente scelgono di aumentare l'interoperabilità a scapito delle funzionalità; di solito scelgono di ricodificare tale funzionalità quando cambiano DBS.
