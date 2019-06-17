---
title: sp_helpmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergefilter
- sp_helpmergefilter_TSQL
helpviewer_keywords:
- sp_helpmergefilter
ms.assetid: f133a094-0009-4771-b93b-e86a5c01e40b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 668233ad7ee79617caa60933a9eef33c5a810164
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62502802"
---
# <a name="sphelpmergefilter-transact-sql"></a>sp_helpmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui filtri di merge. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpmergefilter [ @publication= ] 'publication'   
    [ , [ @article= ] 'article']  
    [ , [ @filtername= ] 'filtername']  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'` È il nome dell'articolo. *articolo* viene **sysname**, il valore predefinito è **%** , che restituisce i nomi di tutti gli articoli.  
  
`[ @filtername = ] 'filtername'` È il nome del filtro su cui si desidera ottenere informazioni. *FilterName* viene **sysname**, il valore predefinito è **%** , che restituisce informazioni su tutti i filtri definiti per l'articolo o la pubblicazione.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**join_filterid**|**int**|ID del filtro join.|  
|**filtername**|**sysname**|Nome del filtro.|  
|**nome di articolo di join**|**sysname**|Nome dell'articolo di join.|  
|**join_filterclause**|**nvarchar(2000)**|Clausola di filtro che qualifica il join.|  
|**join_unique_key**|**int**|Indica se il join è basato su una chiave univoca.|  
|**proprietario della tabella di base**|**sysname**|Nome del proprietario della tabella di base.|  
|**nome della tabella di base**|**sysname**|Nome della tabella di base.|  
|**proprietario della tabella join**|**sysname**|Nome del proprietario della tabella che si desidera unire in join alla tabella di base.|  
|**nome della tabella join**|**sysname**|Nome della tabella che si desidera unire in join alla tabella di base.|  
|**nome dell'articolo**|**sysname**|Nome dell'articolo di tabella che si desidera unire in join alla tabella di base.|  
|**filter_type**|**tinyint**|Tipo di filtro di merge. I possibili valori sono i seguenti:<br /><br /> **1** = solo filtro join<br /><br /> **2** = relazione tra record logici<br /><br /> **3** = both|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpmergefilter** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server e il **db_owner** ruolo predefinito del database possono eseguire **sp_helpmergefilter**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
