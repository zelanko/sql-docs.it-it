---
title: Classe di evento CPU Threshold Exceeded | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- CPU Threshold Exceeded Event Class
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 569b085d28a0339927049fca0d758286dd1b6e8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62686101"
---
# <a name="cpu-threshold-exceeded-event-class"></a>Classe di evento CPU Threshold Exceeded
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Questa classe di evento indica il rilevamento di una query che supera il valore soglia della CPU specificato per REQUEST_MAX_CPU_TIME_SEC.  
  
> [!NOTE]  
>  L'intervallo di rilevamento per questo evento è cinque secondi. È garantita la generazione di un evento se una query supera il limite specificato di almeno cinque secondi. Tuttavia, se una query supera la soglia specificata di meno di cinque secondi, il rilevamento potrebbe non riuscire a seconda del momento della query e dell'ora dell'ultima operazione di rilevamento.  
  
## <a name="cpu-threshold-exceeded-data-columns"></a>Colonne di dati di CPU Threshold Exceeded  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|**int**|Utilizzo della CPU in millisecondi.|18|Sì|  
|EventClass|**int**|214|27|no|  
|EventSubClass|**int**|Violazione del limite della CPU.|21|Sì|  
|GroupID|**int**|ID del gruppo in cui si verifica la violazione.|66|Sì|  
|OwnerID|**int**|SPID del processo che provoca la violazione.|58|Sì|  
|SPID|**int**|ID del processo del server che genera l'evento.<br /><br /> Nota: può essere diverso dallo SPID effettivo dell'utente se il thread di sistema convalida l'utilizzo della CPU come attività di background.|12|Sì|  
|StartTime|**datetime**|Ora di generazione dell'evento.|14|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
