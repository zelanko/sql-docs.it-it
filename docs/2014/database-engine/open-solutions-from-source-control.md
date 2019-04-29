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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844765"
---
# <a name="open-solutions-from-source-control"></a>Aprire Soluzioni dal controllo del codice sorgente
  Per aprire soluzioni direttamente dal controllo del codice sorgente, è possibile utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Quando si esegue questa operazione, viene creata automaticamente una copia della versione più recente dei file della soluzione nel percorso specificato.  
  
 Se sul disco locale non è presente una copia locale della soluzione, prima di utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per estrarre la soluzione o recuperare i file della soluzione sarà necessario aprire il progetto dal controllo del codice sorgente.  
  
> [!NOTE]  
>  Se è già disponibile una copia locale della soluzione che si desidera aprire dal controllo del codice sorgente, verrà chiesto di sovrascrivere la copia locale.  
  
### <a name="to-open-a-solution-from-source-control"></a>Per aprire una soluzione dal controllo del codice sorgente  
  
1.  Nel **File** dal menu **controllo del codice sorgente**, fare clic su **Apri dal controllo del codice sorgente**.  
  
2.  Se richiesto, accedere a [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe.  
  
3.  Nel **Crea progetto locale da SourceSafe** finestra di dialogo, selezionare la cartella che contiene la soluzione che si desidera aprire e fare clic su **OK**.  
  
4.  Se esiste già una cartella di lavoro per la soluzione nell'unità disco locale, il **creare un nuovo progetto nella cartella** casella Cambia per identificare la directory locale. Se non esiste una cartella di lavoro per la soluzione, è possibile digitare o cercare la directory locale nella quale dovrebbe essere aperta la soluzione.  
  
5.  Nel **soluzione aperta** finestra di dialogo, selezionare il file della soluzione e fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Apertura di progetti dal controllo del codice sorgente](../../2014/database-engine/open-projects-from-source-control.md)  
  
  
