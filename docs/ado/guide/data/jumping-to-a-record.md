---
description: Passaggio a un record
title: Passaggio a un record | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: rothja
ms.author: jroth
ms.openlocfilehash: 96987a5c51d7a888672609aa28f3fd223ccfffa1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980402"
---
# <a name="jumping-to-a-record"></a>Passaggio a un record
Il metodo [Move](../../reference/ado-api/move-method-ado.md) consente di spostarsi avanti o indietro nel **Recordset** per un numero specificato di record utilizzando la sintassi seguente:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo **Move** è supportato in tutti gli oggetti **Recordset** .  
  
 Se l'argomento *NumRecords* è maggiore di zero, la posizione corrente del record viene spostata in avanti (verso la fine del **Recordset**). Se *NumRecords* è minore di zero, la posizione corrente del record viene spostata indietro (verso l'inizio del **Recordset**).  
  
 Se la chiamata di **spostamento** sposta la posizione del record corrente in un punto prima del primo record, ADO imposta il record corrente sulla posizione prima del primo record nel **Recordset** (**BOF** è **true**). Un tentativo di spostarsi all'indietro quando la proprietà **BOF** è già **true** genera un errore.  
  
 Se la chiamata di **spostamento** sposta la posizione del record corrente in un punto successivo all'ultimo record, ADO imposta il record corrente sulla posizione dopo l'ultimo record nel **Recordset** (**EOF** è **true**). Un tentativo di andare avanti quando la proprietà **EOF** è già **true** genera un errore.  
  
 Se si chiama il metodo **Move** da un oggetto **Recordset** vuoto, viene generato un errore.  
  
 Se si passa un segnalibro nell'argomento *iniziale* , lo spostamento è relativo al record con questo segnalibro, supponendo che l'oggetto **Recordset** supporti i segnalibri. Un segnalibro viene ottenuto tramite la proprietà [Bookmark](../../reference/ado-api/bookmark-property-ado.md) . Se non specificato, lo spostamento è relativo al record corrente.  
  
 Se si usa la proprietà **CacheSize** per memorizzare nella cache locale i record del provider, il passaggio di un argomento *NumRecords* che sposta la posizione del record corrente all'esterno del gruppo corrente di record memorizzati nella cache impone a ADO di recuperare un nuovo gruppo di record, a partire dal record di destinazione. La proprietà **CacheSize** determina le dimensioni del gruppo appena recuperato e il record di destinazione è il primo record recuperato.