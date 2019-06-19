---
title: Condizioni di test personalizzate per unit test di SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 32a15d61-e908-4ae1-a238-4fd0f988d8c8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6573a8667224eacef61c9c22cb4ede026e7d0a61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106325"
---
# <a name="custom-test-conditions--for-sql-server-unit-tests"></a>Condizioni di test personalizzate per unit test di SQL Server
È possibile aggiungere condizioni di test personalizzate per unit test di SQL Server. Tuttavia, è necessario installare la condizione di test prima di poterla utilizzare, a prescindere se l'estensione è stata creata o se ne sta installando una creata da qualcun altro.  
  
Prima di installare una condizione di test creata da altri, è necessario comprendere i rischi dell'operazione:  
  
-   Il programma di installazione della condizione di test potrebbe essere dannoso e ottenere l'accesso alle risorse protette in base alle autorizzazioni di installazione concesse.  
  
-   La condizione di test in se potrebbe essere dannosa e ottenere il controllo delle risorse protette se l'utente che utilizza l'estensione dispone delle autorizzazioni sufficienti.  
  
Per ridurre il rischio, è necessario installare una condizione di test personalizzata solo se proviene da un'origine nota. Se la condizione di test proviene da un'origine non attendibile, è necessario controllare il codice sorgente della condizione di test e il programma di installazione (se disponibile) prima di installarla.  
  
Per installare una condizione di test personalizzata, è necessario copiare l'assembly firmato (con estensione dll) nella cartella %Programmi%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions. Se la cartella non esiste, è necessario crearla. È necessario disporre dei privilegi amministrativi del computer in uso per eseguire la copia in questa directory.  
  
> [!NOTE]  
> È necessario installare le versioni Visual Studio 2010 e Visual Studio 2012 della condizione di test se:  
>   
> -   Le condizioni di test personalizzate vengono installate in un computer che potrebbe essere usato per compilare unit test di SQL Server.  
> -   Tali unit test vengono utilizzati in Visual Studio 2010 e Visual Studio 2012.  
  
Per altre informazioni sulle condizioni di test personalizzate per unit test di SQL Server, vedere:  
  
-   [Procedura: Creare condizioni di test per la finestra di progettazione unit test di SQL Server](../ssdt/how-to-create-test-conditions-for-the-sql-server-unit-test-designer.md)  
  
-   [Procedura: Aggiornare una condizione di test personalizzata di Visual Studio 2010 da una versione precedente a SQL Server Data Tools](../ssdt/how-to-upgrade-visual-studio-2010-custom-test-condition-to-ssdt.md)  
  
-   [Procedura dettagliata: Uso di una condizione di test personalizzata per verificare i risultati di una stored procedure](../ssdt/walkthrough-use-custom-test-condition-to-verify-stored-procedure-results.md)  
  
## <a name="see-also"></a>Vedere anche  
[Verifica del codice di database tramite unit test di SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
