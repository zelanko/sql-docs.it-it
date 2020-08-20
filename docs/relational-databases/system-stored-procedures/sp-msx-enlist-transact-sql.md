---
description: sp_msx_enlist (Transact-SQL)
title: sp_msx_enlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_enlist_TSQL
- sp_msx_enlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_enlist
ms.assetid: ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 024aa764c6df0fa4e42a006cb6b6d855c32e3573
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481154"
---
# <a name="sp_msx_enlist-transact-sql"></a>sp_msx_enlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Consente di aggiungere il server corrente all'elenco di server disponibili nel server master.  
  
> [!CAUTION]  
>  Il **sp_msx_enlist** stored procedure modifica il registro di sistema. La modifica manuale del Registro di sistema non è un'operazione consigliata, in quanto modifiche inadeguate o non corrette possono causare gravi problemi di configurazione nel sistema. La modifica del Registro di sistema tramite l'editor corrispondente deve essere pertanto eseguita esclusivamente da utenti esperti. Per ulteriori informazioni, vedere la documentazione di Microsoft Windows.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_msx_enlist [@msx_server_name =] 'msx_server'   
     [, [@location =] 'location']  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @msx_server_name = ] 'msx_server'` Nome del server di amministrazione multiserver (Master). *msx_server* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @location = ] 'location'` Percorso del server di destinazione da aggiungere. *location* è di **tipo nvarchar (100)** e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="permissions"></a>Autorizzazioni  
 Le autorizzazioni per l'esecuzione di questa procedura vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente il server corrente viene integrato nel server master `AdventureWorks1`. L'ubicazione del server corrente è `Building 21, Room 309, Rack 5`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_msx_defect &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Stored procedure di sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [xp_cmdshell &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)  
  
  
