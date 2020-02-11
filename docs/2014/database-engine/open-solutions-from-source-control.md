---
title: Aprire soluzioni dal controllo del codice sorgente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- opening solutions
- solutions [SQL Server Management Studio], opening
ms.assetid: a96a1f0d-0183-4587-a3b0-4598309cbdd2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f8405c9fcb04559b6f25d2244bc36dde760a182
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62844765"
---
# <a name="open-solutions-from-source-control"></a>Aprire Soluzioni dal controllo del codice sorgente
  Per aprire soluzioni direttamente dal controllo del codice sorgente, è possibile utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Quando si esegue questa operazione, viene creata automaticamente una copia della versione più recente dei file della soluzione nel percorso specificato.  
  
 Se sul disco locale non è presente una copia locale della soluzione, prima di utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per estrarre la soluzione o recuperare i file della soluzione sarà necessario aprire il progetto dal controllo del codice sorgente.  
  
> [!NOTE]  
>  Se è già disponibile una copia locale della soluzione che si desidera aprire dal controllo del codice sorgente, verrà chiesto di sovrascrivere la copia locale.  
  
### <a name="to-open-a-solution-from-source-control"></a>Per aprire una soluzione dal controllo del codice sorgente  
  
1.  Scegliere **controllo del codice sorgente**dal menu **file** e fare clic su **Apri dal controllo del codice sorgente**.  
  
2.  Se richiesto, accedere a [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe.  
  
3.  Nella finestra di dialogo **Crea progetto locale da SourceSafe** selezionare la cartella che contiene la soluzione che si desidera aprire e fare clic su **OK**.  
  
4.  Se una cartella di lavoro per la soluzione esiste già nell'unità disco locale, la casella **Crea un nuovo progetto nella cartella** cambia per identificare la directory locale. Se non esiste una cartella di lavoro per la soluzione, è possibile digitare o cercare la directory locale nella quale dovrebbe essere aperta la soluzione.  
  
5.  Nella finestra di dialogo **Apri soluzione** selezionare il file della soluzione e fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Apertura di progetti dal controllo del codice sorgente](../../2014/database-engine/open-projects-from-source-control.md)  
  
  
