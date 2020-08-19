---
description: Gestione degli eventi ADO
title: Gestione degli eventi ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: rothja
ms.author: jroth
ms.openlocfilehash: 76af7a55c0f3a6e4de2caea7eb3da67e9c27c5cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453313"
---
# <a name="handling-ado-events"></a>Gestione degli eventi ADO
Il modello di eventi ADO supporta determinate operazioni ADO sincrone e asincrone che inviano *eventi*, o notifiche, prima dell'avvio o dopo il completamento dell'operazione. Un evento è in realtà una chiamata a una routine del gestore eventi definita nell'applicazione.  
  
 Se si forniscono le funzioni o le procedure del gestore per il gruppo di eventi che si verificano prima dell'avvio dell'operazione, è possibile esaminare o modificare i parametri passati all'operazione. Poiché non è ancora stato eseguito, è possibile annullare l'operazione o consentirne il completamento.  
  
 Gli eventi che si verificano dopo il completamento di un'operazione sono particolarmente importanti se si utilizza ADO in modo asincrono. Ad esempio, un'applicazione che avvia un'operazione [Recordset asincrona. Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) riceve una notifica tramite un evento di completamento dell'esecuzione al termine dell'operazione.  
  
 L'utilizzo del modello di eventi ADO comporta un sovraccarico per l'applicazione, ma offre una maggiore flessibilità rispetto ad altri metodi di gestione delle operazioni asincrone, ad esempio il monitoraggio della proprietà [state](../../../ado/reference/ado-api/state-property-ado.md) di un oggetto con un ciclo.  
  
> [!NOTE]
>  Per gestire gli eventi, ADO deve avere un message pump o essere usato in un modello STA (Single-Threaded Apartment). Gli eventi ADO vengono gestiti internamente creando una finestra nascosta. ADO invia messaggi a questa finestra quando gli eventi devono essere generati. Questa operazione viene eseguita per assicurarsi che gli eventi vengano inviati al thread che ha chiamato **IConnectionPoint:: Advise** nel punto di connessione. Questa architettura può causare problemi quando il thread che riceve le notifiche non pompa i messaggi della finestra. Tra i potenziali problemi sono inclusi gli eventi ADO che non vengono recapitati al thread e le trasmissioni di finestra globali e che potrebbero rallentare l'intero sistema perché le finestre nascoste non elaborano i messaggi. I thread STA in genere hanno un message pump in esecuzione in modo che questo problema non si manifesti nei thread STA. I thread MTA, tuttavia, non dispongono in genere di un message pump, quindi il problema si manifesterà in genere nei thread MTA.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [Tipi di eventi](../../../ado/guide/data/types-of-events.md)  
  
-   [Parametri evento](../../../ado/guide/data/event-parameters.md)  
  
-   [Interazione tra i gestori eventi](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [Creazione di istanze evento ADO per linguaggio](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Riepilogo del gestore eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creazione di un'istanza di evento ADO per lingua](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Parametri evento](../../../ado/guide/data/event-parameters.md)   
 [Tipi di eventi](../../../ado/guide/data/types-of-events.md)
