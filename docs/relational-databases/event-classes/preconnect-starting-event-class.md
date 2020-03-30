---
title: Classe di evento PreConnect:Starting | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8e309d3783dab58e42f0be76badfa293d7ce872f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67940683"
---
# <a name="preconnectstarting-event-class"></a>Classe di evento PreConnect:Starting
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La classe di evento PreConnect:Starting indica l'avvio dell'esecuzione di un trigger LOGON o di una funzione di classificazione di Resource Governor.  
  
## <a name="preconnectstarting-event-class-data-columns"></a>Colonne di dati della classe di evento PreConnect:Starting  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|No|  
|SPID|**int**|ID del processo del server che genera l'evento.|12|Sì|  
|EventSubClass|**int**|1 per la funzione di classificazione definita dall'utente.|21|Sì|  
|StartTime|**datetime**|Ora di avvio della funzione di classificazione definita dall'utente.|14|Sì|  
|ObjectID|**int**|ID dell'oggetto di classificazione definito dall'utente.|22|Sì|  
|ObjectName|**nvarchar(256)**|Nome in due parti della funzione di classificazione definita dall'utente, ad esempio dbo.classifier.|34|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)   
 [classe di evento PreConnect:Completed](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
