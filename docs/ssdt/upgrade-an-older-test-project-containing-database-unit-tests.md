---
title: Aggiornare un progetto di test precedente contenente unit test del database | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 42782ff3-e8cf-4c9d-8dac-a95b236edfc4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b2ad973cf845817a0dbd251bbee23ac6f13d7c04
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110581"
---
# <a name="upgrade-an-older-test-project-containing-database-unit-tests"></a>Aggiornare un progetto di test precedente contenente unit test del database
È possibile aggiornare un progetto di test precedente creato in Visual Studio 2010 contenente gli unit test del database in modo da usare i nuovi strumenti e runtime per unit test del database SQL Server Data Tools. Dopo aver aggiornato un progetto precedente è possibile aggiungere unit test di SQL Server al progetto. Per altre informazioni, vedere [Creazione e definizione di unit test di SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md).  
  
> [!TIP]  
> Se si usa Visual Studio 2010, dopo aver aggiunto gli unit test di SQL Server a un progetto dei test, non è possibile aggiungere unit test usando il vecchio modello di unit test del database. Se viene utilizzato, è necessario convertire nuovamente il progetto per poter eseguire correttamente i test.  
  
Se un progetto di database di test è stato creato con una versione precedente a Visual Studio 2010, è possibile seguire l'argomento [Procedura: Aggiornare unit test di database da versioni precedenti di Visual Studio](https://msdn.microsoft.com/library/dd193412(VS.100).aspx) per aggiornare il progetto di database a Visual Studio 2010, prima di aggiornarlo a SQL Server Data Tools.  
  
### <a name="initiating-an-upgrade"></a>Avvio di un aggiornamento  
  
-   È possibile avviare un aggiornamento del progetto dal menu di scelta rapida di un progetto di test.  
  
    In alcuni casi, SQL Server Data Tools visualizza una finestra di dialogo da cui è possibile avviare l'aggiornamento di un progetto di test.  
  
-   L'aggiornamento del progetto rimuove il riferimento dell'assembly al precedente framework di test del database e aggiunge un riferimento al nuovo framework e un assembly dell'adattatore. Anche il file app.config viene aggiornato.  
  
    > [!NOTE]  
    > Se il progetto di test include i file di codice per DatabaseSetup e SQLDatabaseSetup, l'aggiornamento del progetto a SQL Server Data Tools esclude il file DatabaseSetup dalla compilazione. È possibile rimuovere il file DatabaseSetup se viene escluso dalla compilazione.  
  
-   Dopo la conversione, gli unit test del database creati con il modello precedente utilizzeranno i tipi presenti nell'assembly dell'adattatore per accedere al nuovo framework. L'utilizzo dell'assembly dell'adattatore fa si che la procedura di aggiornamento non modifichi il codice e gli script di test. Se si aggiunge uno unit test di SQL Server al progetto, il nuovo test farà riferimento al nuovo framework direttamente e non tramite l'adattatore. È possibile scegliere di aggiornare manualmente il codice per utilizzare il nuovo framework per congruenza con i nuovi test, ma non è obbligatorio.  
  
## <a name="see-also"></a>Vedere anche  
[Verifica del codice di database tramite unit test di SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
