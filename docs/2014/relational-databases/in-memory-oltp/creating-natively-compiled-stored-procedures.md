---
title: Creazione di stored procedure compilate in modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9525ef65973baa38ae19ba4681e4a93f949c004a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63071820"
---
# <a name="creating-natively-compiled-stored-procedures"></a>Creazione di stored procedure compilate in modo nativo
  Le stored procedure compilate in modo nativo non implementano la programmabilità completa di [!INCLUDE[tsql](../../includes/tsql-md.md)] e la superficie di attacco delle query. Alcuni costrutti [!INCLUDE[tsql](../../includes/tsql-md.md)] non possono essere utilizzati all'interno delle stored procedure compilate in modo nativo. Per ulteriori informazioni, vedere [costrutti supportati nelle stored procedure compilate in modo nativo](../in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 Esistono, tuttavia, alcune funzionalità di [!INCLUDE[tsql](../../includes/tsql-md.md)] che sono supportate solo per le stored procedure compilate in modo nativo:  
  
-   Blocchi atomici. Per altre informazioni, vedere [Atomic Blocks](atomic-blocks-in-native-procedures.md).  
  
-   Vincoli `NOT NULL` su parametri e variabili nelle stored procedure compilate in modo nativo. Non è possibile assegnare valori `NULL` ai parametri o alle variabili dichiarate come `NOT NULL`. Per altre informazioni, vedere [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql).  
  
-   Associazione allo schema delle stored procedure compilate in modo nativo.  
  
 Le stored procedure compilate in modo nativo vengono create usando [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql). Nell'esempio seguente vengono illustrate una tabella ottimizzata per la memoria e una stored procedure compilata in modo nativo per inserire righe nella tabella.  
  
```sql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding, execute as owner  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 Nell'esempio di codice `NATIVE_COMPILATION` indica che questa stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] è una stored procedure compilata in modo nativo. Sono necessarie le opzioni seguenti:  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|`SCHEMABINDING`|Le stored procedure compilate in modo nativo devono essere associate allo schema degli oggetti a cui fa riferimento. Ciò significa che i riferimenti alla tabella della procedura non possono essere eliminati. Le tabelle a cui viene fatto riferimento nella procedura devono includere il nome dello schema e\*i caratteri jolly () non sono consentiti nelle query. `SCHEMABINDING` è supportato unicamente per le stored procedure compilate in modo nativo in questa versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`EXECUTE AS`|Le stored procedure compilate in modo nativo non supportano `EXECUTE AS CALLER`, ovvero il contesto di esecuzione predefinito. Di conseguenza, è necessario specificare il contesto di esecuzione. Sono supportate `EXECUTE AS OWNER`le `EXECUTE AS`opzioni, *User*e `EXECUTE AS SELF` .|  
|`BEGIN ATOMIC`|Il corpo di una stored procedure compilata in modo nativo deve essere costituito esattamente da un blocco atomico. I blocchi atomici garantiscono l'esecuzione atomica della stored procedure. Se la stored procedure viene richiamata all'esterno del contesto di una transazione attiva, verrà avviata una nuova transazione il cui commit avverrà alla fine del blocco atomico. I blocchi atomici nelle stored procedure compilate in modo nativo presentano due opzioni obbligatorie:<br /><br /> `TRANSACTION ISOLATION LEVEL`. Vedere [livelli di isolamento delle transazioni](../../database-engine/transaction-isolation-levels.md) per i livelli di isolamento supportati.<br /><br /> `LANGUAGE`. Il linguaggio della stored procedure deve essere impostato su uno dei linguaggi o alias disponibili.|  
  
 In relazione a `EXECUTE AS` e agli account di accesso di Windows, può verificarsi un errore a causa della rappresentazione eseguita tramite `EXECUTE AS`. Se un account utente utilizza l'autenticazione di Windows, è necessario che vi sia attendibilità totale tra l'account del servizio utilizzato per l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e il dominio dell'account di accesso di Windows. Se non è presente alcuna attendibilità totale, quando si crea una stored procedure compilata in modo nativo viene restituito il messaggio di errore seguente: messaggio 15404, non è stato possibile ottenere informazioni relative al gruppo/utente di Windows NT ' username ', codice di errore 0x5.  
  
 Per risolvere l'errore, utilizzare una delle soluzioni seguenti:  
  
-   Utilizzare un account dello stesso dominio dell'utente di Windows per il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizza un account computer, ad esempio Servizio di rete o Sistema locale, il computer deve essere considerato attendibile dal dominio che contiene l'utente di Windows.  
  
-   Utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Durante la creazione di una stored procedure compilata in modo nativo, potrebbe essere visualizzato l'errore 15517. Per ulteriori informazioni, vedere [MSSQLSERVER_15517](../errors-events/mssqlserver-15517-database-engine-error.md).  
  
## <a name="updating-a-natively-compiled-stored-procedure"></a>Aggiornamento di una stored procedure compilata in modo nativo  
 L'esecuzione di operazioni di modifica nelle stored procedure compilate in modo nativo non è supportata. Per modificare una stored procedure compilata in modo nativo è possibile eliminare e ricreare la stored procedure:  
  
1.  Generare lo script per le autorizzazioni della stored procedure.  
  
2.  Facoltativamente, generare lo script per la stored procedure e il salvataggio come backup.  
  
3.  Eliminare la stored procedure.  
  
4.  Creare la stored procedure modificata.  
  
5.  Riapplicare le autorizzazioni dello script alla stored procedure.  
  
 Lo svantaggio di questa procedura consiste nel fatto che l'applicazione sarà offline dall'inizio del passaggio 3 alla fine del passaggio 5. È possibile che siano necessari alcuni secondi e che il client che utilizza l'applicazione riceva messaggi di errore.  
  
 Un'altra soluzione efficace per modificare una stored procedure compilata in modo nativo consiste nel creare innanzitutto una nuova versione della stored procedure. In questo caso, la stored procedure compilata in modo nativo ha un numero di versione associato. La versione precedente si chiama SP_Vold e la nuova versione SP_Vnew.  
  
1.  Generare lo script per le autorizzazioni di SP_Vold.  
  
2.  Creare SP_Vnew.  
  
3.  Applicare le autorizzazioni di SP_Vold a SP_Vnew.  
  
4.  Aggiornare i riferimenti a SP_Vold in modo che puntino a SP_Vnew. Questa operazione può essere eseguita in diversi modi, ad esempio:  
  
     Utilizzare una stored procedure (basata su disco) wrapper e modificare tale procedura in modo che punti a SP_Vnew. Lo svantaggio di questo approccio sta nell'impatto del riferimento indiretto sulle prestazioni.  
  
    ```sql  
    ALTER PROCEDURE dbo.SP p1,...,pn  
    AS  
      EXEC dbo.SP_Vnew p1,...,pn  
    GO  
    ```  
  
5.  Facoltativamente, eliminare SP_Vold.  
  
 Il vantaggio di questo approccio consiste nel fatto che l'applicazione non risulta offline. Tuttavia, è necessario più impegno per mantenere i riferimenti e verificare che puntino sempre alla versione più recente della stored procedure.  
  
## <a name="see-also"></a>Vedi anche  
 [stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)  
  
  
