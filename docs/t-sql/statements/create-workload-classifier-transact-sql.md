---
title: CREATE WORKLOAD CLASSIFIER (Transact-SQL) | Microsoft Docs
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
- CREATE WORKLOAD CLASSIFIER
- CREATE_WORKLOAD_CLASSIFIER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 276ec101595da24dff7ee805a414455936595398
ms.sourcegitcommit: 05bb10710489bef16bb2c53b3803e9b8eea1429a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2019
ms.locfileid: "57988753"
---
# <a name="create-workload-classifier-transact-sql-preview"></a>CREATE WORKLOAD CLASSIFIER (Transact-SQL) (anteprima)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Crea un classificatore di gestione del carico di lavoro.  Il classificatore assegna le richieste in ingresso a un gruppo di carico di lavoro e una priorità in base ai parametri specificati nella definizione di istruzione del classificatore.  I classificatori vengono valutati con ogni richiesta inviata.  Se una richiesta non viene abbinata a un classificatore, viene assegnata al gruppo del carico di lavoro predefinito.  Il gruppo di carico di lavoro predefinito è la classe di risorse smallrc.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintassi

```sql
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    ( WORKLOAD_GROUP = 'name'  
     ,MEMBERNAME = 'security_account'
 [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }])
[;]
```

## <a name="arguments"></a>Argomenti

 *classifier_name*  
 Specifica il nome con cui viene identificato il classificatore del carico di lavoro.  classifier_name è un sysname.  Può essere composto da un massimo di 128 caratteri e deve essere univoco all'interno dell'istanza.

WORKLOAD_GROUP = *'name'* Quando le regole del classificatore soddisfano le condizioni, name esegue il mapping della richiesta a un gruppo di carico di lavoro.  name è un sysname.  Può contenere fino a 128 caratteri e deve essere il nome di un gruppo di carico di lavoro valido al momento della creazione del classificatore.

WORKLOAD_GROUP deve eseguire il mapping a una classe di risorse esistente:

|Classi di risorse statiche|Classi di risorse dinamiche|
|------------------------|-----------------------|
|staticrc10|smallrc|
|staticrc20|mediumrc|
|staticrc30|largerc|
|staticrc40|xlargerc|
|staticrc50||
|staticrc60||
|staticrc70||
|staticrc80||

MEMBERNAME = *'security_account'* Si tratta dell'account di sicurezza da aggiungere al ruolo.  Security_account è un sysname, senza impostazioni predefinite. Security_account può essere un utente del database, un ruolo del database, un account di accesso di Azure Active Directory o un gruppo di Azure Active Directory.

IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } Specifica la priorità relativa di una richiesta.  I possibili valori di importanza sono i seguenti:

- LOW
- BELOW_NORMAL
- NORMAL (valore predefinito)
- ABOVE_NORMAL
- HIGH  

La priorità ha effetti sull'ordine in cui le richieste vengono pianificate, offrendo un accesso prioritario a risorse e blocchi.

## <a name="permissions"></a>Autorizzazioni

 È richiesta l'autorizzazione CONTROL DATABASE.  
  
## <a name="examples"></a>Esempi

 Nell'esempio riportato di seguito viene illustrato come creare un classificatore del carico di lavoro denominato `wgcELTRole`. Viene usato il gruppo di carico di lavoro staticrc20, l'utente `ELTRole` e la priorità viene impostata su `above_normal`.

```sql
CREATE WORKLOAD CLASSIFIER wgcELTRole
  WITH (WORKLOAD_GROUP = 'staticrc20'
       ,MEMBERNAME = 'ELTRole'
      ,IMPORTANCE = above_normal);
```

## <a name="see-also"></a>Vedere anche

[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)  
Vista del catalogo [sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md) Vista del catalogo [sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)
[SQL Data Warehouse Classification](/azure/sql-data-warehouse/classification) (Classificazione SQL Data Warehouse)
