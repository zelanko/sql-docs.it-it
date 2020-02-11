---
title: Unire tabelle in modo automatico (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- joins [SQL Server], creating
- joins [SQL Server], automatic
ms.assetid: f152af82-bcb6-49ca-af19-48cdb7fc9ac6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bab311878966087ef9b6c3f05bb3023d02fdeb20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62711068"
---
# <a name="join-tables-automatically-visual-database-tools"></a>Unione di tabelle in modo automatico (Visual Database Tools)
  Quando si aggiungono due o più tabelle a una query, in [Progettazione query e Progettazione viste](visual-database-tools.md) viene eseguito un tentativo per determinare se le tabelle sono correlate. In caso affermativo, linee di join verranno inserite automaticamente tra i rettangoli che rappresentano le tabelle o gli oggetti con struttura di tabella.  
  
 In Progettazione query e Progettazione viste le tabelle saranno considerate in join se:  
  
-   Il database contiene informazioni che specificano che le tabelle sono correlate.  
  
-   Se due colonne, una per ogni tabella, hanno lo stesso nome e lo stesso tipo di dati. La colonna è una chiave primaria in almeno una delle tabelle. Se, in caso di aggiunta delle tabelle `employee` e `jobs` , la colonna `job_id` è la chiave primaria nella tabella `jobs` ed entrambe le tabelle contengono una colonna denominata `job_id` con lo stesso tipo di dati, le due tabelle verranno unite automaticamente in join in Progettazione query.  
  
    > [!NOTE]  
    >  In Progettazione query e Progettazione viste verrà creato un solo join basato sulle colonne con lo stesso nome e lo stesso tipo di dati. Se sono possibili più join, Progettazione query prevederà un arresto in seguito alla creazione di un join basato sul primo set di colonne corrispondenti incontrate.  
  
-   Si rileverà che una condizione di ricerca (una clausola WHERE) in effetti è una condizione di join. Sarà ad esempio possibile aggiungere le tabelle `employee` e `jobs`e creare una condizione di ricerca per lo stesso valore nella colonna `job_id` di entrambe le tabelle. A questo punto, in Progettazione query si rileverà che il risultato della condizione di ricerca è un join e si creerà una condizione di join basata sulla condizione di ricerca.  
  
 Se in Progettazione query e Progettazione viste è stato creato un join non pertinente alla query, sarà possibile modificare il join o rimuoverlo. For informazioni dettagliate, vedere [Modifica di operatori di join &#40;Visual Database Tools&#41;](modify-join-operators-visual-database-tools.md) e [Rimozione di join &#40;Visual Database Tools&#41;](remove-joins-visual-database-tools.md).  
  
 Se le tabelle non vengono unite in join automaticamente nella query, sarà possibile creare manualmente il join. Per informazioni dettagliate, vedere [Unione di tabelle in modo manuale &#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Rappresentazione di join in Progettazione query e Progettazione viste &#40;Visual Database Tools&#41;](how-the-query-and-view-designer-represents-joins-visual-database-tools.md)   
 [Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Eseguire query con join &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
