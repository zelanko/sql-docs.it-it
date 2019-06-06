---
title: Passaggio a un Record | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cefa6ac39d68040106d38e5f1cfbec8a6eff8358
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700699"
---
# <a name="jumping-to-a-record"></a>Passaggio a un record
Il [spostare](../../../ado/reference/ado-api/move-method-ado.md) metodo consente di spostarsi avanti o indietro nel **Recordset** un numero specificato di record usando la sintassi seguente:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>Note  
 Il **spostare** metodo è supportato su tutti **Recordset** oggetti.  
  
 Se il *NumRecords* argomento è maggiore di zero, la posizione corrente si sposta in avanti (verso la fine del **Recordset**). Se *NumRecords* è minore di zero, la posizione corrente si sposta all'indietro (verso l'inizio della **Recordset**).  
  
 Se il **spostare** chiamata Sposta la posizione del record corrente in un punto prima del primo record, ADO imposta il record corrente alla posizione prima del primo record la **Recordset** (**BOF** viene **True**). Tenta di spostarsi con le versioni precedenti quando le **BOF** proprietà è già **True** genera un errore.  
  
 Se il **spostare** chiamata Sposta la posizione corrente in un punto dopo l'ultimo record, ADO imposta il record corrente alla posizione successiva all'ultimo record nelle **Recordset** (**EOF** viene **True**). Tenta di spostarsi in avanti quando le **EOF** proprietà è già **True** genera un errore.  
  
 Chiama il **spostare** metodo da un oggetto vuoto **Recordset** oggetto genera un errore.  
  
 Se si passa un segnalibro nel *avviare* argomento, lo spostamento è relativo al record con il segnalibro, presupponendo che le **Recordset** oggetto supporta i segnalibri. Un segnalibro ottenuto utilizzando il [segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md) proprietà. Se non specificato, lo spostamento è relativo al record corrente.  
  
 Se si usa la **CacheSize** proprietà da memorizzare localmente i record dal provider, passando un *NumRecords* argomento che sposta la posizione corrente all'esterno del gruppo corrente di record memorizzati nella cache forza ADO per recuperare un nuovo gruppo di record, a partire dal record di destinazione. Il **CacheSize** proprietà determina la dimensione del gruppo appena recuperato e il record di destinazione è il primo record recuperati.
