---
title: Spostare elementi in una soluzione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0c6711b736f0313508f74b6c30253e7b2e2a3f93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63154700"
---
# <a name="move-items-in-a-solution"></a>Spostare elementi in una soluzione
  Gli elementi nei progetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono query, connessioni e file esterni. In Esplora soluzioni è possibile spostare query e file esterni tra progetti, mentre le connessioni non possono essere spostate.  
  
### <a name="to-move-items-in-solution-explorer"></a>Per spostare elementi in Esplora soluzioni  
  
1.  In Esplora soluzioni selezionare l'elemento che si desidera spostare.  
  
2.  Scegliere **Taglia** dal menu **Modifica**.  
  
3.  Sempre in Esplora soluzioni selezionare la destinazione.  
  
4.  Scegliere **Incolla** dal menu **Modifica**.  
  
 È possibile spostare elementi trascinando query e file esterni in Esplora soluzioni e visualizzare il risultato dell'operazione di trascinamento. Se si spostano query da un tipo di progetto a un altro, è possibile che tali query vengano considerate file esterni nel progetto di destinazione.  
  
> [!NOTE]  
>  Quando si sposta una query connessa, la connessione al progetto di destinazione non viene spostata, quindi la query perderà la connessione dopo essere stata spostata nel progetto di destinazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Esplora soluzioni](solution-explorer.md)   
 [Copiare elementi in una soluzione](copy-items-in-a-solution.md)  
  
  
