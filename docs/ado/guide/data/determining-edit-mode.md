---
description: Determinazione della modalità di modifica
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
ms.openlocfilehash: 788a91fc3de259210a5f2756f148161fbb90308e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453503"
---
# <a name="determining-edit-mode"></a>Determinazione della modalità di modifica
ADO gestisce un buffer di modifica associato al record corrente. La proprietà **EditMode** indica se sono state apportate modifiche a questo buffer o se è stato creato un nuovo record. Usare **EditMode** per determinare lo stato di modifica del record corrente. È possibile verificare la presenza di modifiche in sospeso se un processo di modifica è stato interrotto e determinare se è necessario utilizzare il metodo **Update** o **CancelUpdate** .  
  
 **EditMode** restituisce una delle costanti **EditModeEnum** , elencate nella tabella seguente.  
  
|Costante|Descrizione|  
|--------------|-----------------|  
|**adEditNone**|Indica che non è in corso alcuna operazione di modifica.|  
|**adEditInProgress**|Indica che i dati nel record corrente sono stati modificati, ma non salvati.|  
|**adEditAdd**|Indica che il metodo **AddNew** è stato chiamato e che il record corrente nel buffer di copia è un nuovo record che non è stato salvato nel database.|  
|**adEditDelete**|Indica che il record corrente è stato eliminato.|  
  
 **EditMode** può restituire un valore valido solo se è presente un record corrente. **EditMode** restituirà un errore se **BOF** o **EOF** è **true** o se il record corrente è stato eliminato.
