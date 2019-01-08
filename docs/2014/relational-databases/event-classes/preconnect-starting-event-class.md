---
title: Classe di evento PreConnect:Starting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0986e654430a47cc494bf1646c222b4888fc105b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52803713"
---
# <a name="preconnectstarting-event-class"></a>Classe di evento PreConnect:Starting
  La classe di evento PreConnect:Starting indica l'avvio dell'esecuzione di un trigger LOGON o di una funzione di classificazione di Resource Governor.  
  
## <a name="preconnectstarting-event-class-data-columns"></a>Colonne di dati della classe di evento PreConnect:Starting  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|215|27|No|  
|SPID|`int`|ID del processo del server che genera l'evento.|12|Yes|  
|EventSubClass|`int`|1 per la funzione di classificazione definita dall'utente.|21|Yes|  
|StartTime|`datetime`|Ora di avvio della funzione di classificazione definita dall'utente.|14|Yes|  
|ObjectID|`int`|ID dell'oggetto di classificazione definito dall'utente.|22|Yes|  
|ObjectName|`nvarchar(256)`|Nome in due parti della funzione di classificazione definita dall'utente, ad esempio dbo.classifier.|34|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../extended-events/extended-events.md)   
 [classe di evento PreConnect:Completed](preconnect-completed-event-class.md)   
 [Resource Governor](../resource-governor/resource-governor.md)  
  
  
