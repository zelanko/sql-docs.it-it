---
title: 'Procedura: Creare unit test di SQL Server per funzioni, trigger e stored procedure | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5d985e2b2638d8b0047f5b4d010d87c8f631af65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090219"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>Procedura: Creare unit test di SQL Server per funzioni, trigger e stored procedure
È possibile scrivere unit test che restituiscono le modifiche apportate a qualsiasi oggetto di database. Tuttavia, in SQL Server Data Tools sono incluse funzionalità di supporto aggiuntive per creare test per stored procedure, trigger e funzioni di database dal nodo di un progetto di database in Esplora oggetti di SQL Server. È possibile generare automaticamente stub di codice Transact\-SQL personalizzabili.  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>Per creare uno unit test di SQL Server da una funzione, un trigger o una stored procedure  
  
1.  Vedere [Procedura dettagliata: Creazione ed esecuzione di uno unit test di SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md) per un esempio di aggiunta di uno unit test per una stored procedure, nella sezione relativa alla creazione di uno unit test di SQL Server per le stored procedure.  
  
    La condizione di test Senza risultati è la condizione predefinita aggiunta a ogni test. Questa condizione di test viene inclusa per indicare che la verifica del test non è stata implementata. Eliminare tale condizione dal test dopo l'aggiunta di altre condizioni di test. Per altre informazioni, vedere [Procedura: Aggiungere condizioni di test a unit test di SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md).  
  
## <a name="see-also"></a>Vedere anche  
[Creazione e definizione di unit test di SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Procedura: Creare uno unit test di SQL Server vuoto](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
