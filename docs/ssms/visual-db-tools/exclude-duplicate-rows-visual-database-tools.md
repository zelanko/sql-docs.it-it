---
title: Escludere le righe duplicate
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2f652c40278a44d4bbe068a441e08ffe610af002
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012162"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>Escludere le righe duplicate (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Per visualizzare solo valori univoci in un set di risultati, è possibile impostare l'esclusione dei duplicati dai risultati.  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>Per escludere le righe duplicate dal set di risultati  
  
1.  Fare clic con il pulsante destro del mouse sullo sfondo del riquadro diagramma e scegliere **Proprietà** dal menu di scelta rapida.  
  
2.  Nella finestra Proprietà fare clic su **Valori Distinct** e impostare il valore su **Sì**.  
  
    In Progettazione query e Progettazione viste la parola chiave DISTINCT verrà inserita davanti all'elenco di colonne visualizzate nell'istruzione SQL.  
  
    > [!NOTE]  
    > Se si utilizza la parola chiave DISTINCT, potrebbe non essere possibile modificare il set di risultati nel riquadro Risultati.  
  
## <a name="see-also"></a>Vedere anche  
[Specifica dei criteri di ricerca &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
