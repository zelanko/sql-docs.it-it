---
title: Rimuovere o eliminare un elemento o un progetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dd6d04b186c68b128ad35ec5e5bd8b92ad1541c0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63035685"
---
# <a name="remove-or-delete-an-item-or-project"></a>Rimozione o eliminazione di un elemento o di un progetto
  Gli elementi nei progetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono query, connessioni e file esterni. È possibile rimuovere dalla soluzione query di progetto e file esterni senza cancellare i file dall'archivio. Rimuovere un progetto o un elemento quando non è utile nella soluzione corrente, ma si desidera includerlo in un'altra soluzione.  
  
### <a name="to-remove-a-project-item"></a>Per rimuovere un elemento di progetto  
  
1.  In Esplora soluzioni selezionare l'elemento del progetto che si desidera rimuovere.  
  
2.  Scegliere **Rimuovi** dal menu **Modifica**.  
  
3.  Nella finestra di conferma fare clic su **Rimuovi** per rimuovere l'elemento dal progetto.  
  
 Un elemento rimosso rimane comunque nel file system. È pertanto possibile aggiungerlo alla soluzione originale o a un'altra soluzione.  
  
#### <a name="to-remove-a-project"></a>Per rimuovere un progetto  
  
1.  In Esplora soluzioni selezionare il progetto che si desidera rimuovere.  
  
2.  Scegliere **Rimuovi** dal menu **Modifica**.  
  
3.  Nella finestra di conferma fare clic su **OK**per rimuovere il progetto dalla soluzione.  
  
 È possibile eliminare un progetto in modo definitivo. In questo caso è necessario prima rimuovere dalle soluzioni di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tutti i riferimenti al progetto e quindi utilizzare Esplora risorse di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows per eliminare definitivamente i file associati dall'archivio.  
  
#### <a name="to-delete-a-project"></a>Per eliminare un progetto  
  
1.  In Esplora soluzioni rimuovere dalla soluzione il progetto che si desidera eliminare.  
  
2.  In Esplora risorse individuare e selezionare i file associati al progetto o all'elemento da eliminare.  
  
3.  Scegliere **Elimina** dal menu **File**.  
  
## <a name="see-also"></a>Vedere anche  
 [Esplora soluzioni](solution-explorer.md)   
 [Aggiungere nuovi elementi a un progetto](add-new-items-to-a-project.md)   
 [Aggiungere elementi esistenti a un progetto](add-existing-items-to-a-project.md)  
  
  
