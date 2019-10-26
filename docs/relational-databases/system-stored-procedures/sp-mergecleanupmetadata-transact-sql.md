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
ms.openlocfilehash: 0196993f863d973e14834f7eb3b93b797a825ac4
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907330"
---
# <a name="sp_mergecleanupmetadata-transact-sql"></a>sp_mergecleanupmetadata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deve essere utilizzato solo nelle topologie di replica che includono server che eseguono versioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. **sp_mergecleanupmetadata** consente agli amministratori di eliminare i metadati nelle tabelle di sistema **MSmerge_genhistory**, **MSmerge_contents** e **MSmerge_tombstone** . Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_mergecleanupmetadata [ [ @publication = ] 'publication' ]  
    [ , [ @reinitialize_subscriber = ] 'reinitialize_subscriber' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` è il nome della pubblicazione. *Publication* è di **tipo sysname**e il valore predefinito è **%** , che consente di pulire i metadati per tutte le pubblicazioni. Se viene specificata in modo esplicito, la pubblicazione deve essere esistente.  
  
`[ @reinitialize_subscriber = ] 'subscriber'` specifica se reinizializzare il Sottoscrittore. *Subscriber* è **di tipo nvarchar (5)** . può essere **true** o **false**e il valore predefinito è **true**. Se **true**, le sottoscrizioni vengono contrassegnate per la reinizializzazione. Se **false**, le sottoscrizioni non vengono contrassegnate per la reinizializzazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Remarks  
 **sp_mergecleanupmetadata** deve essere utilizzato solo nelle topologie di replica che includono server che eseguono versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1. Per le topologie in cui è incluso solo [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 1 o versioni successive, è consigliabile utilizzare la pulizia dei metadati basata sulla memorizzazione automatica. Quando si esegue questa stored procedure, è importante tenere presente che le dimensioni del file di log nel computer di esecuzione sono destinate ad aumentare, a volte in modo consistente.  
  
> [!CAUTION]
>  Dopo l'esecuzione di **sp_mergecleanupmetadata** , per impostazione predefinita tutte le sottoscrizioni dei sottoscrittori di pubblicazioni che contengono metadati archiviati in **MSmerge_genhistory**, **MSmerge_contents** e **MSmerge_tombstone** sono contrassegnate per la reinizializzazione, le eventuali modifiche in sospeso nel Sottoscrittore vengono perse e lo snapshot corrente è contrassegnato come obsoleto.  
> 
> [!NOTE]
>  Se sono presenti più pubblicazioni in un database e una di queste pubblicazioni utilizza un periodo di conservazione di pubblicazione infinito ( **\@conservazione**=**0**), l'esecuzione di **sp_mergecleanupmetadata** non comporta la pulizia del merge metadati del rilevamento delle modifiche della replica per il database. È pertanto opportuno utilizzare il periodo di memorizzazione infinito con cautela.  
  
 Quando si esegue questa stored procedure, è possibile scegliere se reinizializzare i Sottoscrittori impostando il parametro **\@reinitialize_subscriber** su **true** (impostazione predefinita) o **false**. Se **sp_mergecleanupmetadata** viene eseguita con il parametro **\@Reinitialize_subscriber** impostato su **true**, viene riapplicato uno snapshot nel Sottoscrittore anche se la sottoscrizione è stata creata senza uno snapshot iniziale, ad esempio se lo schema e i dati dello snapshot sono stati applicati manualmente o sono già presenti nel Sottoscrittore. L'impostazione del parametro su **false** deve essere utilizzata con cautela, perché se la pubblicazione non viene reinizializzata, è necessario assicurarsi che i dati nel server di pubblicazione e nel Sottoscrittore siano sincronizzati.  
  
 Indipendentemente dal valore di **\@reinitialize_subscriber**, **sp_mergecleanupmetadata** ha esito negativo se sono presenti processi di merge in corso che tentano di caricare le modifiche in un server di pubblicazione o in un Sottoscrittore di ripubblicazione al momento dell'archiviazione viene richiamata la procedura.  
  
 **Esecuzione di sp_mergecleanupmetadata con \@reinitialize_subscriber = TRUE:**  
  
1.  È consigliabile, ma non richiesto, arrestare tutti gli aggiornamenti nei database di pubblicazione e sottoscrizione. Se l'esecuzione degli aggiornamenti continua, gli aggiornamenti effettuati in un Sottoscrizione dall'ultimo processo di tipo merge andranno perduti quando la pubblicazione viene reinizializzata. Viene tuttavia conservata la convergenza dei dati.  
  
2.  Eseguire un'operazione di merge tramite l'agente di merge. Si consiglia di utilizzare l'opzione della riga di comando **-Validate** Agent in ogni Sottoscrittore quando si esegue il agente di merge. Se si eseguono operazioni di merge in modalità continua, vedere *considerazioni speciali per le operazioni di merge in modalità continua* più avanti in questa sezione.  
  
3.  Al termine di tutte le unioni, eseguire **sp_mergecleanupmetadata**.  
  
4.  Eseguire **sp_reinitmergepullsubscription** in tutti i Sottoscrittori che utilizzano una sottoscrizione pull denominata o anonima per garantire la convergenza dei dati.  
  
5.  Se si eseguono operazioni di merge in modalità continua, vedere *considerazioni speciali per le operazioni di merge in modalità continua* più avanti in questa sezione.  
  
6.  Rigenerare i file di snapshot per tutte le pubblicazioni di tipo merge a tutti i livelli. Se si tenta di eseguire il merge senza rigenerare prima lo snapshot, viene richiesto di rigenerare lo snapshot.  
  
7.  Eseguire il backup del database di pubblicazione. Se non si esegue questa operazione, dopo il ripristino del database di pubblicazione può verificarsi un errore del processo di merge.  
  
 **Esecuzione di sp_mergecleanupmetadata con \@reinitialize_subscriber = FALSE:**  
  
1.  Arrestare **tutti** gli aggiornamenti ai database di pubblicazione e sottoscrizione.  
  
2.  Eseguire un'operazione di merge tramite l'agente di merge. Si consiglia di utilizzare l'opzione della riga di comando **-Validate** Agent in ogni Sottoscrittore quando si esegue il agente di merge. Se si eseguono operazioni di merge in modalità continua, vedere *considerazioni speciali per le operazioni di merge in modalità continua* più avanti in questa sezione.  
  
3.  Al termine di tutte le unioni, eseguire **sp_mergecleanupmetadata**.  
  
4.  Se si eseguono operazioni di merge in modalità continua, vedere *considerazioni speciali per le operazioni di merge in modalità continua* più avanti in questa sezione.  
  
5.  Rigenerare i file di snapshot per tutte le pubblicazioni di tipo merge a tutti i livelli. Se si tenta di eseguire il merge senza rigenerare prima lo snapshot, viene richiesto di rigenerare lo snapshot.  
  
6.  Eseguire il backup del database di pubblicazione. Se non si esegue questa operazione, dopo il ripristino del database di pubblicazione può verificarsi un errore del processo di merge.  

 **Considerazioni speciali per i merge in modalità continua**  
  
 In caso di esecuzione di operazioni di merge in modalità continua, è necessario eseguire una delle operazioni seguenti:  
  
-   Arrestare il agente di merge, quindi eseguire un'altra operazione di merge senza il parametro **-Continuous** specificato.  
  
-   Disattivare la pubblicazione con **sp_changemergepublication** per assicurarsi che le unioni in modalità continua che eseguono il polling dello stato della pubblicazione abbiano esito negativo.  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'inactive'  
    ```  
  
 Dopo aver completato il passaggio 3 dell'esecuzione di **sp_mergecleanupmetadata**, riprendere le operazioni di merge in modalità continua in base alla modalità di interruzione. Eseguire una delle operazioni seguenti:  
  
-   Aggiungere di nuovo il parametro **-Continuous** per la agente di merge.  
  
-   Riattivare la pubblicazione con **sp_changemergepublication.**  
  
    ```  
    EXEC central..sp_changemergepublication @publication = 'dynpart_pubn', @property = 'status', @value = 'active'  
    ```  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_mergecleanupmetadata**.  
  
 Per utilizzare questa stored procedure, il server di pubblicazione deve eseguire [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. È necessario che nei Sottoscrittori sia in esecuzione [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7,0, Service Pack 2.  
  
## <a name="see-also"></a>Vedere anche  
 [ &#40;Transact-SQL&#41; MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)  
 [ &#40;Transact-SQL&#41; MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)  
 [Transact &#40;-SQL MSmerge_tombstone&#41;](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)  
  
  
