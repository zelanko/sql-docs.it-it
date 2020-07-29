---
title: Spostare elementi in una soluzione
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 67456bfd826610aaf500735d4f055e00f0c58aa7
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000802"
---
# <a name="move-items-in-a-solution"></a>Spostare elementi in una soluzione
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Gli elementi nei progetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono query, connessioni e file esterni. In Esplora soluzioni è possibile spostare query e file esterni tra progetti, mentre le connessioni non possono essere spostate.  
  
### <a name="to-move-items-in-solution-explorer"></a>Per spostare elementi in Esplora soluzioni  
  
1.  In Esplora soluzioni selezionare l'elemento che si desidera spostare.  
  
2.  Scegliere **Taglia** dal menu **Modifica**.  
  
3.  Sempre in Esplora soluzioni selezionare la destinazione.  
  
4.  Scegliere **Incolla** dal menu **Modifica**.  
  
È possibile spostare elementi trascinando query e file esterni in Esplora soluzioni e visualizzare il risultato dell'operazione di trascinamento. Se si spostano query da un tipo di progetto a un altro, è possibile che tali query vengano considerate file esterni nel progetto di destinazione.  
  
> [!NOTE]  
> Quando si sposta una query connessa, la connessione al progetto di destinazione non viene spostata, quindi la query perderà la connessione dopo essere stata spostata nel progetto di destinazione.  
  
## <a name="see-also"></a>Vedere anche  
[Esplora soluzioni](../../ssms/solution/solution-explorer.md)  
[Copiare elementi in una soluzione](../../ssms/solution/copy-items-in-a-solution.md)  
  
