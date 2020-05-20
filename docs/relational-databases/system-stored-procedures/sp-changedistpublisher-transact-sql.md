---
title: sp_changedistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fb90ec6a3d5413d22f4721491d3b151a7e28ac05
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833432"
---
# <a name="sp_changedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Modifica le proprietà del server di pubblicazione della distribuzione. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'`Nome del server di pubblicazione. *Publisher* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @property = ] 'property'`Proprietà da modificare per il server di pubblicazione specificato. *Property* è di **tipo sysname** . i possibili valori sono i seguenti.  
  
`[ @value = ] 'value'`Valore per la proprietà specificata. *value* è di **tipo nvarchar (255)** e il valore predefinito è null.  
  
`[ @storage_connection_string = ] 'storage_connection_string'`È obbligatorio per istanza gestita di database SQL, deve corrispondere alla chiave di accesso per il volume di archiviazione del database SQL di Azure. 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 Nella tabella seguente vengono descritte le proprietà valide dei server di pubblicazione e i valori corrispondenti.  
  
|Proprietà|Valori|Descrizione|  
|--------------|------------|-----------------|  
|**active**|**true**|Attiva il server di pubblicazione.|  
||**false**|Disattiva il server di pubblicazione.|  
|**distribution_db**||Nome del database di distribuzione.|  
|**accesso**||Nome dell'account di accesso.|  
|**password**||Password complessa per l'account di accesso fornito.|  
|**security_mode**|**1**|Esegue la connessione al server di pubblicazione utilizzando l'autenticazione di Windows. *Non è possibile modificare questo valore per un non* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *server di pubblicazione.*|  
||**0**|Esegue la connessione al server di pubblicazione utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Non è possibile modificare questo valore per un non* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *server di pubblicazione.*|  
|**working_directory**||Directory di lavoro utilizzata per archiviare i file dei dati e di schema per la pubblicazione.|  
|NULL (predefinito)||Verranno stampate tutte le opzioni di *Proprietà* disponibili.| 
|**storage_connection_string**| Chiave di accesso | Chiave di accesso per la directory di lavoro quando il database viene Istanza gestita di database SQL di Azure. 
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_changedistpublisher** viene utilizzato in tutti i tipi di replica.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_changedistpublisher**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà del server di distribuzione e dell'editore](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
