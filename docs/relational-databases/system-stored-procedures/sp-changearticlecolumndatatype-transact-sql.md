---
title: sp_changearticlecolumndatatype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changearticlecolumndatatype
- sp_changearticlecolumndatatype_TSQL
helpviewer_keywords:
- sp_changearticlecolumndatatype
ms.assetid: 0db80e08-fb77-4d0c-aa41-455b13ffa9b4
author: stevestein
ms.author: sstein
ms.openlocfilehash: f101d9081c7eb898d43c461a3bd64eca0c043b64
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67995522"
---
# <a name="sp_changearticlecolumndatatype-transact-sql"></a>sp_changearticlecolumndatatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica il mapping del tipo di dati della colonna dell'articolo per una pubblicazione Oracle. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
> [!NOTE]  
>  Sono disponibili per impostazione predefinita i mapping dei tipi di dati tra i tipi supportati dal server di pubblicazione. Utilizzare **sp_changearticlecolumndatatype** solo quando si esegue l'override di queste impostazioni predefinite.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changearticlecolumndatatype [ @publication= ] 'publication'  
    [ @article = ] 'article'   
    [ @column = ] 'column'  
    [ , [ @type = ] 'type' ]  
    [ , [ @length = ] length ]  
    [ , [ @precision = ] precision ]  
    [ , [ @scale = ] scale ]  
    [ , [ @publisher = ] 'publisher'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione Oracle. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'`Nome dell'articolo. *article* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @column = ] 'column'`Nome della colonna per cui modificare il mapping dei tipi di dati. *Column* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @type = ] 'type'`Nome del tipo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati nella colonna di destinazione. *Type* è di tipo **sysname**e il valore predefinito è null.  
  
`[ @length = ] length`Lunghezza del tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati nella colonna di destinazione. *length* è di tipo **bigint**e il valore predefinito è null.  
  
`[ @precision = ] precision`Precisione del tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati nella colonna di destinazione. *Precision* è di tipo **bigint**e il valore predefinito è null.  
  
`[ @publisher = ] 'publisher'`Specifica un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione non. *Publisher* è di **tipo sysname**e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **Sp_changearticlecolumndatatype** viene utilizzato per eseguire l'override dei mapping dei tipi di dati predefiniti tra i tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]server di pubblicazione supportati (Oracle e). Per visualizzare i mapping dei tipi di dati predefiniti, eseguire [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **sp_changearticlecolumndatatype** è supportato solo per i Publisher Oracle. Se si esegue questa stored procedure su una pubblicazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene generato un errore.  
  
 è necessario eseguire **sp_changearticlecolumndatatype** per ogni mapping di colonna degli articoli che è necessario modificare.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_changearticlecolumndatatype**.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le proprietà di pubblicazioni e articoli](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Mapping dei tipi di dati per i Publisher Oracle](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
