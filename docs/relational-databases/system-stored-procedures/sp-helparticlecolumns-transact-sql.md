---
title: sp_helparticlecolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticlecolumns
- sp_helparticlecolumns_TSQL
helpviewer_keywords:
- sp_helparticlecolumns
ms.assetid: 9ea55df3-2e99-4683-88ad-bde718288bc7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c15a9051c6d706ddec55d031e93858a3d33c9d3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82815869"
---
# <a name="sp_helparticlecolumns-transact-sql"></a>sp_helparticlecolumns (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Restituisce tutte le colonne della tabella sottostante. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione. Per i server di pubblicazione Oracle questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helparticlecolumns [ @publication = ] 'publication'   
        , [ @article = ] 'article'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione contenente l'articolo. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'`Nome dell'articolo per cui vengono restituite le colonne. *article* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @publisher = ] 'publisher'`Specifica un server di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pubblicazione non. *Publisher* è di **tipo sysname**e il valore predefinito è null.  
  
> [!NOTE]  
>  il *server di pubblicazione* non deve essere specificato quando l'articolo richiesto viene pubblicato da un server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pubblicazione.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (colonne non pubblicate) o **1** (colonne pubblicate)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**ID colonna**|**int**|Identificatore della colonna.|  
|**column**|**sysname**|Nome della colonna.|  
|**published**|**bit**|Indica se la colonna è pubblicata:<br /><br /> **0** = No<br /><br /> **1** = Sì|  
|**tipo di server di pubblicazione**|**sysname**|Tipo di dati della colonna nel server di pubblicazione.|  
|**tipo di Sottoscrittore**|**sysname**|Tipo di dati della colonna nel Sottoscrittore.|  
  
## <a name="remarks"></a>Commenti  
 **sp_helparticlecolumns** viene utilizzata per la replica snapshot e transazionale.  
  
 **sp_helparticlecolumns** è utile per il controllo di una partizione verticale.  
  
## <a name="permissions"></a>Autorizzazioni  
 È possibile eseguire **sp_helparticlecolumns**solo i membri del ruolo predefinito del server **sysadmin** , del ruolo predefinito del database **db_owner** o dell'elenco di accesso alla pubblicazione corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Definire e modificare un filtro colonne](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [sp_addarticle &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_droppublication &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
