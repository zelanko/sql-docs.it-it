---
title: sp_article_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: be3ccf8b0c85b61f536c381e4a42d1b5e37fbacf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62998269"
---
# <a name="sparticlevalidation-transact-sql"></a>sp_article_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inizializza una richiesta di convalida dei dati per l'articolo specificato. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione e nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_article_validation [ @publication = ] 'publication'  
    [ , [ @article = ] 'article' ]  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @subscription_level = ] subscription_level ]  
    [ , [ @reserved = ] reserved ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione in cui l'articolo esista. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'` È il nome dell'articolo da convalidare. *articolo* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @rowcount_only = ] type_of_check_requested` Specifica se il conteggio delle righe per la tabella viene restituito solo. *type_of_check_requested* viene **smallint**, il valore predefinito è **1**.  
  
 Se **0**, eseguire un conteggio delle righe e una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] checksum compatibile con 7.0.  
  
 Se **1**, eseguire solo un controllo di conteggio delle righe.  
  
 Se **2**, eseguire un conteggio delle righe e checksum binario.  
  
`[ @full_or_fast = ] full_or_fast` Il metodo consente di calcolare il conteggio delle righe. *full_or_fast* viene **tinyint**, i possibili valori sono i seguenti.  
  
|**Valore**|**Descrizione**|  
|---------------|---------------------|  
|**0**|Esegue un conteggio completo tramite COUNT(*).|  
|**1**|Esegue un conteggio rapido in **sysindexes**. Conteggio delle righe **sysindexes** è più veloce rispetto al conteggio delle righe nella tabella effettiva. Tuttavia **sysindexes** viene aggiornato in modo differito, e il conteggio delle righe potrebbe non essere accurata.|  
|**2** (impostazione predefinita)|Esegue un conteggio rapido condizionale eseguendo innanzitutto un tentativo con il metodo rapido. Se il metodo rapido evidenzia delle differenze, viene applicato il metodo completo. Se *expected_rowcount* è NULL e la stored procedure viene utilizzata per ottenere il valore, viene utilizzato sempre un Count (\*) completo.|  
  
`[ @shutdown_agent = ] shutdown_agent` Indica se l'agente di distribuzione viene interrotta immediatamente dopo il completamento della convalida. *shutdown_agent* viene **bit**, il valore predefinito è **0**. Se **0**, l'agente di distribuzione non viene arrestato. Se **1**, l'agente di distribuzione viene interrotta al termine della convalida dell'articolo.  
  
`[ @subscription_level = ] subscription_level` Indica se la convalida viene prelevata da un set di sottoscrittori. *subscription_level* viene **bit**, il valore predefinito è **0**. Se **0**, la convalida viene applicata a tutti i sottoscrittori. Se **1**, la convalida viene applicata solo a un subset dei sottoscrittori specificati tramite chiamate a **sp_marksubscriptionvalidation** nella transazione aperta corrente.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzata quando si richiede la convalida in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_article_validation** viene utilizzata nella replica transazionale.  
  
 **sp_article_validation** fa sì che le informazioni di convalida di sull'articolo specificato e invia una richiesta di convalida nel log delle transazioni. Quando l'agente di distribuzione riceve la richiesta, confronta le informazioni di convalida incluse nella richiesta con quelle della tabella del Sottoscrittore. I risultati della convalida vengono visualizzati negli avvisi di Monitoraggio replica e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="permissions"></a>Permissions  
 Solo gli utenti con autorizzazioni SELEZIONANO ALL nella tabella di origine per l'articolo in fase di convalida può eseguire **sp_article_validation**.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati replicati](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
