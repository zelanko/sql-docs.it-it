---
title: sp_helpmergearticlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticlecolumn
- sp_helpmergearticlecolumn_TSQL
helpviewer_keywords:
- sp_helpmergearticlecolumn
ms.assetid: 651c017b-9e9a-48f2-a0bd-6fc896eab334
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f4829928bbf1f8e13483de69a749e748bd9dd095
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779063"
---
# <a name="sphelpmergearticlecolumn-transact-sql"></a>sp_helpmergearticlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce l'elenco di colonne dell'articolo della tabella o vista specificato per una pubblicazione di tipo merge. Poiché le stored procedure non includono colonne, questa procedura restituisce un errore se, come articolo, viene specificata una stored procedure. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpmergearticlecolumn [ @publication = ] 'publication' ]  
        , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'***pubblicazione***'**  
 È il nome della pubblicazione. *publication* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@article=**] **'***articolo***'**  
 È il nome di una tabella o vista che rappresenta l'articolo per recuperare le informazioni su. *articolo* viene **sysname**, non prevede alcun valore predefinito.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**column_id**|**sysname**|Identificatore della colonna.|  
|**column_name**|**sysname**|Nome della colonna di una tabella o vista.|  
|**Pubblicato**|**bit**|Specifica se pubblicare il nome della colonna.<br /><br /> **1** specifica che la colonna viene pubblicata.<br /><br /> **0** specifica che non è pubblicata.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpmergearticlecolumn** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **replmonitor** ruolo predefinito del database nel database di distribuzione o elenco di accesso alla pubblicazione per la pubblicazione possono eseguire **sp_helpmergearticlecolumn**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
