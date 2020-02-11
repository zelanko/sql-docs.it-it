---
title: dbo. sysdownloadlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdownloadlist
- sysdownloadlist_TSQL
- dbo.sysdownloadlist_TSQL
- sysdownloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sysdownloadlist system table
ms.assetid: 71087a4c-e829-488e-aa7d-a9476e2b4779
author: stevestein
ms.author: sstein
ms.openlocfilehash: 03e888cc3d36b909035247d5f1c16dd1ab61e0d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061192"
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Include la coda delle istruzioni di download per tutti i server di destinazione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Colonna Identity che indica la sequenza di inserimento naturale delle righe.|  
|**source_server**|**sysname**|Nome del server di origine.|  
|**operation_code**|**tinyint**|Codice operativo per il processo:<br /><br /> **1** = ins (inserimento)<br /><br /> **2** = UPD (aggiornamento)<br /><br /> **3** = CANC (Delete)<br /><br /> **4** = avvio<br /><br /> **5** = arresta|  
|**object_type**|**tinyint**|Codice del tipo di oggetto.|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|Numero di identificazione dell'oggetto.|  
|**target_server**|**sysname**|Nome del server di destinazione.|  
|**error_message**|**nvarchar(1024)**|Messaggio di errore restituito se nel server di destinazione viene rilevato un errore durante l'elaborazione di una determinata riga|  
|**date_posted**|**datetime**|Giorno e ora in cui il processo è stato inviato al server di destinazione.|  
|**date_downloaded**|**datetime**|Giorno e ora in cui è stato eseguito l'ultimo download del processo.|  
|**stato**|**tinyint**|Stato del processo:<br /><br /> **0** = non ancora scaricato<br /><br /> **1** = scaricato correttamente|  
|**deleted_object_name**|**sysname**|Nome dell'oggetto eliminato.|  
  
 <sup>1</sup> la colonna **object_id** può essere un valore pari a **-1**, che corrisponde al valore all se la colonna **operation_code** è un valore Delete.  
  
  
