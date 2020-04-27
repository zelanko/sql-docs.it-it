---
title: Aggiungere progetti al controllo del codice sorgente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0936af9b97d08c6bcd5033e61d9fa1c9153272e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62791789"
---
# <a name="add-projects-to-source-control"></a>Aggiungere progetti al controllo del codice sorgente
  Nelle soluzioni di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] possono essere ospitati più progetti. L'inclusione o meno della soluzione alla quale appartiene un progetto nel controllo del codice sorgente determina il modo in cui il progetto stesso viene aggiunto al controllo. Se si archivia una soluzione inclusa nel controllo del codice sorgente, il progetto verrà aggiunto automaticamente al controllo. Per ulteriori informazioni sull'archiviazione di soluzioni, vedere [archiviare i file](../../2014/database-engine/check-in-files.md).  
  
 Se la soluzione alla quale appartiene il progetto non è inclusa nel controllo del codice sorgente, è possibile aggiungere tale soluzione al controllo in modo che tutti i progetti della soluzione vengano aggiunti automaticamente. Per ulteriori informazioni sull'aggiunta di soluzioni al controllo del codice sorgente, vedere [aggiungere soluzioni al controllo del codice sorgente](../../2014/database-engine/add-solutions-to-source-control.md).  
  
 Se non si desidera aggiungere la soluzione al controllo del codice sorgente, è possibile utilizzare il comando **Aggiungi selezione al controllo del codice sorgente** per aggiungere manualmente il progetto.  
  
 Gli oggetti di database non vengono protetti direttamente dal provider del controllo del codice sorgente. È tuttavia possibile creare script relativi agli oggetti di database e salvarli includendoli nel controllo del codice sorgente.  
  
### <a name="to-add-a-project-to-source-control"></a>Per aggiungere un progetto al controllo del codice sorgente  
  
1.  In Esplora soluzioni selezionare il progetto desiderato.  
  
2.  Scegliere **controllo del codice sorgente**dal menu **file** , quindi fare clic su **Aggiungi progetti selezionati al controllo del codice sorgente**.  
  
    > [!NOTE]  
    >  Se si utilizza il comando **Aggiungi progetti selezionati al controllo del codice sorgente** per aggiungere un progetto che appartiene a una soluzione controllata dal codice sorgente, viene richiesto se si desidera aggiungere il progetto come sottocartella della soluzione controllata dal codice sorgente o aggiungere il progetto come cartella separata.  
  
3.  Se richiesto, eseguire l'accesso al provider del controllo del codice sorgente.  
  
4.  Verrà visualizzata la finestra **di dialogo Aggiungi a progetto SourceSafe** . Il nome del progetto viene visualizzato nella casella **progetto** .  
  
5.  Nell'elenco **cartelle** aprire la cartella in cui si vuole inserire il progetto. In alternativa, è possibile fare clic su **Crea** per creare una cartella con il nome visualizzato nella casella **progetto** .  
  
## <a name="see-also"></a>Vedi anche  
 [Aggiungere soluzioni e progetti al controllo del codice sorgente](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
