---
title: Creare unit test di SQL Server per funzioni, trigger e stored procedure
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c7218f035ca907bf9052865408b3a7311e8f75b4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241465"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>Procedura: Creare unit test di SQL Server per funzioni, trigger e stored procedure

È possibile scrivere unit test che restituiscono le modifiche apportate a qualsiasi oggetto di database. Tuttavia, in SQL Server Data Tools sono incluse funzionalità di supporto aggiuntive per creare test per stored procedure, trigger e funzioni di database dal nodo di un progetto di database in Esplora oggetti di SQL Server. È possibile generare automaticamente stub di codice Transact\-SQL personalizzabili.  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>Per creare uno unit test di SQL Server da una funzione, un trigger o una stored procedure  
  
1.  Vedere [Procedura dettagliata: Creazione ed esecuzione di uno unit test di SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md) per un esempio di aggiunta di uno unit test per una stored procedure, nella sezione relativa alla creazione di uno unit test di SQL Server per le stored procedure.  
  
    La condizione di test Senza risultati è la condizione predefinita aggiunta a ogni test. Questa condizione di test viene inclusa per indicare che la verifica del test non è stata implementata. Eliminare tale condizione dal test dopo l'aggiunta di altre condizioni di test. Per altre informazioni, vedere [Procedura: Aggiungere condizioni di test a unit test di SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md).  
  
## <a name="see-also"></a>Vedere anche  
[Creazione e definizione di unit test di SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Procedura: Creare uno unit test di SQL Server vuoto](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
