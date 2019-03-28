---
title: sp_mergecleanupmetadata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergecleanupmetadata_TSQL
- sp_mergecleanupmetadata
helpviewer_keywords:
- sp_mergecleanupmetadata
ms.assetid: 892f8628-4cbe-4cc3-b959-ed45ffc24064
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6924ef36c57036cf6cad6e25a6dc5cebfa5fa5f2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529003"
---
# <a name="spmergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deve essere utilizzato solo nelle topologie di replica che includono server che eseguono versioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. **sp_mergecleanupmetadata** consente agli amministratori di pulizia dei metadati nel **MSmerge_genhistory**, **MSmerge_contents** e **MSmerge_tombstone** tabelle di sistema. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, il valore predefinito è **%**, che rimuove i metadati per tutte le pubblicazioni. Se viene specificata in modo esplicito, la pubblicazione deve essere esistente.  
  
`[ @reinitialize_subscriber = ] 'subscriber'` Specifica se reinizializzare il sottoscrittore. *Sottoscrittore* viene **nvarchar(5**, può essere **TRUE** oppure **FALSE**, il valore predefinito è **TRUE**. Se **TRUE**, le sottoscrizioni vengono contrassegnate per la reinizializzazione. Se **FALSE**, le sottoscrizioni non sono contrassegnate per la reinizializzazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_mergecleanupmetadata** deve essere utilizzato solo nelle topologie di replica che includono server che eseguono versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. Per le topologie in cui è incluso solo [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 o versioni successive, è consigliabile utilizzare la pulizia dei metadati basata sulla memorizzazione automatica. Quando si esegue questa stored procedure, è importante tenere presente che le dimensioni del file di log nel computer di esecuzione sono destinate ad aumentare, a volte in modo consistente.  
  
> [!CAUTION]
>  Dopo aver **sp_mergecleanupmetadata** viene eseguita, per impostazione predefinita, tutte le sottoscrizioni nei Sottoscrittori delle pubblicazioni che includono metadati archiviati nelle **MSmerge_genhistory**, **MSmerge_contents**  e **MSmerge_tombstone** sono contrassegnati per la reinizializzazione, eventuali modifiche in sospeso nel Sottoscrittore andranno perse e lo snapshot corrente è contrassegnato come obsoleto.  
> 
> [!NOTE]
>  Se sono presenti più pubblicazioni in un database e una di esse viene utilizzato un periodo di memorizzazione infinito (**@retention**=**0**), in esecuzione  **sp_mergecleanupmetadata** non la pulizia di metadati per il database di rilevamento delle modifiche merge della replica. È pertanto opportuno utilizzare il periodo di memorizzazione infinito con cautela.  
  
 Quando si esegue questa stored procedure, è possibile scegliere se reinizializzare i sottoscrittori impostando il **@reinitialize_subscriber** parametro **TRUE** (predefinito) o **FALSE**. Se **sp_mergecleanupmetadata** viene eseguita con il **@reinitialize_subscriber** parametro impostato su **TRUE**, uno snapshot verrà riapplicato al sottoscrittore anche se la sottoscrizione è stata creato senza uno snapshot (ad esempio, se i dati dello snapshot e lo schema sono stati applicati manualmente o esistevano già nel Sottoscrittore) iniziale. Impostazione del parametro su **FALSE** deve essere usata con cautela, poiché se la pubblicazione non viene reinizializzata è necessario assicurarsi che i dati nel server di pubblicazione e sottoscrittore sono sincronizzati.  
  
 Indipendentemente dal valore della **@reinitialize_subscriber**, **sp_mergecleanupmetadata** processi che siano tentando di caricare le modifiche in un server di pubblicazione o a un sottoscrittore di ripubblicazione di merge ha esito negativo se sono presenti in corso Quando che viene richiamata la stored procedure.  
  
 **Esecuzione di sp_mergecleanupmetadata con @reinitialize_subscriber = TRUE:**  
  
1.  È consigliabile, ma non richiesto, arrestare tutti gli aggiornamenti nei database di pubblicazione e sottoscrizione. Se l'esecuzione degli aggiornamenti continua, gli aggiornamenti effettuati in un Sottoscrizione dall'ultimo processo di tipo merge andranno perduti quando la pubblicazione viene reinizializzata. Viene tuttavia conservata la convergenza dei dati.  
  
2.  Eseguire un'operazione di merge tramite l'agente di merge. È consigliabile usare la **-convalidare** opzione della riga di comando dell'agente in ogni sottoscrittore quando si esegue l'agente di Merge. Se si eseguono operazioni di merge in modalità continua, vedere *considerazioni relative alla modalità continua unisce* più avanti in questa sezione.  
  
3.  Dopo aver completato tutte le unioni, eseguire **sp_mergecleanupmetadata**.  
  
4.  Eseguire **sp_reinitmergepullsubscription** su tutti i sottoscrittori con sottoscrizioni pull denominato o anonimo per garantire la convergenza dei dati.  
  
5.  Se si eseguono operazioni di merge in modalità continua, vedere *considerazioni relative alla modalità continua unisce* più avanti in questa sezione.  
  
6.  Rigenerare i file di snapshot per tutte le pubblicazioni di tipo merge a tutti i livelli. Se si tenta di eseguire il merge senza rigenerare prima lo snapshot, viene richiesto di rigenerare lo snapshot.  
  
7.  Eseguire il backup del database di pubblicazione. Se non si esegue questa operazione, dopo il ripristino del database di pubblicazione può verificarsi un errore del processo di merge.  
  
 **Esecuzione di sp_mergecleanupmetadata con @reinitialize_subscriber = FALSE:**  
  
1.  Arrestare **tutti** aggiornamenti al database di pubblicazione e sottoscrizione.  
  
2.  Eseguire un'operazione di merge tramite l'agente di merge. È consigliabile usare la **-convalidare** opzione della riga di comando dell'agente in ogni sottoscrittore quando si esegue l'agente di Merge. Se si eseguono operazioni di merge in modalità continua, vedere *considerazioni relative alla modalità continua unisce* più avanti in questa sezione.  
  
3.  Dopo aver completato tutte le unioni, eseguire **sp_mergecleanupmetadata**.  
  
4.  Se si eseguono operazioni di merge in modalità continua, vedere *considerazioni relative alla modalità continua unisce* più avanti in questa sezione.  
  
5.  Rigenerare i file di snapshot per tutte le pubblicazioni di tipo merge a tutti i livelli. Se si tenta di eseguire il merge senza rigenerare prima lo snapshot, viene richiesto di rigenerare lo snapshot.  
  
6.  Eseguire il backup del database di pubblicazione. Se non si esegue questa operazione, dopo il ripristino del database di pubblicazione può verificarsi un errore del processo di merge.  
  
 **Considerazioni speciali per merge in modalità continua**  
  
 In caso di esecuzione di operazioni di merge in modalità continua, è necessario eseguire una delle operazioni seguenti:  
  
-   Arrestare l'agente di Merge e quindi eseguire un'altra operazione di merge senza il **-continua** parametro specificato.  
  
-   Disattivare la pubblicazione tramite **sp_changemergepublication** per garantire che eventuali operazioni di merge in modalità continua che eseguono il polling dello stato della pubblicazione abbiano esito negativo.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Dopo aver completato passaggio3 Running **sp_mergecleanupmetadata**, riprendere merge in modalità continua basate sul modo in cui è stata arrestata. Eseguire una delle operazioni seguenti:  
  
-   Aggiungere il **-continua** parametro nuovamente per l'agente di Merge.  
  
-   Riattivare la pubblicazione con **sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_mergecleanupmetadata**.  
  
 Per utilizzare questa stored procedure, il server di pubblicazione deve eseguire [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. I sottoscrittori devono essere in esecuzione [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] oppure [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, Service Pack 2.  
  
## <a name="see-also"></a>Vedere anche  
 [MSmerge_genhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)   
 [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)   
 [MSmerge_tombstone &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
