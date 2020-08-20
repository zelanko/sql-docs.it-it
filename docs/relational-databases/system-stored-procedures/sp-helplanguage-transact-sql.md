---
description: sp_helplanguage (Transact-SQL)
title: sp_helplanguage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 72f2e867c8139045b107cbb99871742c26440ee4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489334"
---
# <a name="sp_helplanguage-transact-sql"></a>sp_helplanguage (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce informazioni su una lingua alternativa specifica o su tutte le lingue in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @language = ] 'language'` Nome della lingua alternativa per la quale visualizzare le informazioni. *Language* è di **tipo sysname**e il valore predefinito è null. Se viene specificata la *lingua* , vengono restituite informazioni sulla lingua specificata. Se la lingua non è specificata, vengono restituite informazioni su tutte le lingue nella vista di compatibilità **sys.syslinguaggi** .  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|Numero di identificazione della lingua.|  
|**DateFormat**|**nchar(3)**|Formato della data.|  
|**DATEFIRST**|**tinyint**|Primo giorno della settimana: 1 per lunedì, 2 per martedì e così via fino a 7 per domenica.|  
|**aggiornamento**|**int**|Versione dell'ultimo aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la lingua specificata.|  
|**nome**|**sysname**|Nome della lingua.|  
|**alias**|**sysname**|Nome alternativo per la lingua.|  
|**months**|**nvarchar(372)**|Nomi dei mesi.|  
|**shortmonths**|**nvarchar(132)**|Nomi brevi dei mesi.|  
|**giorni**|**nvarchar(217)**|Nomi dei giorni.|  
|**lcid**|**int**|ID delle impostazioni locali di Windows relative alla lingua.|  
|**msglangid**|**smallint**|ID del gruppo di messaggi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo **public** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-information-about-a-single-language"></a>R. Restituzione di informazioni su una sola lingua  
 Nell'esempio seguente vengono visualizzate informazioni sulla lingua alternativa `French`.  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. Restituzione di informazioni su tutte le lingue  
 Nell'esempio seguente vengono visualizzate informazioni su tutte le lingue alternative installate.  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di motore di database &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [IMPOSTAZIONE della lingua &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
