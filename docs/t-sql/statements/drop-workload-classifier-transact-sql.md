---
title: DROP WORKLOAD CLASSIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 67909db180af056add12324622cfd6094d8729fe
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105827"
---
# <a name="drop-workload-classifier-transact-sql"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Elimina un classificatore di gestione del carico di lavoro esistente definito dall'utente.  
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintassi  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>Argomenti

*classifier_name*  
Specifica il nome con cui viene identificato il classificatore del carico di lavoro.  classifier_name è un sysname.  Può essere composto da un massimo di 128 caratteri e deve essere univoco all'interno dell'istanza.
  
## <a name="remarks"></a>Remarks

L'istruzione DROP WORKLOAD CLASSIFIER non è consentita nei classificatori di carico di lavoro di sistema.

Se le richieste sono in esecuzione o nella coda di richieste in sospeso, mantengono la classificazione e il classificatore può essere eliminato immediatamente.  Se si elimina un classificatore e lo si ricrea con una priorità diversa non si avrà alcun effetto sulle richieste già classificate.

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione CONTROL DATABASE.  
  
## <a name="examples"></a>Esempi

L'esempio seguente illustra come eliminare il classificatore di carico di lavoro denominato `wgcELTROLE`.  

```sql
DROP WORKLOAD CLASSIFIER wgcELTRole;
```

> [!NOTE]
> Le richieste inviate senza un classificatore corrispondente vengono classificate nel gruppo di carico di lavoro predefinito.  Il gruppo di carico di lavoro predefinito è la classe di risorse smallrc.
  
## <a name="see-also"></a>Vedere anche

[CREATE WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-classifier-transact-sql.md)</br>
[SQL Data Warehouse Classification](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) (Classificazione SQL Data Warehouse)
