---
title: sys.sp_rda_reconcile_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reconcile_indexes
- sp_rda_reconcile_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_indexes stored procedure
ms.assetid: 96b31ab9-bf84-46d6-9990-81f5c51f885a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fcb2226c52e8572e6432e0f21f4a782e130df067
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982946"
---
# <a name="syssprdareconcileindexes-transact-sql"></a>sys.sp_rda_reconcile_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Accoda un'attività di schema per riconciliare gli indici nella tabella remota. Dopo questa attività viene completata correttamente, la tabella remota ha gli stessi indici presenti nella tabella locale abilitata per l'estensione.  
  
 Se è presente un'altra attività in coda per riconciliare gli indici, quando si chiama **sp_rda_reconcile_indexes**, questa stored procedure non accodare un'attività duplicata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>Argomenti  
 [@objname =] *'objname'*  
 È il nome qualificato o non qualificato della tabella abilitata per l'estensione per il quale si desidera riconciliare gli indici. Le virgolette sono necessarie solo se si specifica un oggetto completo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o > 0 (esito negativo)  
  
## <a name="see-also"></a>Vedere anche  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
