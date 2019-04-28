---
title: Classe di evento PreConnect:Completed | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Completed Event Class
ms.assetid: 7ed2f620-6511-4985-9961-d2927c2b1759
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eaad0a80fd77257c6e79e092733d75c0c8df5df5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827082"
---
# <a name="preconnectcompleted-event-class"></a>classe di evento PreConnect:Completed
  La classe di evento PreConnect:Completed indica la fine dell'esecuzione di un trigger LOGON o di una funzione di classificazione di Resource Governor.  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>Colonne di dati della classe di evento PreConnect:Completed  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|216|27|No|  
|SPID|`int`|ID del processo del server che genera l'evento.|12|Yes|  
|EventSubClass|`int`|1 per la funzione di classificazione definita dall'utente.|21|Yes|  
|StartTime|`datetime`|Ora di avvio della funzione di classificazione definita dall'utente.|14|Yes|  
|EndTime|`datetime`|Ora di avvio della funzione di classificazione definita dall'utente.|15|Yes|  
|Duration|`bigint`|Durata della funzione di classificazione in microsecondi.|13|Yes|  
|ObjectID|`int`|ID dell'oggetto di classificazione definito dall'utente.|22|Yes|  
|CPU|`int`|Utilizzo della CPU in millisecondi.|18|Yes|  
|Reads|`int`|Numero di letture logiche.|16|Yes|  
|Writes|`int`|Numero di scritture logiche.|17|Yes|  
|GroupID|`int`|ID del gruppo del carico di lavoro classificato.|66|Yes|  
|Errore|`int`|Ultimo numero di errore se non è possibile eseguire la funzione di classificazione definita dall'utente.|31|Yes|  
|State|`int`|Stato dell'ultimo errore.|30|Yes|  
|TargetUserName|`sysname`|Valore restituito (nome del gruppo del carico di lavoro) per la funzione di classificazione definita dall'utente se non è possibile trovare un gruppo attivo corrispondente. Negli altri casi la colonna è impostata su NULL.|39|Yes|  
|ObjectName|`nvarchar(256)`|Nome in due parti della funzione di classificazione definita dall'utente, ad esempio dbo.classifier.|34|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [Classe di evento PreConnect:Starting](preconnect-starting-event-class.md)   
 [Resource Governor](../resource-governor/resource-governor.md)  
  
  
