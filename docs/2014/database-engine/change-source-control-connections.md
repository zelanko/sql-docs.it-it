---
title: Modificare le connessioni del controllo del codice sorgente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server Management Studio], source controls
- source controls [SQL Server Management Studio], connections
ms.assetid: 538e3beb-f99c-4095-bd65-6413e872d26e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 077a09cdca0c0aff777184f04467ca39592690aa
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936073"
---
# <a name="change-source-control-connections"></a>Modifica delle connessioni del controllo del codice sorgente
  La prima volta che viene aggiunta o aperta una soluzione dal controllo del codice sorgente, il provider del controllo crea un'associazione tra la cartella radice della directory della soluzione locale e la cartella corrispondente del server.  
  
 La cartella radice, chiamata anche radice unificata, risiede nel client. Sotto di essa si trovano tutti i file a cui fa riferimento una soluzione o un progetto. Per trovare l'ultima versione di una soluzione, la cronologia e le informazioni sullo stato, individuare la cartella che si trova nel server del controllo del codice sorgente. In [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, le cartelle del server sono denominate progetti.  
  
 In molti casi è necessario disassociare o disconnettere una soluzione dalla sua cartella del server. Se, ad esempio, il computer in cui si trova il provider del controllo del codice sorgente non è disponibile, è possibile connettersi a un computer di backup, riassociare la soluzione a una cartella del server sottoposta a backup e riprendere a lavorare normalmente. Se un progetto di controllo del codice sorgente è inoltre duplicato, potrebbe essere necessario associare la soluzione alla cartella del server in cui si trova la nuova versione del progetto.  
  
 Utilizzare l'interfaccia utente del provider del controllo del codice sorgente per cambiare la cartella del server alla quale è associata una soluzione. È possibile aprire l'interfaccia utente del controllo del codice sorgente dall'ambiente [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-open-the-source-control-user-interface-from-the-studio-environment"></a>Per aprire l'interfaccia utente del controllo del codice sorgente dall'ambiente Studio  
  
1.  Scegliere **controllo del codice sorgente**dal menu **file** e quindi fare clic su **avvia Microsoft Visual SourceSafe**.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali sul controllo del codice sorgente](../../2014/database-engine/source-control-basics.md)   
 [Impostare le opzioni di controllo del codice sorgente](../../2014/database-engine/set-source-control-options.md)   
 [Esclusione di file dal controllo del codice sorgente](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
