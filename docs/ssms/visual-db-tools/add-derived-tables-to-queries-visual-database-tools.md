---
description: Aggiunta di tabelle derivate a query (Visual Database Tools)
title: Aggiungere tabelle derivate a query
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [Visual Database Tools]
- joins [SQL Server], derived tables
- table joins [SQL Server]
- derived tables
ms.assetid: 05f1ba1d-465f-4e36-84bb-21b963c9b8f9
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: ec4389810e09af78f61e99762dbb30862919f1d1
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037189"
---
# <a name="add-derived-tables-to-queries-visual-database-tools"></a>Aggiunta di tabelle derivate a query (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Le tabelle derivate sono set di risultati utilizzati come origini di tabella in una query. È possibile aggiungere una tabella derivata a una query nel **riquadro Diagramma**.  
  
### <a name="to-add-a-derived-table-to-a-query"></a>Per aggiungere una tabella derivata a una query  
  
1.  Aprire una query esistente o creare una nuova query.  
  
2.  Fare clic con il pulsante destro del mouse sul **riquadro Diagramma** e scegliere **Aggiungi nuova tabella derivata**.  
  
    Verrà aggiunta una nuova tabella con il nome derivedtbl_*N* e l'istruzione SELECT della tabella derivata verrà aggiunta alla clausola FROM della query.  
  
## <a name="see-also"></a>Vedere anche  
[Eseguire operazioni di base con le query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[Creare query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[Apertura di query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-queries-visual-database-tools.md)  
[SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
