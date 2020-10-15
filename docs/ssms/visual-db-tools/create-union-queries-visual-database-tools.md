---
description: Creare query UNION (Visual Database Tools)
title: Creare query UNION
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b6d4d7618b3130e2b06d3efb8e9e2a35bc7ca0ee
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038374"
---
# <a name="create-union-queries-visual-database-tools"></a>Creare query UNION (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
La parola chiave UNION consente di includere i risultati di due istruzioni SELECT in una tabella risultante. Tutte le righe restituite dalle due istruzioni SELECT vengono combinate nel risultato dell'espressione UNION. Per gli esempi, vedere [Esempi di istruzioni SELECT (Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md).  
  
> [!NOTE]  
> Poiché nel riquadro Diagramma è possibile visualizzare solo una clausola SELECT, quando si lavora a una query di unione (query UNION), il Riquadro operazioni tabella verrà nascosto in Progettazione query.  
  
### <a name="to-create-a-merged-select-query"></a>Per creare una query SELECT unita  
  
1.  Aprire una query esistente o crearne una nuova.  
  
2.  Nel riquadro SQL digitare un'espressione UNION valida.  
  
    Nell'esempio seguente viene illustrata un'espressione UNION valida.  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  Per eseguire la query, scegliere **Esegui SQL** dal menu **Progettazione query** .  
  
    La query di unione verrà così formattata da Progettazione query.  
  
## <a name="see-also"></a>Vedere anche  
[Tipi di query supportati](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Procedure per la progettazione di query e viste](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Eseguire operazioni di base con le query](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION (Transact-SQL)](../../t-sql/language-elements/set-operators-union-transact-sql.md)