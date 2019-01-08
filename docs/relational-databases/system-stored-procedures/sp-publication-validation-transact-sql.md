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
manager: craigg
ms.openlocfilehash: 8612b3713113435461ca59845710b9f7284f1a78
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591405"
---
# <a name="sppublicationvalidation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inizializza una richiesta di convalida per ogni articolo nella pubblicazione specificata. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [**@publication=**] **'**_pubblicazione '_  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [**@rowcount_only=**] *rowcount_only*  
 Indica se restituire solo il conteggio delle righe per la tabella. *rowcount_only* viene **smallint** e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Esegue un checksum compatibile con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.<br /><br /> Nota: Quando a un articolo è applicato un filtro orizzontale, viene eseguita un'operazione di conteggio delle righe anziché di checksum.|  
|**1** (impostazione predefinita)|Esegue solo la convalida mediante conteggio delle righe.|  
|**2**|Esegue la convalida mediante conteggio delle righe e checksum binario.<br /><br /> Nota: Per i Sottoscrittori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 7.0, viene eseguita solo la convalida con conteggio delle righe.|  
  
 [**@full_or_fast=**] *full_or_fast*  
 Metodo utilizzato per il conteggio delle righe. *full_or_fast* viene **tinyint** e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Esegue un conteggio completo con COUNT(*).|  
|**1**|Un conteggio rapido in **sysindexes**. Conteggio delle righe [sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) è molto più veloce rispetto al conteggio delle righe nella tabella effettiva. Tuttavia, poiché [sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) in modalità differita è aggiornato, il conteggio delle righe potrebbe non essere accurata.|  
|**2** (impostazione predefinita)|Esegue un conteggio rapido condizionale eseguendo innanzitutto un tentativo con il metodo rapido. Se il metodo rapido evidenzia delle differenze, viene applicato il metodo completo. Se *expected_rowcount* è NULL e la stored procedure viene utilizzata per ottenere il valore, viene utilizzato sempre un Count (\*) completo.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 Indica se l'agente di distribuzione deve essere chiuso immediatamente dopo il completamento della convalida. *shutdown_agent* viene **bit**, il valore predefinito è **0**. Se **0**, l'agente di replica non viene arrestato. Se **1**, l'agente di replica viene chiuso al termine della convalida dell'ultimo articolo.  
  
 [ **@publisher** =] **'**_editore_**'**  
 Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzata quando si richiede la convalida in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_publication_validation** viene utilizzata nella replica transazionale.  
  
 **sp_publication_validation** può essere chiamato in qualsiasi momento dopo gli articoli associati alla pubblicazione sono stati attivati. Questa procedura può essere eseguita in modo manuale una sola volta oppure nell'ambito di un processo con pianificazione periodica per la convalida dei dati.  
  
 Se l'applicazione include sottoscrittori ad aggiornamento immediato **sp_publication_validation** rilevi errori. **sp_publication_validation** Calcola prima del conteggio delle righe o del checksum nel server di pubblicazione e quindi nel Sottoscrittore. Dato che il trigger per l'aggiornamento immediato può propagare un aggiornamento dal Sottoscrittore al server di pubblicazione dopo l'esecuzione del conteggio delle righe o del checksum nel server di pubblicazione ma prima del completamento di queste operazioni nel Sottoscrittore, i valori potrebbero cambiare. Per assicurarsi che i valori nel Sottoscrittore e nel server di pubblicazione non vengano modificati durante la convalida di una pubblicazione, arrestare il servizio Microsoft Distributed Transaction Coordinator (MS DTC) nel server di pubblicazione durante l'operazione di convalida.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_publication_validation**.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati nel Sottoscrittore](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
