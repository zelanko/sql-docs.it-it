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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791789"
---
# <a name="add-projects-to-source-control"></a>Aggiungere progetti al controllo del codice sorgente
  Nelle soluzioni di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] possono essere ospitati più progetti. L'inclusione o meno della soluzione alla quale appartiene un progetto nel controllo del codice sorgente determina il modo in cui il progetto stesso viene aggiunto al controllo. Se si archivia una soluzione inclusa nel controllo del codice sorgente, il progetto verrà aggiunto automaticamente al controllo. Per altre informazioni sull'archiviazione di soluzioni, vedere [deposita](../../2014/database-engine/check-in-files.md).  
  
 Se la soluzione alla quale appartiene il progetto non è inclusa nel controllo del codice sorgente, è possibile aggiungere tale soluzione al controllo in modo che tutti i progetti della soluzione vengano aggiunti automaticamente. Per altre informazioni sull'aggiunta di soluzioni al controllo del codice sorgente, vedere [aggiungere soluzioni al controllo del codice sorgente](../../2014/database-engine/add-solutions-to-source-control.md).  
  
 Se non si desidera aggiungere la soluzione al controllo del codice sorgente, è possibile usare la **Aggiungi selezione al controllo del codice sorgente** comando per aggiungere manualmente il progetto.  
  
 Gli oggetti di database non vengono protetti direttamente dal provider del controllo del codice sorgente. È tuttavia possibile creare script relativi agli oggetti di database e salvarli includendoli nel controllo del codice sorgente.  
  
### <a name="to-add-a-project-to-source-control"></a>Per aggiungere un progetto al controllo del codice sorgente  
  
1.  In Esplora soluzioni selezionare il progetto desiderato.  
  
2.  Nel **File** dal menu **controllo del codice sorgente**, quindi fare clic su **Aggiungi progetti selezionati a controllo del codice sorgente**.  
  
    > [!NOTE]  
    >  Se si usa la **Aggiungi progetti selezionati a controllo del codice sorgente** comando per aggiungere un progetto a cui appartiene a una soluzione di controllo del codice sorgente, viene chiesto se si desidera aggiungere il progetto come una sottocartella della soluzione di controllo del codice sorgente o da aggiungere il progetto come una cartella separata.  
  
3.  Se richiesto, eseguire l'accesso al provider del controllo del codice sorgente.  
  
4.  Il **Aggiungi a progetto SourceSafe** verrà visualizzata la finestra di dialogo. Il nome del progetto visualizzato nei **progetto** casella.  
  
5.  Nel **cartelle** elenco, aprire la cartella in cui si desidera salvare il progetto. In alternativa, è possibile fare clic su **Create** per creare una cartella con il nome visualizzato nei **progetto** casella.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere soluzioni e progetti al controllo del codice sorgente](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
