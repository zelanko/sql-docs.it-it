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
manager: craigg
ms.openlocfilehash: 07213247345280e992c2fbd5552d5cdfb96747ab
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133561"
---
# <a name="spchangearticlecolumndatatype-transact-sql"></a>sp_changearticlecolumndatatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica il mapping del tipo di dati della colonna dell'articolo per una pubblicazione Oracle. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
> [!NOTE]  
>  Sono disponibili per impostazione predefinita i mapping dei tipi di dati tra i tipi supportati dal server di pubblicazione. Uso **sp_changearticlecolumndatatype** solo quando si esegue l'override delle impostazioni predefinite.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=** ] **'**_pubblicazione_**'**  
 Nome della pubblicazione Oracle. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@article =** ] **'**_articolo_**'**  
 Nome dell'articolo. *articolo* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@column**=] **'**_colonna_**'**  
 Nome della colonna per cui modificare il mapping dei tipi di dati. *colonna* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@type** =] **'**_tipo_**'**  
 È il nome del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati nella colonna di destinazione. *tipo di* viene **sysname**, con un valore predefinito è NULL.  
  
 [ **@length** =] *lunghezza*  
 Lunghezza del tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella colonna di destinazione. *lunghezza* viene **bigint**, con un valore predefinito è NULL.  
  
 [ **@precision**=] *precisione*  
 Precisione del tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella colonna di destinazione. *precisione* viene **bigint**, con un valore predefinito è NULL.  
  
 [ **@publisher**=] **'**_editore_**'**  
 Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **Sp_changearticlecolumndatatype** viene usato per sostituire il mapping dei tipi di dati predefiniti tra i tipi supportati di server di pubblicazione (Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Per visualizzare questi mapping dei tipi di dati predefiniti, eseguire [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **sp_changearticlecolumndatatype** è supportata solo per i server di pubblicazione Oracle. Se si esegue questa stored procedure su una pubblicazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene generato un errore.  
  
 **sp_changearticlecolumndatatype** deve essere eseguita per ogni mapping di colonna di articolo che deve essere modificata.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_changearticlecolumndatatype**.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le proprietà di pubblicazioni e articoli](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
