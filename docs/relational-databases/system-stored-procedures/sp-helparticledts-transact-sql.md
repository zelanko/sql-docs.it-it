---
description: sp_helparticledts (Transact-SQL)
title: sp_helparticledts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9e768bd98561338d392c5fc4c65c00c9ab5c7f59
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541781"
---
# <a name="sp_helparticledts-transact-sql"></a>sp_helparticledts (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Consente di ottenere informazioni sui nomi delle attività personalizzate da utilizzare per la creazione di una sottoscrizione di trasformazione in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` Nome della pubblicazione. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'` Nome di un articolo della pubblicazione. *article* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|Nome dell'attività di programmazione eseguita prima della copia dei dati dello snapshot. L'esecuzione del programma viene proseguita se viene rilevato un errore di script.|  
|**pre_script_task_name**|**sysname**|Nome dell'attività di programmazione eseguita prima della copia dei dati dello snapshot. L'esecuzione del programma viene interrotta se viene rilevato un errore.|  
|**transformation_task_name**|**sysname**|Nome dell'attività di programmazione quando si utilizza un'attività Query guidata dai dati.|  
|**post_script_ignore_error_task_name**|**sysname**|Nome dell'attività di programmazione eseguita dopo la copia dei dati dello snapshot. L'esecuzione del programma viene proseguita se viene rilevato un errore di script.|  
|**post_script_task_name**|**sysname**|Nome dell'attività di programmazione eseguita dopo la copia dei dati dello snapshot. L'esecuzione del programma viene interrotta se viene rilevato un errore.|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helparticledts** viene utilizzata nella replica snapshot e nella replica transazionale.  
  
 Per i nomi delle attività di un programma di replica DTS (Data Transformation Services) è necessario seguire determinate convenzioni di denominazione richieste dagli agenti di replica. Per le attività personalizzate, ad esempio Esegui SQL, il nome è una stringa concatenata composta dal nome dell'articolo, da un prefisso e da una terza parte facoltativa. Durante la scrittura del codice, in caso di dubbio sui nomi delle attività, è possibile analizzare il set di risultati che indica i nomi delle attività da utilizzare.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** e del ruolo predefinito del database **db_owner** possono eseguire **sp_helparticledts**.  
  
  
