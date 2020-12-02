---
description: catalog.add_execution_worker (database SSISDB)
title: catalog.add_execution_worker (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
author: chugugrace
ms.author: chugu
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 102277139885379f4c2f75c912756e09131ec546
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129948"
---
# <a name="catalogadd_execution_worker-ssisdb-database"></a>catalog.add_execution_worker (database SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]

Aggiunge un servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker a un'istanza di esecuzione in Scale Out.

## <a name="syntax"></a>Sintassi

```sql
catalog.add_execution_worker [ @execution_id = ] execution_id, [ @workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>Argomenti
[ @execution_id = ] *execution_id*  
 Identificatore univoco per l'istanza di esecuzione. *execution_id* è di tipo **bigint**.  
 
[@workeragent_id = ] *workeragent_id*  
ID agente di lavoro di uno Scale Out Worker. *workeragent_id* è di tipo **uniqueIdentifier**.

## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  

## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni READ e MODIFY per l'istanza di esecuzione  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
 
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono generare un errore o un avviso:  
 
- Utente senza autorizzazioni appropriate.

- Identificatore di esecuzione non valido.

- ID agente di lavoro non valido.

- Esecuzione non inclusa in Scale Out.

## <a name="see-also"></a>Vedere anche
[Eseguire pacchetti in Scale Out](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).

