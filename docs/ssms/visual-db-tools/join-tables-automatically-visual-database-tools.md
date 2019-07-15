---
title: Unire tabelle in modo automatico (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- joins [SQL Server], creating
- joins [SQL Server], automatic
ms.assetid: f152af82-bcb6-49ca-af19-48cdb7fc9ac6
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 43bcfa304979b918d9588c8bdd8bd07f9296fa5f
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67682158"
---
# <a name="join-tables-automatically-visual-database-tools"></a>Unione di tabelle in modo automatico (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Quando si aggiungono due o più tabelle a una query, in [Progettazione query e Progettazione viste](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) viene eseguito un tentativo per determinare se le tabelle sono correlate. In caso affermativo, linee di join verranno inserite automaticamente tra i rettangoli che rappresentano le tabelle o gli oggetti con struttura di tabella.  
  
In Progettazione query e Progettazione viste le tabelle saranno considerate in join se:  
  
-   Il database contiene informazioni che specificano che le tabelle sono correlate.  
  
-   Se due colonne, una per ogni tabella, hanno lo stesso nome e lo stesso tipo di dati. La colonna è una chiave primaria in almeno una delle tabelle. Se, in caso di aggiunta delle tabelle `employee` e `jobs` , la colonna `job_id` è la chiave primaria nella tabella `jobs` ed entrambe le tabelle contengono una colonna denominata `job_id` con lo stesso tipo di dati, le due tabelle verranno unite automaticamente in join in Progettazione query.  
  
    > [!NOTE]  
    > In Progettazione query e Progettazione viste verrà creato un solo join basato sulle colonne con lo stesso nome e lo stesso tipo di dati. Se sono possibili più join, Progettazione query prevederà un arresto in seguito alla creazione di un join basato sul primo set di colonne corrispondenti incontrate.  
  
-   Si rileverà che una condizione di ricerca (una clausola WHERE) in effetti è una condizione di join. Sarà ad esempio possibile aggiungere le tabelle `employee` e `jobs`e creare una condizione di ricerca per lo stesso valore nella colonna `job_id` di entrambe le tabelle. A questo punto, in Progettazione query si rileverà che il risultato della condizione di ricerca è un join e si creerà una condizione di join basata sulla condizione di ricerca.  
  
Se in Progettazione query e Progettazione viste è stato creato un join non pertinente alla query, sarà possibile modificare il join o rimuoverlo. For informazioni dettagliate, vedere [Modifica di operatori di join &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md) e [Rimozione di join &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-joins-visual-database-tools.md).  
  
Se le tabelle non vengono unite in join automaticamente nella query, sarà possibile creare manualmente il join. Per informazioni dettagliate, vedere [Unione di tabelle in modo manuale &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
[Rappresentazione di join in Progettazione query e Progettazione viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/how-the-query-and-view-designer-represents-joins-visual-database-tools.md)  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Eseguire query con join &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
