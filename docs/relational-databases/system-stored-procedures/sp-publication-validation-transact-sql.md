---
title: sp_publication_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: stevestein
ms.author: sstein
ms.openlocfilehash: bdfe70e3df86f792d250cd7abcc3ef3013e9df19
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056228"
---
# <a name="sp_publication_validation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Inizializza una richiesta di convalida per ogni articolo nella pubblicazione specificata. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` è il nome della pubblicazione. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @rowcount_only = ] 'rowcount_only'` indica se restituire solo il conteggio delle righe per la tabella. *rowcount_only* è di **smallint** . i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**0**|Esegue un checksum compatibile con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.<br /><br /> Nota: quando un articolo viene filtrato orizzontalmente, viene eseguita un'operazione di conteggio delle righe anziché un'operazione di checksum.|  
|**1** (impostazione predefinita)|Esegue solo la convalida mediante conteggio delle righe.|  
|**2**|Esegue la convalida mediante conteggio delle righe e checksum binario.<br /><br /> Nota: per i sottoscrittori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 7,0, viene eseguita solo una convalida con conteggio delle righe.|  
  
`[ @full_or_fast = ] 'full_or_fast'` è il metodo utilizzato per calcolare il conteggio delle righe. *full_or_fast* è di **tinyint** . i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**0**|Esegue un conteggio completo con COUNT(*).|  
|**1**|Esegue un conteggio rapido da **sysindexes. Rows**. Il conteggio delle righe in [sys. sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) è molto più rapido rispetto al conteggio delle righe nella tabella effettiva. Tuttavia, poiché [sys. sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) viene aggiornato in modo differito, il conteggio delle righe potrebbe non essere accurato.|  
|**2** (impostazione predefinita)|Esegue un conteggio rapido condizionale eseguendo innanzitutto un tentativo con il metodo rapido. Se il metodo rapido evidenzia delle differenze, viene applicato il metodo completo. Se *expected_rowcount* è NULL e la stored procedure viene utilizzata per ottenere il valore, viene utilizzato sempre un Count (\*) completo.|  
  
`[ @shutdown_agent = ] 'shutdown_agent'` indica se il agente di distribuzione deve essere arrestato immediatamente dopo il completamento della convalida. *shutdown_agent* è di **bit**e il valore predefinito è **0**. Se è **0**, l'agente di replica non viene arrestato. Se è **1**, l'agente di replica si arresta dopo la convalida dell'ultimo articolo.  
  
`[ @publisher = ] 'publisher'` specifica un server di pubblicazione non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* è di **tipo sysname**e il valore predefinito è null.  
  
> [!NOTE]  
>  il *server di pubblicazione* non deve essere utilizzato quando viene richiesta la convalida in un server di pubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_publication_validation** viene utilizzata nella replica transazionale.  
  
 **sp_publication_validation** possibile chiamare in qualsiasi momento dopo l'attivazione degli articoli associati alla pubblicazione. Questa procedura può essere eseguita in modo manuale una sola volta oppure nell'ambito di un processo con pianificazione periodica per la convalida dei dati.  
  
 Se l'applicazione dispone di Sottoscrittori ad aggiornamento immediato, **sp_publication_validation** possibile rilevare errori non corretti. **sp_publication_validation** calcola innanzitutto il conteggio delle righe o il checksum nel server di pubblicazione e quindi nel Sottoscrittore. Dato che il trigger per l'aggiornamento immediato può propagare un aggiornamento dal Sottoscrittore al server di pubblicazione dopo l'esecuzione del conteggio delle righe o del checksum nel server di pubblicazione ma prima del completamento di queste operazioni nel Sottoscrittore, i valori potrebbero cambiare. Per assicurarsi che i valori nel Sottoscrittore e nel server di pubblicazione non vengano modificati durante la convalida di una pubblicazione, arrestare il servizio Microsoft Distributed Transaction Coordinator (MS DTC) nel server di pubblicazione durante l'operazione di convalida.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_publication_validation**.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati nel Sottoscrittore](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
