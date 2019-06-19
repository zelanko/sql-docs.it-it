---
title: catalog.add_execution_worker (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
author: janinezhang
ms.author: janinez
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: a7e68b6f2ad46eb4f18bd46e0f4728bdec35d366
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65717240"
---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>catalog.add_execution_worker (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Aggiunge un servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker a un'istanza di esecuzione in Scale Out.

## <a name="syntax"></a>Sintassi

```sql
catalog.add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>Argomenti
[ @execution_id = ] *execution_id*  
 Identificatore univoco per l'istanza di esecuzione. *execution_id* è di tipo **bigint**.  
 
[@workeragent_id = ] *workeragent_id*  
ID agente di lavoro di uno Scale Out Worker. *workeragent_id* è di tipo **uniqueIdentifier**.

## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  

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

