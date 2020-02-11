---
title: Modifica file archiviati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying checked-in files
- checking in files
ms.assetid: 560cd19f-ab22-4273-b00c-149993a630e6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97d6ab997a1ece36919a49243e0f1dc3cc6f3593
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779605"
---
# <a name="edit-checked-in-files"></a>Modificare i file archiviati
  Prima di poter modificare i file inclusi nel controllo del codice sorgente in genere è necessario estrarli. Tuttavia, è possibile configurare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] in modo che sia possibile modificare i file non estratti. Quando si esegue questa operazione, le modifiche vengono mantenute in memoria fino a quando non si salvano i file. In seguito verrà chiesto di estrarre il file dal controllo del codice di origine.  
  
 Se si lavora in un team, non è consigliabile consentire modifiche dei file archiviati a meno che il provider del controllo del codice sorgente non supporti estrazioni sia della versione locale sia della versione del server. La maggior parte dei provider non supporta estrazioni della versione locale. In questo caso e se un file archiviato viene modificato, sarà necessario unire manualmente la versione in memoria e la versione del server prima di poter archiviare il file. In questo scenario, le unioni automatiche e assistite dal provider non sono supportate.  
  
### <a name="to-edit-checked-in-files"></a>Per modificare i file archiviati  
  
1.  Scegliere **Opzioni** dal menu **Strumenti**.  
  
2.  Nella finestra di dialogo **Opzioni** espandere la cartella **source**contro l, quindi fare clic su **ambiente**.  
  
3.  Fare clic su **Consenti modifica elementi archiviati**, quindi fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestisci archiviazioni](../../2014/database-engine/manage-checkins.md)   
 [Gestione delle estrazioni](../../2014/database-engine/manage-checkouts.md)  
  
  
