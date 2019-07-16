---
title: sp_changesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- changesubscription
- sp_changesubscription
- changesubscription_TSQL
- sp_changesubscription_TSQL
helpviewer_keywords:
- sp_changesubscription
ms.assetid: f9d91fe3-47cf-4915-b6bf-14c9c3d8a029
author: stevestein
ms.author: sstein
ms.openlocfilehash: cddc14c14054ecfa81a963d15a7a604e8d71d085
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016543"
---
# <a name="spchangesubscription-transact-sql"></a>sp_changesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le proprietà di una sottoscrizione pull o push transazionale o snapshot coinvolta in una replica transazionale ad aggiornamento in coda. Per modificare le proprietà di tutti gli altri tipi di sottoscrizioni pull, utilizzare [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md). **sp_changesubscription** viene eseguito nel server di pubblicazione nel database di pubblicazione.  
  
> [!IMPORTANT]  
>  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changesubscription [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione da modificare. *pubblicazione*viene **sysname**, non prevede alcun valore predefinito  
  
`[ @article = ] 'article'` È il nome dell'articolo da modificare. *articolo* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @destination_db = ] 'destination_db'` È il nome del database di sottoscrizione. *destination_db* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @property = ] 'property'` È la proprietà da modificare per la sottoscrizione specificata. *proprietà* viene **nvarchar(30)** , e può essere uno dei valori nella tabella.  
  
`[ @value = ] 'value'` Nuovo valore per l'oggetto specificato *proprietà*. *valore* viene **nvarchar (4000)** , e può essere uno dei valori nella tabella.  
  
|Proprietà|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Account di accesso per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione dell'agente.|  
|**distrib_job_password**||Password dell'account di Windows utilizzato per l'esecuzione dell'agente.|  
|**subscriber_catalog**||Catalogo da utilizzare per stabilire una connessione al provider OLE DB Questa proprietà è valida solo per non -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.|  
|**subscriber_datasource**||Nome dell'origine dei dati riconosciuto dal provider OLE DB. *Questa proprietà è valida solo per non -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *sottoscrittori.*|  
|**subscriber_location**||Percorso del database riconosciuto dal provider OLE DB. *Questa proprietà è valida solo per non -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *sottoscrittori.*|  
|**subscriber_login**||Nome dell'account di accesso nel Sottoscrittore.|  
|**subscriber_password**||Password complessa per l'account di accesso fornito.|  
|**subscriber_security_mode**|**1**|Esegue la connessione al Sottoscrittore utilizzando l'autenticazione di Windows.|  
||**0**|Esegue la connessione al Sottoscrittore utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**subscriber_provider**||ProgID univoco con il quale viene registrato il provider OLE DB per l'origine dei dati non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Questa proprietà è valida solo per non -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *sottoscrittori.*|  
|**subscriber_providerstring**||Stringa di connessione specifica del provider OLE DB che identifica l'origine dei dati. *Questa proprietà è valida solo per non -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *sottoscrittori.*|  
|**subscriptionstreams**||Numero di connessioni consentite per agente di distribuzione per l'applicazione di batch di modifiche in parallelo a un Sottoscrittore. Un intervallo di valori da **1** al **64** è supportata per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione. Questa proprietà deve essere **0** per non -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori, server di pubblicazione Oracle o sottoscrizioni peer-to-peer.|  
|**subscriber_type**|**1**|Server dell'origine dei dati ODBC.|  
||**3**|Provider OLE DB|  
|**memory_optimized**|**bit**|Indica che la sottoscrizione supporta le tabelle ottimizzate per la memoria. *memory_optimized* viene **bit**, dove 1 è uguale a true (la sottoscrizione supporta le tabelle ottimizzate per la memoria).|  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere specificato per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changesubscription** viene utilizzata nella replica snapshot e transazionale.  
  
 **sp_changesubscription** utilizzabile solo per modificare le proprietà delle sottoscrizioni push o pull coinvolte nella coda di replica transazionale ad aggiornamento. Per modificare le proprietà di tutti gli altri tipi di sottoscrizioni pull, utilizzare [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md).  
  
 Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_changesubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
