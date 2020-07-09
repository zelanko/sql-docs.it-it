---
title: catalog.disable_worker_agent (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cc3aae082a59cf122971798739e5add2b1886689
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053695"
---
# <a name="catalogdisable_worker_agent-ssisdb-database"></a>catalog.disable_worker_agent (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Disabilita uno Scale Out Worker per lo Scale Out Master che interagisce con questo catalogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

## <a name="syntax"></a>Sintassi

```sql
catalog.disable_worker_agent [ @WorkerAgentId = ] WorkerAgentId
```
## <a name="arguments"></a>Argomenti
[@WorkerAgentId =] *WorkerAgentId* ID agente di lavoro di Scale Out Worker. *WorkerAgentId* è di tipo **uniqueidentifier**.

## <a name="example"></a>Esempio
Questo esempio disabilita Scale Out Worker sul computer MachineA.

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[disable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  

## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin** 

## <a name="errors-and-warnings"></a>Errori e avvisi
Se l'ID agente di lavoro non è valido, la stored procedure restituisce un errore.
