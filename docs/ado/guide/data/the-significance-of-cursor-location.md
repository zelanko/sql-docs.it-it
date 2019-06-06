---
title: Il significato della posizione del cursore | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ed59dc8c4dd2cc53c4ad86992e5b778f0f8b17ac
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704834"
---
# <a name="the-significance-of-cursor-location"></a>Significato della posizione del cursore
Ogni cursore utilizza risorse temporanee per conservare i relativi dati. Queste risorse possono essere memoria, un file di paging su disco, i file del disco temporaneo o un archivio temporaneo nel database. Il cursore viene chiamato un *lato client* cursore quando queste risorse si trovano nel computer client. Il cursore viene chiamato un *sul lato server* cursore quando queste risorse si trovano nel server.  
  
## <a name="client-side-cursors"></a>Cursori sul lato client  
 In ADO chiamare per un cursore sul lato client usando la **adUseClient CursorLocationEnum.** Con un cursore lato client non keyset, il server invia l'intero set di risultati attraverso la rete a computer client. Il client fornisce e gestisce le risorse temporanee necessarie per il set di risultati e cursore. L'applicazione lato client può passare attraverso l'intero set di risultati a determinare quali righe richiede.  
  
 I cursori sul lato client statici e gestito da keyset possono generare un carico notevole nella workstation se includono troppe righe. Anche se tutte le librerie di cursore sono in grado di generare i cursori con migliaia di righe, le applicazioni progettate per recuperare tali set di righe di grandi dimensioni potrebbero offrire prestazioni ridotte. Sono presenti eccezioni, ovviamente. Per alcune applicazioni, un cursore lato client di grandi dimensioni potrebbe essere perfettamente appropriato e le prestazioni potrebbero non costituire un problema.  
  
 Un beneficio ovvio del cursore lato client è una risposta rapida. Dopo aver scaricato il set di risultati al computer client, le righe di esplorazione è molto veloce. L'applicazione è in genere più scalabile con i cursori sul lato client, perché i requisiti delle risorse del cursore vengono inseriti in ogni client separata e non nel server.  
  
## <a name="server-side-cursors"></a>Cursori sul lato server  
 In ADO chiamare per un cursore sul lato server usando il **adUseServer CursorLocationEnum.** Con un cursore lato server, il server gestisce il set di risultati utilizzando le risorse fornite dal computer del server. Il cursore sul lato server restituisce solo i dati richiesti tramite la rete. Questo tipo di cursore in alcuni casi possa fornire prestazioni migliori rispetto a cursore lato client, specialmente in situazioni in cui un numero eccessivo traffico di rete è un problema.  
  
 Tuttavia, è importante sottolineare che un cursore lato server, almeno temporaneamente - utilizza risorse del server per tutti i client attivi. È necessario pianificare di conseguenza per assicurarsi che l'hardware del server sia in grado di gestire tutti i cursori sul lato server richiesti dai client attivi. Inoltre, un cursore lato server può essere lento in quanto fornisce l'accesso alle righe solo singole: non è disponibile nessun cursore di batch.  
  
 I cursori sul lato server sono utili durante l'inserimento, aggiornamento o l'eliminazione di record. Con cursori sul lato server, si possono avere più istruzioni attive nella stessa connessione.
