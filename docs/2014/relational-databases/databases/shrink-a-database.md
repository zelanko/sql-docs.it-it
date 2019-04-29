---
title: Compattare un database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.shrinkdatabase.f1
helpviewer_keywords:
- shrinking databases
- databases [SQL Server], shrinking
- decreasing database size
- database shrinking [SQL Server]
- reducing database size
ms.assetid: 83afbf74-fd50-4c39-831c-b1f473a50620
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21f58cd6991b760edeefb81c37e02c617f8e09cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917008"
---
# <a name="shrink-a-database"></a>Compattare un database
  In questo argomento si illustra come compattare un database mediante Esplora oggetti in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Compattando i file di dati si recupera spazio spostando le pagine di dati dalla fine del file allo spazio non occupato più vicino all'inizio del file. Quando alla fine del file viene creato sufficiente spazio libero, le pagine di dati possono essere deallocate e restituite al file system.  
  

  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Non è possibile ridurre il database a dimensioni inferiori a quelle minime. Le dimensioni minime corrispondono alle dimensioni specificate quando il database è stato inizialmente creato o alle ultime dimensioni impostate in modo esplicito mediante un'operazione di modifica delle dimensioni dei file, ad esempio DBCC SHRINKFILE. Pertanto, se originariamente è stato creato un database con dimensioni pari a 10 MB e le dimensioni sono aumentate fino a 100 MB, è possibile compattare il database fino a un minimo di 10 MB, anche se tutti i dati nel database sono stati eliminati.  
  
-   Non è possibile compattare un database mentre ne viene eseguito il backup e non è possibile eseguire il backup di un database mentre è in corso un'operazione di compattazione.  
  
-   Se viene rilevato un indice columnstore ottimizzato in memoria xVelocity, DBCC SHRINKDATABASE avrà esito negativo. L'operazione avrà esito positivo se completata prima del rilevamento dell'indice columnstore ottenendo dimensioni del database inferiori. Per completare DBCC SHRINKDATABASE, disabilitare tutti gli indici columnstore prima di eseguire DBCC SHRINKDATABASE, quindi ricompilare gli indici columnstore.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Per visualizzare la quantità corrente di spazio disponibile, cioè non allocato, nel database. Per altre informazioni, vedere [Visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database](display-data-and-log-space-information-for-a-database.md)  
  
-   Quando si pianifica la compattazione di un database, considerare le informazioni seguenti:  
  
    -   Un'operazione di compattazione è più efficace dopo l'esecuzione di un'operazione che crea una quantità elevata di spazio inutilizzato, ad esempio il troncamento o l'eliminazione di una tabella.  
  
    -   La maggior parte dei database richiede spazio disponibile per lo svolgimento delle normali attività quotidiane. Se si compatta ripetutamente un database ma le sue dimensioni aumentano di nuovo significa che lo spazio compattato è necessario per le normali operazioni. In questi casi è inutile compattare ripetutamente il database.  
  
    -   L'operazione di compattazione generalmente aumenta la frammentazione degli indici del database. Questo è un ulteriore motivo per evitare di compattare ripetutamente un database.  
  
    -   Se non è necessario soddisfare esigenze specifiche, non impostare l'opzione di database AUTO_SHRINK su ON.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o al ruolo predefinito del database **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-shrink-a-database"></a>Per compattare un database  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere **Database**, quindi fare clic con il pulsante destro del mouse sul database che si vuole compattare.  
  
3.  Scegliere **Attività**, **Compatta**, quindi fare clic su **Database**.  
  
     **Database**  
     Consente di visualizzare il nome del database selezionato.  
  
     **Spazio allocato**  
     Consente di visualizzare lo spazio totale utilizzato e inutilizzato per il database selezionato.  
  
     **Spazio disponibile**  
     Consente di visualizzare lo spazio disponibile totale nei file di log e di dati del database selezionato.  
  
     **Riorganizza i file prima di rilasciare lo spazio inutilizzato**  
     La selezione di questa opzione equivale all'esecuzione di DBCC SHRINKDATABASE specificando la percentuale di compattazione. Deselezionare l'opzione equivale all'esecuzione di DBCC SHRINKDATABASE con l'opzione TRUNCATEONLY. Per impostazione predefinita, questa opzione non è selezionata all'apertura della finestra di dialogo. Se viene selezionata, l'utente deve specificare la percentuale di compattazione.  
  
     **Spazio massimo disponibile nei file dopo la compattazione**  
     Immettere la massima percentuale di spazio che si desidera sia disponibile nei file del database dopo la compattazione del database. I valori consentiti sono compresi tra 0 e 99.  
  
4.  Fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-shrink-a-database"></a>Per compattare un database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. In questo esempio si utilizza [DBCC SHRINKDATABASE](/sql/t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql) per ridurre le dimensioni dei file di dati e di log nel database `UserDB` e per ottenere il `10` percento di spazio disponibile nel database.  
  
 [!code-sql[DBCC#DBCC_SHRINKDB1](../../snippets/tsql/SQL14/tsql/dbcc/transact-sql/dbcc_other.sql#dbcc_shrinkdb1)]  
  
##  <a name="FollowUp"></a> Completamento: Dopo la compattazione di un database  
 I dati spostati per ridurre un file possono essere dispersi in qualsiasi percorso disponibile nel file, provocando la frammentazione dell'indice e rallentando le prestazioni di query che eseguono ricerche in un intervallo dell'indice Per eliminare la frammentazione, valutare la possibilità di ricompilare gli indici sul file dopo la compattazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Compattare un file](shrink-a-file.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)   
 [Filegroup e file di database](database-files-and-filegroups.md)  
  
  
