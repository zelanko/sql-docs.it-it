---
title: sp_removedistpublisherdbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6801079c3d16871712e5ba4494ca2c3dbf5bb662
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751666"
---
# <a name="sp_removedistpublisherdbreplication-transact-sql"></a>sp_removedistpublisherdbreplication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Rimuove i metadati di pubblicazione appartenenti a una pubblicazione specifica nel server di distribuzione. La stored procedure viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'`Nome del server di pubblicazione. *Publisher* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @publisher_db = ] 'publisher_db'`Nome del database di pubblicazione. *publisher_db* è di **tipo sysname** e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_removedistpublisherdbreplication** viene utilizzata dalla replica transazionale e snapshot.  
  
 **sp_removedistpublisherdbreplication** viene utilizzato quando è necessario ricreare un database pubblicato senza eliminare anche il database di distribuzione. Vengono rimossi i metadati seguenti:  
  
-   Tutti i metadati della pubblicazione.  
  
-   I metadati di tutti gli articoli che appartengono alla pubblicazione.  
  
-   I metadati di tutte le sottoscrizioni della pubblicazione.  
  
-   I metadati di tutti i processi dell'agente di replica che appartengono alla pubblicazione.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** nel server di distribuzione o i membri del ruolo predefinito del database **db_owner** nel database di distribuzione possono eseguire **sp_removedistpublisherdbreplication**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
