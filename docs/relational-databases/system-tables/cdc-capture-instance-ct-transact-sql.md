---
title: cdc.&lt;capture_instance&gt;_CT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc
- cdc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.<capture_instance>_CT
ms.assetid: 979c8110-3c54-4e76-953c-777194bc9751
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c4d6202e3ac68a1c1d36e307b9073ce23f1efb6e
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586380"
---
# <a name="cdcltcaptureinstancegtct-transact-sql"></a>cdc.&lt;capture_instance&gt;_CT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Tabella delle modiche creata quando Change Data Capture è abilitato in una tabella di origine. La tabella restituisce una riga per ogni operazione di inserimento ed eliminazione eseguita nella tabella di origine e due righe per ogni operazione di aggiornamento eseguita nella tabella di origine. Se non viene specificato al momento dell'abilitazione della tabella di origine, il nome della tabella delle modifiche viene derivato. Il formato del nome è cdc. *capture_instance*CT dove *capture_instance* è il nome dello schema della tabella di origine e il nome della tabella di origine nel formato *schema_table*. Ad esempio, se la tabella **Person. Address** nel **AdventureWorks** database di esempio è abilitato per change data capture, il nome della tabella modifiche derivato è **cdc. Person_Address_CT**.  
  
 È consigliabile che si **eseguono query direttamente le tabelle di sistema**. Eseguire invece i [CDC. fn_cdc_get_all_changes < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) e [CDC. fn_cdc_get_net_changes < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) funzioni.  
  

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|Numero di sequenza del file di log (LSN) associato alla transazione commit per la modifica.<br /><br /> Tutte le modifiche di cui è stato eseguito il commit nella stessa transazione condividono lo stesso valore LSN di commit. Ad esempio, se un'operazione di eliminazione nella tabella di origine rimuove due righe, la tabella delle modifiche conterrà due righe, ognuna con lo stesso **_ $start_lsn** valore.|  
|**__$end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] questa colonna è sempre a NULL.|  
|**__$seqval**|**binary(10)**|Valore di sequenza utilizzato per ordinare le modifiche a una riga all'interno di una transazione.|  
|**__$operation**|**int**|Identifica l'operazione DML (Data Manipulation Language) associata alla modifica. I possibili valori sono i seguenti:<br /><br /> 1 = eliminazione<br /><br /> 2 = inserimento<br /><br /> 3 = aggiornamento (valori obsoleti)<br /><br /> I dati della colonna includono valori di riga prima dell'esecuzione dell'istruzione di aggiornamento.<br /><br /> 4 = aggiornamento (valori nuovi)<br /><br /> I dati della colonna includono valori di riga dopo l'esecuzione dell'istruzione di aggiornamento.|  
|**__$update_mask**|**varbinary(128)**|Maschera di bit basata su numeri ordinali di colonna della tabella delle modifiche che identificano le colonne modificate.|  
|*\<colonne della tabella di origine acquisite>*|variabile|Le colonne rimanenti della tabella delle modifiche sono le colonne della tabella di origine identificate come colonne acquisite durante la creazione dell'istanza di acquisizione. Se non è stata specificata alcuna colonna nell'elenco delle colonne acquisite, tutte le colonne della tabella di origine vengono incluse in questa tabella.|  
|**__$command_id** |**int** |Registra l'ordine delle operazioni in una transazione. |  
  
## <a name="remarks"></a>Note  

Il `__$command_id` colonna è una colonna è stata introdotta in un aggiornamento cumulativo nelle versioni 2012 alla 2016. Per informazioni di versione e il download, vedere l'articolo 3030352 [FIX: La tabella delle modifiche è ordinata in modo non corretto per aggiornate righe dopo aver abilitato change data capture per un database Microsoft SQL Server](https://support.microsoft.com/help/3030352/fix-the-change-table-is-ordered-incorrectly-for-updated-rows-after-you).  Per altre informazioni, vedere [funzionalità CDC funzioni dopo l'aggiornamento cumulativo più recente per SQL Server 2012, 2014 e 2016](https://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/).

## <a name="captured-column-data-types"></a>Tipi di dati delle colonne acquisite  
 Le colonne acquisite incluse in questa tabella hanno lo stesso tipo di dati e valore delle corrispondenti colonne di origine, con le seguenti eccezioni:  
  
-   **Timestamp** colonne sono definite come **binari (8)** .  
  
-   **Identity** le colonne sono definite come **int** oppure **bigint**.  
  
 Tuttavia, i valori in queste colonne sono uguali ai valori della colonna di origine.  
  
### <a name="large-object-data-types"></a>Tipi di dati per oggetti di grandi dimensioni:  
 Colonne di tipo di dati **immagine**, **testo**, e **ntext** viene sempre assegnato un **NULL** valore quando _ $operation = 1 o \_ \_$operation = 3. Colonne di tipo di dati **varbinary (max)** , **varchar (max)** , o **nvarchar (max)** vengono assegnati un **NULL** valore quando \_ \_$operation = 3, a meno che le colonne modificate durante l'aggiornamento. Quando \_ \_$operation = 1, queste colonne vengono assegnate i rispettivi valori al momento dell'eliminazione. Le colonne calcolate sono sempre inclusi in un'istanza di acquisizione hanno un valore pari **NULL**.  
  
 Per impostazione predefinita, la dimensione massima che può essere aggiunta a una colonna acquista in una singola istruzione INSERT, UPDATE, WRITETEXT o UPDATETEXT è pari a 65.536 byte o 64 KB Per aumentare questa dimensione per supportare i dati LOB di maggiori dimensioni, usare il [configurare l'opzione di configurazione del Server max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md) per specificare una dimensione massima più grande. Per altre informazioni, vedere [Configurare l'opzione di configurazione del server max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md).  
  
## <a name="data-definition-language-modifications"></a>Modifiche DDL  
 Le modifiche DDL alla tabella di origine, ad esempio aggiunta o eliminazione di colonne, vengono registrate nella [ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) tabella. Queste modifiche non sono applicate alla tabella delle modifiche, ossia la definizione della tabella delle modifiche rimane costante. Nel caso di inserimento di righe nella tabella delle modifiche, il processo di acquisizione ignora le colonne che non sono visualizzate nell'elenco di colonne acquisite associate alla tabella di origine. Se una colonna è visualizzata nell'elenco di colonne acquisite che non compare più nella tabella di origine, alla colonna viene assegnato un valore Null.  
  
 Modifica il tipo di dati di una colonna nella tabella di origine verrà inoltre registrata il [ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) tabella. Tuttavia, questa modifica non altera la definizione della tabella delle modifiche. Il tipo di dati della colonna acquisita nella tabella delle modifiche viene modificato quando il processo di acquisizione incontra il record del log per la modifica DDL apportata alla tabella di origine.  
  
 Se è necessario modificare il tipo di dati di una colonna acquisita nella tabella di origine in una modalità che decresce la dimensione del tipo di dati, utilizzare la procedura descritta di seguito per assicurasi che la colonna equivalente nella tabella delle modifiche possa essere modificata correttamente.  
  
1.  Nella tabella di origine, aggiornare i valori nella colonna da modificare per adattarli nella dimensione del tipo di dati pianificata. Ad esempio, se si modifica il tipo di dati da **int** al **smallint**, aggiornare i valori a una dimensione che rientra nel **smallint** compresi, tra-32.768 e 32.767.  
  
2.  Nella tabella delle modifiche, eseguire la stessa operazione di aggiornamento alla colonna equivalente.  
  
3.  Modificare la tabella di origine specificando il nuovo tipo di dati. La modifica del tipo di dati è propagata correttamente alla tabella delle modifiche.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="data-manipulation-language-modifications"></a>Modifiche DML  
 Quando su una tabella di origine abilitata per Change Data Capture vengono eseguite operazioni di inserimento, aggiornamento ed eliminazione, nel log delle transazioni del database viene visualizzato un record relativo a tali operazioni DML. Il processo change data capture recupera le informazioni su tali modifiche dal log delle transazioni e aggiunge uno o due righe alla tabella delle modifiche per registrare la modifica. Le voci vengono aggiunte alla tabella delle modifiche nello stesso ordine in cui è stato eseguito il relativo commit nella tabella di origine, anche se il commit delle voci della tabella delle modifiche deve essere eseguito in genere per un gruppo di modifiche anziché per una voce singola.  
  
 Entro la voce della tabella di modifica, la **_ $start_lsn** colonna viene utilizzata per registrare il LSN associato per la tabella di origine, la modifica di commit e il **colonna _ $seqval** viene utilizzata per ordinare la modifica all'interno la transazione. Nel loro complesso queste colonne di metadati possono essere utilizzate per garantire che venga mantenuto l'ordine di commit delle modifiche di origine. Poiché il processo di acquisizione ottiene le informazioni relative alle modifiche dal log delle transazioni, è importante notare che le voci della tabella delle modifiche non vengono visualizzate in modo sincrono con le modifiche della tabella di origine corrispondenti. Al contrario, le modifiche corrispondenti vengono visualizzate in modo asincrono dopo che il processo di acquisizione ha elaborato le voci di modifica attinenti dal log delle transazioni.  
  
 Per le operazioni di inserimento ed eliminazione, sono impostati tutti i bit della maschera di aggiornamento. Per le operazioni di aggiornamento, la maschera di aggiornamento sia nelle vecchie righe aggiornate obsolete che nelle righe di nuovo aggiornamento sarà modificata per riflettere le colonne modificate durante l'aggiornamento.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)  
  
  
