---
title: Pubblicazione dell'esecuzione delle stored procedure nella replica transazionale | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], stored procedures and
- transactional replication, publishing stored procedure execution
ms.assetid: f4686f6f-c224-4f07-a7cb-92f4dd483158
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 25aa20472daec1e20113627b4cbd778dfa142002
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769326"
---
# <a name="publishing-stored-procedure-execution-in-transactional-replication"></a>Pubblicazione dell'esecuzione delle stored procedure nella replica transazionale
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Se una o più stored procedure vengono eseguite nel server di pubblicazione e influiscono su tabelle pubblicate, è possibile includerle nella pubblicazione sotto forma di articoli di esecuzione delle stored procedure. La definizione della procedura, ovvero l'istruzione CREATE PROCEDURE, viene replicata nel Sottoscrittore durante l'inizializzazione della sottoscrizione. Quando la procedura viene eseguita nel server di pubblicazione, la replica esegue la procedura corrispondente nel Sottoscrittore. Ciò può migliorare sensibilmente le prestazioni, ad esempio nel caso di operazioni batch di grandi dimensioni, poiché viene replicata solo l'esecuzione della procedura senza necessità di replicare le singole modifiche di ogni riga. Si supponga, ad esempio, di creare la stored procedure seguente nel database di pubblicazione:  
  
```  
CREATE PROC give_raise AS  
UPDATE EMPLOYEES SET salary = salary * 1.10  
```  
  
 La stored procedure assegna a ognuno dei 10.000 dipendenti della società un aumento di stipendio del 10%. Quando si esegue la stored procedure nel server di pubblicazione, viene aggiornato lo stipendio di ogni dipendente. Senza la replica dell'esecuzione della stored procedure, l'aggiornamento verrebbe inviato ai Sottoscrittori sotto forma di transazione multipla di grandi dimensioni:  
  
```  
BEGIN TRAN  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 1'  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 2'  
```  
  
 La stessa riga di codice viene eseguita per ognuno dei 10.000 dipendenti.  
  
 Tramite la replica dell'esecuzione della stored procedure, viene inviato solo il comando di esecuzione della stored procedure nel Sottoscrittore, anziché scrivere tutti gli aggiornamenti nel database di distribuzione e inviarli in rete al Sottoscrittore.  
  
```  
EXEC give_raise  
```  
  
> [!IMPORTANT]  
>  La replica delle stored procedure non è adatta a tutte le applicazioni. Se in seguito all'applicazione di un filtro orizzontale a un articolo il server di pubblicazione include set di righe diversi rispetto al Sottoscrittore, l'esecuzione della stessa stored procedure nei due server restituisce risultati diversi. In modo analogo, se un aggiornamento è basato su una sottoquery di un'altra tabella non replicata, l'esecuzione della stessa stored procedure nel server di pubblicazione e nel Sottoscrittore restituisce risultati diversi.  
  
 **Per pubblicare l'esecuzione di una stored procedure**  
  
-   SQL Server Management Studio: [Pubblicare l'esecuzione di una stored procedure in una pubblicazione transazionale &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
-   Programmazione Transact-SQL della replica: eseguire [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) e specificare un valore 'serializable proc exec' (consigliato) o 'proc exec' per il parametro **@type** . Per altre informazioni sulla definizione degli articoli, vedere [Definire un articolo](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="modifying-the-procedure-at-the-subscriber"></a>Modifica della procedura nel Sottoscrittore  
 Per impostazione predefinita, la definizione della stored procedure nel server di pubblicazione viene distribuita in ogni Sottoscrittore. È comunque possibile modificare la stored procedure anche nel Sottoscrittore. Ciò risulta utile se nel Sottoscrittore si desidera eseguire logica diversa da quella eseguita nel server di pubblicazione. Si supponga, ad esempio, che la stored procedure **sp_big_delete**nel server di pubblicazione svolga due funzioni, ovvero elimini 1.000.000 di righe dalla tabella replicata **big_table1** e aggiorni la tabella non replicata **big_table2**. In questo caso, per ridurre la quantità di risorse di rete utilizzate, è necessario distribuire l'eliminazione del milione di righe come stored procedure pubblicando **sp_big_delete**. Nel Sottoscrittore è possibile modificare **sp_big_delete** in modo che esegua l'eliminazione delle righe, ma non l'aggiornamento successivo di **big_table2**.  
  
> [!NOTE]  
>  Per impostazione predefinita tutte le modifiche apportate nel server di pubblicazione utilizzando ALTER PROCEDURE vengono distribuite nel Sottoscrittore. Per impedire questa operazione, disabilitare la distribuzione delle modifiche dello schema prima di eseguire ALTER PROCEDURE. Per informazioni sulle modifiche dello schema, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="types-of-stored-procedure-execution-articles"></a>Tipi di articoli di esecuzione delle stored procedure  
 L'esecuzione di una stored procedure può essere pubblicata in due modi diversi, ovvero sotto forma di articolo di esecuzione delle procedure serializzabili e sotto forma di articolo di esecuzione delle procedure.  
  
-   È consigliabile utilizzare l'opzione serializzabile poiché esegue la replica dell'esecuzione della procedura solo se la procedura viene eseguita nel contesto di una transazione serializzabile. Se viene eseguita in un contesto diverso, le modifiche ai dati delle tabelle pubblicate vengono replicate come una serie di istruzioni DML. In questo modo i dati nel Sottoscrittore risultano sempre consistenti con i dati nel server di pubblicazione. Questo risulta particolarmente utile per le operazioni batch, ad esempio operazioni di pulizia dei riferimenti molto estese.  
  
-   Con l'opzione di esecuzione della procedura, è possibile che l'esecuzione sia stata replicata in tutti i Sottoscrittori, indipendentemente dal fatto che le singole istruzioni nella stored procedure abbiano avuto o meno esito positivo. Inoltre, poiché le modifiche ai dati apportate dalla stored procedure possono essere presenti in più transazioni, i dati nei Sottoscrittori potrebbero essere incoerenti con i dati nel server di pubblicazione. Per risolvere questi problemi, è necessario che i Sottoscrittori siano di sola lettura e che si utilizzi un livello di isolamento maggiore di Read Uncommitted. Se si utilizza Read Uncommitted, le modifiche ai dati nelle tabelle pubblicate vengono replicate come una serie di istruzioni DML.  
  
 Nell'esempio seguente viene illustrato il motivo per cui è consigliabile impostare la replica delle procedure sotto forma di articoli di procedure serializzabili.  
  
```  
BEGIN TRANSACTION T1  
SELECT @var = max(col1) FROM tableA  
UPDATE tableA SET col2 = <value>   
   WHERE col1 = @var   
  
BEGIN TRANSACTION T2  
INSERT tableA VALUES <values>  
COMMIT TRANSACTION T2  
```  
  
 Nell'esempio precedente si presuppone che l'istruzione SELECT della transazione T1 venga eseguita prima dell'istruzione INSERT della transazione T2.  
  
 Se la procedura non viene eseguita nell'ambito di una transazione serializzabile, ad esempio con il livello di isolamento impostato su SERIALIZABLE, la transazione T2 potrà inserire una nuova riga nell'intervallo dell'istruzione SELECT della transazione T1. Inoltre il commit della transazione T2 verrà eseguito prima di quello della transazione T1. Questo significa infine che T2 verrà applicata nel Sottoscrittore prima di T1. Quando T1 viene applicata nel Sottoscrittore, è possibile che l'istruzione SELECT restituisca un valore diverso di quello presente nel server di pubblicazione e che si ottenga un risultato diverso dall'istruzione UPDATE.  
  
 Se la procedura viene eseguita nell'ambito di una transazione serializzabile, la transazione T2 non potrà eseguire inserimenti nell'intervallo dell'istruzione SELECT di T2, ma rimarrà bloccata fino al commit di T1 in modo da garantire gli stessi risultati nel Sottoscrittore.  
  
 I blocchi verranno mantenuti più a lungo se si esegue la procedura in una transazione serializzabile e possono comportare una riduzione della concorrenza.  
  
## <a name="the-xactabort-setting"></a>Impostazione XACT_ABORT  
 Durante la replica dell'esecuzione della stored procedure, l'impostazione XACT_ABORT della sessione nella quale avviene l'esecuzione della stored procedure deve essere impostata su ON. Se XACT_ABORT è impostata su OFF, durante l'esecuzione della procedura nel server di pubblicazione viene generato un errore, che si ripeterà anche nel Sottoscrittore, interrompendo l'attività dell'agente di distribuzione. Se si imposta XACT_ABORT su ON, per tutti gli errori rilevati durante l'esecuzione nel server di pubblicazione viene eseguito il rollback dell'intera esecuzione, il che impedisce che si verifichino errori nell'agente di distribuzione. Per altre informazioni sull'impostazione XACT_ABORT, vedere [SET XACT_ABORT &#40;Transact-SQL&#41;](../../../t-sql/statements/set-xact-abort-transact-sql.md).  
  
 Se è necessario impostare XACT_ABORT su OFF, specificare il parametro **-SkipErrors** per l'agente di distribuzione. Ciò consente all'agente di continuare ad applicare eventuali modifiche nel Sottoscrittore anche in caso di errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
