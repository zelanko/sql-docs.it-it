---
title: sys. sp_rda_reconcile_indexes (Transact-SQL) | Microsoft Docs
description: Informazioni su sys. sp_rda_reconcile_indexes. Vedere come utilizzare questo stored procedure Transact-SQL per accodare un'attività dello schema per riconciliare gli indici in una tabella remota.
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 098649587cbb6f01caafdedb631c901af160c85f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87236031"
---
# <a name="syssp_rda_reconcile_indexes-transact-sql"></a>sys. sp_rda_reconcile_indexes (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Accoda un'attività dello schema per riconciliare gli indici nella tabella remota. Al termine di questa attività, la tabella remota presenta gli stessi indici presenti nella tabella abilitata per l'estensione locale.  
  
 Se è presente un'altra attività in coda per riconciliare gli indici quando si chiama **sp_rda_reconcile_indexes**, questo stored procedure non accoda un'attività duplicata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @objname =] *' objname '*  
 Nome completo o non qualificato della tabella abilitata per l'estensione per la quale si desidera riconciliare gli indici. Le virgolette sono necessarie solo se si specifica un oggetto completo.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (esito positivo) o >0 (esito negativo)  
  
## <a name="see-also"></a>Vedi anche  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
