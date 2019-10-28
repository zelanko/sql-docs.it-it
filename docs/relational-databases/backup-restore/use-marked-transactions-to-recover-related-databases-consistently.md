---
title: Usare transazioni contrassegnate per recuperare coerentemente i database correlati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction marks [SQL Server]
- marked transactions [SQL Server]
- database restores [SQL Server], inserting transaction marks for
- recovery [SQL Server], related databases
- restoring databases [SQL Server], related database recovery
- database restores [SQL Server], related databases
- marked transactions [SQL Server], creating
- BEGIN TRAN...WITH MARK statement
- two-phase commit
ms.assetid: 50a73574-1a69-448e-83dd-9abcc7cb7e1a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c884662acb111ab197ebf437d7eaacd5859ebde7
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908785"
---
# <a name="use-marked-transactions-to-recover-related-databases-consistently"></a>Usare transazioni contrassegnate per recuperare coerentemente i database correlati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Le informazioni contenute in questo argomento sono rilevanti solo per i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano i modelli di recupero con registrazione completa o con registrazione minima delle operazioni bulk.  
  
 Quando si eseguono aggiornamenti in due o più *database correlati*, è possibile usare i contrassegni delle transazioni per recuperarli fino a un punto consistente logico. In questo recupero viene tuttavia persa qualsiasi transazione di cui sia stato eseguito il commit dopo il contrassegno utilizzato come punto di recupero. L'utilizzo del contrassegno delle transazioni è adeguato solo quando si esegue il test di database correlati o quando la perdita delle transazioni di cui sia stato eseguito il commit di recente non è importante.  
  
 L'applicazione ripetuta di contrassegni alle transazioni correlate in ogni database correlato determina una serie di punti di recupero comuni nei database. I contrassegni delle transazioni vengono registrati nel log delle transazioni e inclusi nei backup del log. In caso di emergenza, è possibile ripristinare tutti i database rispetto allo stesso contrassegno della transazione per recuperarli fino a una punto consistente.  
  
> [!NOTE]  
>  I backup del log nei diversi database possono essere creati in modo indipendente gli uni dagli altri e non è necessario che siano simultanei.  
  
 Il recupero di database correlati negli scenari seguenti richiede che siano già presenti transazioni contrassegnate in ogni database correlato:  
  
-   Uno o più log delle transazioni sono danneggiati. È necessario ripristinare il set di database in uno stato consistente al momento dell'ultimo backup del log.  
  
-   È necessario ripristinare l'intero set di database in uno stato mutualmente consistente fino a un punto nel tempo precedente.  
  
> [!IMPORTANT]  
>  È possibile recuperare database correlati solo fino a una transazione contrassegnata e non a un momento specifico.  
  
 Per informazioni su come creare transazioni contrassegnate, vedere "Creazione di transazioni contrassegnate", di seguito in questo argomento.  
  
## <a name="typical-scenario-for-using-marked-transactions"></a>Scenario tipico per l'utilizzo delle transazioni contrassegnate  
 Uno scenario tipico per l'utilizzo delle transazioni contrassegnate include i passaggi seguenti:  
  
1.  Creare un backup completo o differenziale del database per ogni database correlato.  
  
2.  Contrassegnare un blocco di transazioni in tutti i database.  
  
3.  Eseguire il backup del log delle transazioni per tutti i database.  
  
4.  Ripristinare i backup dei database WITH NORECOVERY.  
  
5.  Ripristinare i log WITH STOPATMARK.  

## <a name="considerations-for-using-marked-transactions"></a>Considerazioni sull'utilizzo delle transazioni contrassegnate  
 Prima di inserire contrassegni denominati nel log delle transazioni, considerare quanto segue:  
  
-   I contrassegni di transazione occupano spazio nei log e pertanto è consigliabile utilizzarli esclusivamente per transazioni importanti ai fini della strategia di recupero dei database.  
  
-   Dopo il commit di una transazione contrassegnata, viene inserita una riga nella tabella [logmarkhistory](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) del database **msdb**.  
  
-   Se una transazione contrassegnata si estende su più database dello stesso server di database o di server diversi, i contrassegni devono essere registrati nei log di tutti i database interessati.  
  
## <a name="creating-the-marked-transactions"></a>Creazione delle transazioni contrassegnate  
 Per creare una transazione contrassegnata, usare l'istruzione [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) e la clausola WITH MARK [*description*]. L'argomento *description* è facoltativo e rappresenta una descrizione del contrassegno. Il nome del contrassegno della transazione è obbligatorio. È possibile riutilizzare il nome di un contrassegno. Il log delle transazioni registra il nome del contrassegno, la descrizione, il database, l'utente, le informazioni di data/ora e il numero di sequenza del file di log (LSN). Le informazioni di data/ora sono utilizzate insieme al nome del contrassegno per identificare il contrassegno in modo univoco.  
  
 **Per creare transazioni contrassegnate in un set di database:**  
  
1.  Denominare la transazione nell'istruzione BEGIN TRAN e utilizzare la clausola WITH MARK  
  
     È possibile nidificare l'istruzione BEGIN TRAN *nuovo_nome_contrassegno* WITH MARK all'interno di una transazione esistente. Il valore di *nuovo_nome_contrassegno* è il nome di contrassegno per la transazione, anche se è dotata di un nome di transazione.  
  
    > [!NOTE]  
    >  Se si esegue una seconda istruzione nidificata BEGIN TRAN...WITH MARK, l'istruzione verrà ignorata ma provocherà un messaggio di avviso.  
  
2.  Eseguire un aggiornamento di tutti i database nel set.  
  
     Il contrassegno per una transazione specifica viene inserito solo nei log delle transazioni dell'istanza del server in cui viene eseguita l'istruzione BEGIN TRAN. Il contrassegno della transazione viene inserito nel log delle transazioni di ogni database aggiornato dalla transazione contrassegnata in tale istanza del server. Se il database si trova in istanze del server diverse, è necessario creare contrassegni identici in ogni istanza del server.  
  
### <a name="examples"></a>Esempi  
 Nell'esempio seguente viene ripristinato il log delle transazioni fino al contrassegno nella transazione contrassegnata denominata `ListPriceUpdate`.  
  
```sql  
USE AdventureWorks  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master  
GO  
  
RESTORE DATABASE AdventureWorks  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'ListPriceUpdate';  
```  
  
## <a name="forcing-a-mark-to-spread-to-other-servers"></a>Distribuzione forzata di un contrassegno in altri server  
 Il nome di un contrassegno di transazione non viene distribuito automaticamente in altri server se la transazione viene distribuita. Per forzare la distribuzione del contrassegno in altri server, è necessario scrivere una stored procedure contenente un'istruzione BEGIN TRAN *name* WITH MARK. Tale stored procedure deve quindi essere eseguita nel server remoto nell'ambito della transazione del server di origine.  
  
 Ad esempio, considerare un database partizionato esistente in più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In ogni istanza è presente un database denominato `coyote`. Creare innanzitutto una stored procedure in ogni database, ad esempio `sp_SetMark`.  
  
```sql  
CREATE PROCEDURE sp_SetMark  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION @name WITH MARK  
UPDATE coyote.dbo.Marks SET one = 1  
COMMIT TRANSACTION;  
GO  
```  
  
 Creare quindi una stored procedure `sp_MarkAll` contenente una transazione che inserisce un contrassegno in ogni database. `sp_MarkAll` può essere eseguita da qualsiasi istanza.  
  
```sql  
CREATE PROCEDURE sp_MarkAll  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION  
EXEC instance0.coyote.dbo.sp_SetMark @name  
EXEC instance1.coyote.dbo.sp_SetMark @name  
EXEC instance2.coyote.dbo.sp_SetMark @name  
COMMIT TRANSACTION;  
GO  
```  
  
### <a name="two-phase-commit"></a>commit in due fasi  
 L'esecuzione del commit di una transazione distribuita avviene in due fasi: la preparazione e il commit. Quando si esegue il commit di una transazione contrassegnata, il record di commit del log per ogni database interessato dalla transazione contrassegnata viene inserito nel log in un punto in cui non sono presenti transazioni in sospeso in nessuno dei log. In questo modo, si garantisce che non vi siano transazioni di cui è stato eseguito il commit in un log ma di cui non è stato eseguito il commit in un altro log.  
  
 I passaggi seguenti garantiscono questo risultato durante il commit di una transazione contrassegnata:  
  
1.  La fase di preparazione di una transazione contrassegnata blocca tutte le nuove operazioni di preparazione e commit.  
  
2.  È consentito il proseguimento solo delle operazioni di commit di transazioni già preparate.  
  
3.  La transazione contrassegnata attende quindi il completamento di tutte le transazioni preparate (con timeout).  
  
4.  La transazione contrassegnata viene preparata e quindi ne viene eseguito il commit.  
  
5.  Il blocco di nuove operazioni di preparazione e commit viene annullato.  
  
 I blocchi generati dalle transazioni contrassegnate che si estendono su più database possono rallentare le prestazioni di elaborazione delle transazioni nel server.  
  
 È consigliabile non eseguire transazioni contrassegnate simultanee. È raro ma possibile che il commit di una transazione contrassegnata distribuita generi un deadlock quando viene eseguito il commit simultaneo di altre transazioni contrassegnate distribuite. In tal caso, la transazione contrassegnata verrà scelta come oggetto del deadlock e ne verrà eseguito il rollback. Se si verifica questo errore, l'applicazione può ripetere il tentativo di esecuzione della transazione contrassegnata. Quando più transazioni contrassegnate tentano di eseguire il commit simultaneamente, la probabilità che venga generato un deadlock è maggiore.  
  
## <a name="recovering-to-a-marked-transaction"></a>Recupero fino a una transazione contrassegnata  
 Per informazioni su come recuperare un database che contiene transazioni contrassegnate fino a un contrassegno particolare o appena prima di esso, vedere [Recupero di database correlati che contengono transazioni contrassegnate](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md).  
  
## <a name="see-also"></a>Vedere anche  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [Backup e ripristino di database di sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [Applicare backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Recupero di database correlati che contengono transazioni contrassegnate](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
  
