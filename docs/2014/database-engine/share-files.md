---
title: Condividi file | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- sharing files
- file sharing [SQL Server]
- version control services [SQL Server], file sharing
ms.assetid: 645f5c0a-e949-4e87-8988-85e4d6128464
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e779a0c0da9920b2efda5f52135e85f31959d10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62843557"
---
# <a name="share-files"></a>Condivisione di file
  È possibile utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per condividere elementi nei progetti di controllo del codice sorgente. Quando un elemento viene condiviso, qualsiasi modifica all'elemento apportata verrà applicata in tutti i progetti con i quali l'elemento è condiviso.  
  
 La condivisione degli elementi offre i vantaggi seguenti agli utenti del controllo del codice sorgente:  
  
-   Evita di dover archiviare una copia separata dell'elemento in ogni progetto che utilizza l'elemento condiviso, risparmiando spazio su disco sia nel client che nel server del controllo del codice sorgente. Il provider del controllo del codice sorgente archivia l'elemento condiviso in un percorso centrale e in ogni progetto con cui è condiviso viene archiviato un puntatore per quel percorso.  
  
-   Evita incompatibilità tra le versioni. Poiché ogni progetto con cui l'elemento è condiviso utilizza la stessa versione dell'elemento, vengono evitati i conflitti che insorgono quando ogni copia di un elemento cambia in maniera indipendente all'interno di più progetti.  
  
### <a name="to-share-an-item"></a>Per condividere un elemento  
  
1.  In Esplora soluzioni selezionare la cartella o il progetto in cui si desidera posizionare i file condivisi.  
  
2.  Scegliere **controllo del codice sorgente**dal menu **file** , quindi fare clic su **Condividi**.  
  
3.  Nella finestra di dialogo **Condividi con** individuare l'elemento che si desidera condividere nell'elenco di directory, quindi fare clic su tale elemento.  
  
4.  Fare clic su **Condividi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali sul controllo del codice sorgente](../../2014/database-engine/source-control-basics.md)  
  
  
