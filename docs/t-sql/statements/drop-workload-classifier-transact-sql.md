---
title: DROP WORKLOAD CLASSIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
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
ms.openlocfilehash: a9ef53323d77f1439df5daf0fedc669fe380cb3f
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581515"
---
# <a name="drop-workload-classifier-transact-sql-preview"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL) (anteprima)

> [!Note]
> La classificazione del carico di lavoro è disponibile in anteprima in SQL Data Warehouse Gen2. L'anteprima dell'importanza e della classificazione per la gestione del carico di lavoro è destinata alle build con data di rilascio 9 aprile 2019 o successiva.  Si consiglia agli utenti di evitare l'uso di build precedenti a tale data per il test della gestione del carico di lavoro.  Per determinare se la build in uso supporta la gestione del carico di lavoro, eseguire select @@version quando si è connessi all'istanza di SQL Data Warehouse.

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
