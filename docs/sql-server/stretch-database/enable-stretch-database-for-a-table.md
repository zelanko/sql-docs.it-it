---
title: Abilitare Stretch Database per una tabella
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, enabling table
- enabling table for Stretch Database
ms.assetid: de4ac0c5-46ef-4593-a11e-9dd9bcd3ccdc
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 49d3f7fa266be69c767b0fb0450cc6898351f39b
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843811"
---
# <a name="enable-stretch-database-for-a-table"></a>Abilitare Stretch Database per una tabella
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Per configurare una tabella per Stretch Database, selezionare **Stretch | Abilita** per una tabella in SQL Server Management Studio in modo da aprire la procedura guidata **Abilita la tabella per Stretch**. È anche possibile usare Transact-SQL per abilitare Stretch Database in una tabella esistente o creare una nuova tabella con Stretch Database abilitato.  
  
-   Se i dati ad accesso sporadico vengono archiviati in una tabella separata, è possibile eseguire la migrazione dell'intera tabella.  
  
-   Se la tabella contiene dati usati più di frequente e dati usati meno di frequente, è possibile specificare una funzione di filtro per selezionare le righe di cui eseguire la migrazione.    
 
 **Prerequisiti**. Se si seleziona **Stretch | Abilita** per una tabella e Stretch Database non è ancora stato abilitato per il database, la procedura guidata configura prima di tutto il database per Stretch Database. Seguire i passaggi descritti in [Avviare la procedura guidata Abilitare il database per Stretch](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md) anziché quelli riportati in questo articolo.  
  
 **Autorizzazioni**. Per abilitare Stretch Database in un database o una tabella sono necessarie autorizzazioni db_owner. L'abilitazione di Stretch Database in una tabella richiede anche autorizzazioni ALTER sulla tabella.  

 > [!NOTE]
 > Se successivamente si disabilita Stretch Database, tenere presente che questa operazione per una tabella o per un database non elimina l'oggetto remoto. Se si vuole eliminare la tabella remota o il database remoto, è necessario eliminarlo tramite il portale di gestione di Azure. Gli oggetti remoti continuano a generare costi di Azure fino a quando non vengono eliminati manualmente.
 
##  <a name="EnableWizardTable"></a> Usare la procedura guidata per abilitare Stretch Database in una tabella  
 **Avviare la procedura guidata**  
 1.  In Esplora oggetti di SQL Server Management Studio selezionare la tabella in cui si vuole abilitare l'estensione.  
  
2.  Fare clic con il pulsante destro del mouse e selezionare **Estendi**, quindi scegliere **Abilita** per avviare la procedura guidata.  
  
 **Introduzione**  
 Esaminare lo scopo della procedura guidata e i prerequisiti.  
  
 **Selezionare le tabelle del database**  
 Verificare che la tabella che si vuole abilitare sia visualizzata e selezionata.  
  
 È possibile eseguire la migrazione di un'intera tabella oppure specificare una funzione di filtro semplice nella procedura guidata. Se si vuole usare un tipo diverso di funzione di filtro per selezionare le righe di cui eseguire la migrazione, eseguire una di queste operazioni.  
  
-   Uscire dalla procedura guidata ed eseguire l'istruzione ALTER TABLE per abilitare l'Estensione per la tabella e specificare una funzione di filtro.  
  
-   Eseguire l'istruzione ALTER TABLE per specificare una funzione di filtro dopo l'uscita dalla procedura guidata. Per i passaggi necessari, vedere [Aggiungere una funzione di filtro dopo l'esecuzione della procedura guidata](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz).  
  
 La sintassi di ALTER TABLE è descritta più avanti in questo articolo.  
  
 **Riepilogo**  
 Esaminare i valori immessi e le opzioni selezionate nella procedura guidata. Selezionare quindi **Fine** per abilitare l'estensione.  
  
 **Risultati**  
 Controllare i risultati.  
  
##  <a name="EnableTSQLTable"></a> Usare Transact-SQL per abilitare Stretch Database in una tabella  
 È possibile usare Transact-SQL per abilitare Stretch Database in una tabella esistente o creare una nuova tabella con Stretch Database abilitato.  
  
### <a name="options"></a>Opzioni  
 Usare le opzioni seguenti quando si esegue CREATE TABLE o ALTER TABLE per abilitare Stretch Database in una tabella.  
  
-   Facoltativamente, usare la clausola `FILTER_PREDICATE = <function>` per specificare una funzione che selezioni le righe di cui eseguire la migrazione se la tabella contiene sia dati usati più di frequente sia dati usati meno di frequente. Il predicato deve eseguire la chiamata a una funzione inline con valori di tabella. Per altre informazioni, vedere [Selezionare le righe di cui eseguire la migrazione tramite una funzione di filtro](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Se non si specifica una funzione di filtro, viene eseguita la migrazione dell'intera tabella.  
  
    > [!IMPORTANT]  
    > Se si specifica una funzione di filtro dalle prestazioni scarse, anche la migrazione dei dati avrà prestazioni scarse. Stretch Database applica la funzione di filtro alla tabella usando l'operatore CROSS APPLY.  
  
-   Specificare `MIGRATION_STATE = OUTBOUND` per avviare subito la migrazione dei dati o  `MIGRATION_STATE = PAUSED` per rimandare l'inizio della migrazione dei dati.  
  
### <a name="enable-stretch-database-for-an-existing-table"></a>Abilitare Stretch Database per una tabella esistente  
 Per configurare una tabella esistente per Stretch Database, eseguire il comando ALTER TABLE.  
  
 Ecco un esempio in cui viene eseguita la migrazione dell'intera tabella e la migrazione dei dati viene avviata subito.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 Ecco un esempio in cui viene eseguita la migrazione solo delle righe identificate dalla funzione inline `dbo.fn_stretchpredicate` con valori di tabella e si rimanda l'esecuzione della migrazione dei dati. Per altre informazioni sulla funzione di filtro, vedere [Selezionare le righe di cui eseguire la migrazione tramite una funzione di filtro](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
 GO
```  
  
 Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
### <a name="create-a-new-table-with-stretch-database-enabled"></a>Creare una nuova tabella con Stretch Database abilitato  
 Per creare una nuova tabella con la funzionalità Stretch Database abilitata, eseguire il comando CREATE TABLE.  
  
 Ecco un esempio in cui viene eseguita la migrazione dell'intera tabella e la migrazione dei dati viene avviata subito.  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name>
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 Ecco un esempio in cui viene eseguita la migrazione solo delle righe identificate dalla funzione inline `dbo.fn_stretchpredicate` con valori di tabella e si rimanda l'esecuzione della migrazione dei dati. Per altre informazioni sulla funzione di filtro, vedere [Selezionare le righe di cui eseguire la migrazione tramite una funzione di filtro](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name> 
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
GO  
```  
  
 Per altre informazioni, vedere [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  
