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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22e63bad49586bbbc1a5616114055779cd3ea041
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925541"
---
# <a name="determining-edit-mode"></a>Determinazione della modalità di modifica
ADO mantiene un buffer di modifica associato al record corrente. Il **EditMode** proprietà indica se sono state apportate modifiche a questo buffer oppure se è stato creato un nuovo record. Uso **EditMode** per determinare lo stato di modifica del record corrente. È possibile verificare le modifiche in sospeso se un processo di modifica è stata interrotta e determinare se è necessario usare il **Update** oppure **CancelUpdate** (metodo).  
  
 **Proprietà EditMode** restituisce uno dei **EditModeEnum** costanti, sono elencate nella tabella seguente.  
  
|Costante|Descrizione|  
|--------------|-----------------|  
|**adEditNone**|Indica che nessuna operazione di modifica è in corso.|  
|**adEditInProgress**|Indica che i dati presenti nel record corrente sono stati modificati ma non salvati.|  
|**adEditAdd**|Indica che il **AddNew** chiamata al metodo e il record corrente nel buffer di copia è un nuovo record che non è stato salvato nel database.|  
|**adEditDelete**|Indica che il record corrente è stato eliminato.|  
  
 **Proprietà EditMode** può restituire un valore valido solo se viene rilevato un record corrente. **Proprietà EditMode** restituirà un errore se **BOF** oppure **EOF** viene **True** o se il record corrente è stato eliminato.
