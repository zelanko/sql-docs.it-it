---
title: 'Procedura: Connettersi a un database e visualizzare gli oggetti esistenti | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.connectionpicker.f1
ms.assetid: 9b331800-3806-4459-ac58-88cdc98124d3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 21096819ebd7a54ab8f4505ad980c0e6a5266d6f
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65098110"
---
# <a name="how-to-connect-to-a-database-and-browse-existing-objects"></a>Procedura: Connettersi a un database e visualizzare gli oggetti esistenti
Un'attività molto comune per sviluppatori e amministratori di database è connettersi a un database attivo, progettare o sfogliare il relativo schema ed eseguire una query sugli oggetti. In Esplora oggetti di SQL Server in Visual Studio è ora disponibile un nodo **SQL Server** dedicato in cui tutte le istanze di SQL Server connesse e i relativi database sono raggruppati in una gerarchia analoga a quella di SSMS. Le istanze di SQL Server connesse possono essere locali, quale l'esecuzione di SQL Server 2008, o istanze di SQL Azure ospitate.  
  
Nella procedura seguente si presuppone che si dispone già di un database di esempio AdventureWorks installato. Usare [CodePlex](https://msftdbprodsamples.codeplex.com/) per individuare e installare database di esempio per diverse versioni di SQL Server. Se si preferisce, è possibile seguire anche i passaggi e utilizzare un database esistente nel server.  
  
### <a name="to-connect-to-a-database-instance"></a>Per connettersi a un'istanza del database  
  
1.  In Visual Studio verificare che **Esplora oggetti di SQL Server** sia aperto. In caso contrario, fare clic sul menu **Visualizza** e selezionare **Esplora oggetti di SQL Server**.  
  
2.  Fare clic con il pulsante destro del mouse sul nodo **SQL Server** in **Esplora oggetti di SQL Server** e selezionare **Aggiungi SQL Server**.  
  
3.  Nella finestra di dialogo **Connetti al server** immettere il **Nome server** dell'istanza del server a cui si desidera eseguire la connessione, le credenziali e fare clic su **Connetti**.  
  
4.  In **Esplora oggetti di SQL Server** espandere il nodo **Database** nell'istanza del server. Verranno visualizzati tutti i database che si trovano in questa istanza del server aggiunta in questo nodo **Database** .  
  
5.  Espandere il nodo **AdventureWorks** (o un altro database). Si noterà che tutte le entità del database sono organizzate in una gerarchia simile a SQL Server Management Studio.  
  
