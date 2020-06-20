---
title: Specificare una versione come ultima versione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], latest version
- latest file version specified
- file versions [SQL Server]
ms.assetid: 407dffb1-3ecf-461e-835d-124781f26ee7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d598ec6f828fc7d8d59b3f998b775a752b94c4a6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928870"
---
# <a name="specify-a-version-as-the-latest-version"></a>Specifica di una versione come ultima versione
  Quando un file viene archiviato nel controllo del codice sorgente, l'ultima versione diventa quella archiviata. Gli utenti che la estraggono o la recuperano ricevono copie locali dell'elemento archiviato più di recente.  
  
 In alcune situazioni, tuttavia, potrebbe essere necessario designare come ultima una versione precedente di un elemento. Ad esempio, si estrae, si modifica e quindi si archivia il file. In un secondo momento si decide di rimuovere le modifiche. Dal momento che il file è stato archiviato, non è possibile annullare l'estrazione originale. In questo caso è possibile impostare la versione estratta originariamente come ultima versione dell'elemento.  
  
 Per impostare l'ultima versione:  
  
-   **Aggiunta di una versione**. Quando si blocca una versione del file, le versioni più recenti di quella bloccata non vengono eliminate. È inoltre possibile sbloccare un file bloccato in precedenza. In questo caso, l'ultima versione del file sarà quella archiviata più di recente. Non è tuttavia possibile estrarre un file bloccato.  
  
-   **Rollback a una versione specificata**. Quando viene eseguito il ripristino di una versione, tutte le versioni più recenti di quella ripristinata verranno eliminate dal controllo del codice sorgente. È possibile quindi estrarre l'ultima versione rimanente.  
  
### <a name="to-pin-a-version"></a>Per bloccare una versione  
  
1.  In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] aprire la soluzione.  
  
2.  In Esplora soluzioni selezionare il file che si desidera specificare come ultima versione.  
  
3.  Scegliere **controllo del codice sorgente** dal menu **file** e fare clic su **ViewHistory**.  
  
4.  Nella finestra **di dialogo cronologia di** \<file> selezionare la versione che si desidera specificare come ultima e quindi fare clic su **Aggiungi**.  
  
     Accanto alla versione selezionata viene visualizzato un simbolo di blocco per indicare che si tratta della versione corrente del file. Se in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] è caricata una versione diversa, viene chiesto di ricaricare il file.  
  
### <a name="to-roll-back-to-a-version"></a>Per ripristinare una versione  
  
1.  In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] aprire la soluzione.  
  
2.  In Esplora soluzioni selezionare l'elemento che si desidera specificare come ultima versione.  
  
3.  Scegliere **controllo del codice sorgente** dal menu **file** e fare clic su **cronologia**.  
  
4.  Nella finestra di dialogo **Opzioni cronologia** fare clic su **OK** per visualizzare la finestra **di dialogo Cronologia file** .  
  
5.  Nella casella **cronologia del file** selezionare la versione che si desidera specificare come ultima versione, quindi fare clic su **rollback**.  
  
     Verrà visualizzato un messaggio che informa che tutte le versioni successive a quella selezionata verranno eliminate.  
  
6.  Fare clic su **Sì** per eseguire il rollback alla versione selezionata.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestisci archiviazioni](../../2014/database-engine/manage-checkins.md)   
 [Archiviazione di file](../../2014/database-engine/check-in-files.md)  
  
  
