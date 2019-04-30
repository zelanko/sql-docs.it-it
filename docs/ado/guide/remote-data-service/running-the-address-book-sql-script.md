---
title: Esecuzione dello Script SQL libro indirizzo | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c77bece1b2ab67cc361f7445240e1a2b1190587
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191777"
---
# <a name="running-the-address-book-sql-script"></a>Esecuzione dello script SQL per Address Book
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 È necessario usare l'utilità della riga di comando ISQL/Query Analyzer o SQL Server Enterprise Manager per eseguire lo script SQL incluso (Sampleemp.sql) che:  
  
-   Crea un nuovo database, AddrBookDB, nel dispositivo predefinito.  
  
-   Si connette al database, AddrBookDB.  
  
-   Crea una tabella dei dipendenti.  
  
-   Popola la tabella con dati di esempio.  
  
-   Esegue un'istruzione SELECT semplice per verificare il popolamento della tabella di database.  
  
-   Configura un account utente denominato "adcdemo" con la password "adcdemo."  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Per eseguire lo script Sampleemp.sql in Microsoft SQL Server 6.5  
  
1.  Fare clic su **avviare**, scegliere **programmi**, quindi scegliere **Microsoft SQL Server 6.5**. Fare clic su **SQL Enterprise Manager**.  
  
2.  Dal **Tools** menu, fare clic su **strumento di Query SQL**.  
  
3.  Fare clic su **lo Script SQL del carico** e passare a c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Selezionare il file Sampleemp.sql. Fare clic su **Apri**.  
  
5.  Scegliere il **Esegui Query** (la freccia verde sulla barra degli strumenti).  
  
6.  Dopo l'esecuzione, chiudere la **Query** e **Enterprise Manager** windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Per eseguire lo script Sampleemp.sql in Microsoft SQL Server 7.0  
  
1.  Fare clic su **avviare**, scegliere **programmi**, quindi scegliere **Microsoft SQL Server 7.0**. Fare clic su **Enterprise Manager**.  
  
2.  Assicurarsi che sia selezionato il Server SQL che si vuole usare dall'elenco dei server registrati in Enterprise Manager.  
  
3.  Dal **degli strumenti** menu, fare clic su **Query Analyzer di SQL Server**.  
  
4.  Scegliere il **lo Script SQL del carico** pulsante (la cartella aperta sulla barra degli strumenti) e accedere a c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Selezionare il file Sampleemp.sql. Fare clic su **Apri**.  
  
6.  Scegliere il **Esegui Query** (la freccia verde sulla barra degli strumenti) o **F5**.  
  
7.  Dopo l'esecuzione, chiudere la **Query**, **Query Analyzer**, e **Enterprise Manager** windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione dell'applicazione di esempio Address Book](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


