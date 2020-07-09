---
title: Creare trigger annidati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- DML triggers, nested
- triggers [SQL Server], nested
- direct recursion [SQL Server]
- triggers [SQL Server], recursive
- DML triggers, recursive
- RECURSIVE_TRIGGERS option
- indirect recursion [SQL Server]
- nested DML triggers
ms.assetid: cd522dda-b4ab-41b8-82b0-02445bdba7af
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 357dae5608e938eda4ea4fd42a92420f9297958e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757666"
---
# <a name="create-nested-triggers"></a>Creazione di trigger annidati
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Entrambi i trigger DML e DDL vengono nidificati quando un trigger esegue un'operazione che ne avvia un altro. Tali operazioni possono quindi avviare altri trigger e così via. I trigger DML e DDL possono essere nidificati fino a un massimo di 32 livelli. Per gestire la nidificazione dei trigger AFTER, utilizzare l'opzione di configurazione del server **nested triggers** . I trigger INSTEAD OF (solo DML) possono essere nidificati indipendentemente da questa impostazione.  
  
> [!NOTE]  
>  Qualsiasi riferimento a codice gestito da un trigger [!INCLUDE[tsql](../../includes/tsql-md.md)] viene conteggiato come un unico livello rispetto al limite dei 32 livelli di nidificazione. I metodi richiamati da codice gestito non vengono inclusi nel conteggio per questo limite.  
  
 Se è consentito l'utilizzo di trigger nidificati e un trigger della catena avvia un ciclo infinito, il livello di nidificazione viene superato e il trigger viene interrotto.  
  
 È possibile utilizzare i trigger nidificati per eseguire funzioni di manutenzione, utili quali l'archiviazione di una copia di backup delle righe interessate da un trigger precedente. È ad esempio possibile creare un trigger su `PurchaseOrderDetail` per salvare una copia di backup delle righe di `PurchaseOrderDetail` eliminate dal trigger `delcascadetrig` . Se il trigger `delcascadetrig` è attivo, l'eliminazione di `PurchaseOrderID` 1965 dalla tabella `PurchaseOrderHeader` implica l'eliminazione della riga o delle righe corrispondenti da `PurchaseOrderDetail`. Per salvare i dati eliminati in un'altra tabella creata separatamente denominata `PurchaseOrderDetail` , creare un trigger DELETE su `del_save`. Ad esempio:  
  
```  
CREATE TRIGGER Purchasing.savedel  
   ON Purchasing.PurchaseOrderDetail  
FOR DELETE  
AS  
   INSERT del_save;  
   SELECT * FROM deleted;  
```  
  
 È consigliabile non utilizzare trigger nidificati in una sequenza dipendente dall'ordinamento. Utilizzare trigger distinti per eseguire modifiche a catena dei dati.  
  
> [!NOTE]  
>  Poiché i trigger vengono eseguiti all'interno di una transazione, un errore a qualsiasi livello di un set di trigger nidificati annulla l'intera transazione con conseguente rollback di tutte le modifiche apportate ai dati. Per determinare la posizione in cui si è verificato l'errore, includere nei trigger le istruzioni PRINT.  
  
## <a name="recursive-triggers"></a>Trigger ricorsivi  
 Un trigger AFTER non chiama se stesso in modo ricorsivo a meno che non sia stata impostata l'opzione di database RECURSIVE_TRIGGERS.  
  
 Esistono due tipi di ricorsione:  
  
-   Ricorsione diretta  
  
     Questo tipo di ricorsione si verifica quando un trigger viene attivato ed esegue un'azione che attiva nuovamente lo stesso trigger. Ad esempio, un'applicazione aggiorna la tabella **T3**che attiva il trigger **Trig3** . **Trig3** aggiorna nuovamente la tabella **T3** , che attiva nuovamente il trigger **Trig3** .  
  
     La ricorsione diretta può inoltre verificarsi quando lo stesso trigger viene richiamato, ma solo dopo la chiamata di un trigger di tipo diverso (AFTER o INSTEAD OF). In altri termini, la ricorsione diretta di un trigger INSTEAD OF può verificarsi quando lo stesso trigger INSTEAD OF viene chiamato per la seconda volta, anche se nel frattempo sono stati chiamati uno o più trigger AFTER. Analogamente, la ricorsione diretta di un trigger AFTER può verificarsi quando lo stesso trigger AFTER viene chiamato per la seconda volta, anche se nel frattempo sono stati chiamati uno o più trigger INSTEAD OF. Ad esempio, un'applicazione aggiorna la tabella **T4**. L'aggiornamento attiva il trigger INSTEAD OF **Trig4** . **Trig4** aggiorna la tabella **T5**. L'aggiornamento attiva il trigger AFTER **Trig5** . **Trig5** aggiorna la tabella **T4**e questa operazione attiva nuovamente il trigger INSTEAD OF **Trig4** . Questa catena di eventi costituisce una ricorsione diretta per il trigger **Trig4**.  
  
-   Ricorsione indiretta  
  
     Questo tipo di ricorsione si verifica quando un trigger viene attivato ed esegue un'azione che attiva un altro trigger dello stesso tipo (AFTER o INSTEAD OF). Il secondo esegue un'operazione che implica nuovamente l'attivazione del trigger originale. In altri termini, la ricorsione indiretta può verificarsi quando un trigger INSTEAD OF viene chiamato per la seconda volta, ma non prima della chiamata di un altro trigger INSTEAD OF. Analogamente, la ricorsione indiretta può verificarsi quando un trigger AFTER viene chiamato per la seconda volta, ma non prima della chiamata di un altro trigger AFTER. Ad esempio, un'applicazione aggiorna la tabella **T1**. L'aggiornamento attiva il trigger AFTER **Trig1** . **Trig1** aggiorna la tabella **T2**e questa operazione attiva il trigger AFTER **Trig2** . **Trig2** aggiorna, a sua volta, la tabella **T1** che attiva nuovamente il trigger AFTER **Trig1** .  
  
 Se l'opzione di database RECURSIVE_TRIGGERS è impostata su OFF, viene evitata solo la ricorsione diretta dei trigger AFTER. Per disabilitare la ricorsione indiretta dei trigger AFTER, impostare su **0** anche l'opzione del server **nested triggers**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo dei trigger ricorsivi per risolvere una relazione autoreferenziale, nota anche come chiusura transitiva. Ad esempio, nella tabella `emp_mgr` vengono definiti gli elementi seguenti:  
  
-   Il dipendente (`emp`) di una società.  
  
-   Il responsabile di ciascun dipendente (`mgr`).  
  
-   Il numero totale di dipendenti nell'albero organizzativo di cui ogni dipendente è responsabile (`NoOfReports`).  
  
 È possibile utilizzare un trigger UPDATE ricorsivo per aggiornare la colonna `NoOfReports` quando vengono inseriti i record di nuovi dipendenti. Il trigger INSERT aggiorna la colonna `NoOfReports` del record del responsabile che aggiorna in modo ricorsivo la colonna `NoOfReports` degli altri record fino ai livelli più alti dell'organigramma.  
  
```  
USE AdventureWorks2012;  
GO  
-- Turn recursive triggers ON in the database.  
ALTER DATABASE AdventureWorks2012  
   SET RECURSIVE_TRIGGERS ON;  
GO  
CREATE TABLE dbo.emp_mgr (  
   emp char(30) PRIMARY KEY,  
    mgr char(30) NULL FOREIGN KEY REFERENCES emp_mgr(emp),  
    NoOfReports int DEFAULT 0  
);  
GO  
CREATE TRIGGER dbo.emp_mgrins ON dbo.emp_mgr  
FOR INSERT  
AS  
DECLARE @e char(30), @m char(30);  
DECLARE c1 CURSOR FOR  
   SELECT emp_mgr.emp  
   FROM   emp_mgr, inserted  
   WHERE emp_mgr.emp = inserted.mgr;  
  
OPEN c1;  
FETCH NEXT FROM c1 INTO @e;  
WHILE @@fetch_status = 0  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Add 1 for newly  
   WHERE emp_mgr.emp = @e ;                           -- added employee.  
  
   FETCH NEXT FROM c1 INTO @e;  
END  
CLOSE c1;  
DEALLOCATE c1;  
GO  
-- This recursive UPDATE trigger works assuming:  
--   1. Only singleton updates on emp_mgr.  
--   2. No inserts in the middle of the org tree.  
CREATE TRIGGER dbo.emp_mgrupd ON dbo.emp_mgr FOR UPDATE  
AS  
IF UPDATE (mgr)  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Increment mgr's  
   FROM inserted                            -- (no. of reports) by  
   WHERE emp_mgr.emp = inserted.mgr;         -- 1 for the new report.  
  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports - 1 -- Decrement mgr's  
   FROM deleted                             -- (no. of reports) by 1  
   WHERE emp_mgr.emp = deleted.mgr;          -- for the new report.  
END  
GO  
-- Insert some test data rows.  
INSERT dbo.emp_mgr(emp, mgr) VALUES  
    ('Harry', NULL)  
    ,('Alice', 'Harry')  
    ,('Paul', 'Alice')  
    ,('Joe', 'Alice')  
    ,('Dave', 'Joe');  
GO  
SELECT emp,mgr,NoOfReports  
FROM dbo.emp_mgr;  
GO  
-- Change Dave's manager from Joe to Harry  
UPDATE dbo.emp_mgr SET mgr = 'Harry'  
WHERE emp = 'Dave';  
GO  
SELECT emp,mgr,NoOfReports FROM emp_mgr;  
  
GO  
```  
  
 Risultati prima dell'aggiornamento.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Joe                            0  
Harry                          NULL                           1  
Joe                            Alice                          1  
Paul                           Alice                          0  
```  
  
 Risultati dopo l'aggiornamento.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Harry                          0  
Harry                          NULL                           2  
Joe                            Alice                          0  
Paul                           Alice                          0  
```  
  
 **Per impostare l'opzione nested triggers**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 **Per impostare l'opzione di database RECURSIVE_TRIGGERS**  
  
-   [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Configurare l'opzione di configurazione del server nested triggers](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)  
  
  
