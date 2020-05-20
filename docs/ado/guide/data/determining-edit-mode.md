---
title: Determinazione della modalità di modifica | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: rothja
ms.author: jroth
ms.openlocfilehash: 6df3765b8dd9461349937fc14f6edebcaab3fbfb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761077"
---
# <a name="determining-edit-mode"></a>Determinazione della modalità di modifica
ADO gestisce un buffer di modifica associato al record corrente. La proprietà **EditMode** indica se sono state apportate modifiche a questo buffer o se è stato creato un nuovo record. Usare **EditMode** per determinare lo stato di modifica del record corrente. È possibile verificare la presenza di modifiche in sospeso se un processo di modifica è stato interrotto e determinare se è necessario utilizzare il metodo **Update** o **CancelUpdate** .  
  
 **EditMode** restituisce una delle costanti **EditModeEnum** , elencate nella tabella seguente.  
  
|Costante|Description|  
|--------------|-----------------|  
|**adEditNone**|Indica che non è in corso alcuna operazione di modifica.|  
|**adEditInProgress**|Indica che i dati nel record corrente sono stati modificati, ma non salvati.|  
|**adEditAdd**|Indica che il metodo **AddNew** è stato chiamato e che il record corrente nel buffer di copia è un nuovo record che non è stato salvato nel database.|  
|**adEditDelete**|Indica che il record corrente è stato eliminato.|  
  
 **EditMode** può restituire un valore valido solo se è presente un record corrente. **EditMode** restituirà un errore se **BOF** o **EOF** è **true** o se il record corrente è stato eliminato.
