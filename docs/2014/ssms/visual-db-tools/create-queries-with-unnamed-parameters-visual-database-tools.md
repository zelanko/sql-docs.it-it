---
title: Creare query con parametri senza nome (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9eebede28d257083b55ffd4b14943b7ebc1a95b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184340"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>Creazione di query con parametri senza nome (Visual Database Tools)
  Per creare una query con un parametro senza nome, è possibile inserire un punto interrogativo (?) come segnaposto per un valore letterale. In Progettazione query e Progettazione viste gli verrà assegnato automaticamente un nome temporaneo. Nella query è possibile specificare qualsiasi numero di parametri senza nome.  
  
 Al momento dell'esecuzione della query in Progettazione query e Progettazione viste, nella finestra di dialogo Parametri query viene visualizzato il nome temporaneo.  
  
### <a name="to-specify-an-unnamed-parameter"></a>Per specificare un parametro senza nome  
  
1.  Aggiungere al [riquadro Criteri](visual-database-tools.md)le colonne o le espressioni da includere nella ricerca. Per evitare che le colonne o le espressioni compaiano nell'output della query, rimuoverle dalle colonne di output.  
  
2.  Individuare la riga che contiene la colonna di dati o l'espressione da includere nella ricerca e aggiungere un punto interrogativo (?) nella colonna **Filtro** della griglia.  
  
     Per impostazione predefinita viene aggiunto l'operatore "=". In ogni caso, è possibile modificare la cella inserendo ">", "<" o qualsiasi altro operatore di confronto SQL.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query mediante parametri &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)  
  
  
