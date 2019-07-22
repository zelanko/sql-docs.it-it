---
title: catalog.set_worker_agent_property (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 986807ab07a563fef1ae8a9231db194a4a5943e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038671"
---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Imposta la proprietà di un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker.

## <a name="syntax"></a>Sintassi

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>Argomenti
[@WorkerAgentId =] *WorkerAgentId*  
ID agente di lavoro dello Scale Out Worker. *WorkerAgentId* è di tipo **uniqueidentifier**.

[@PropertyName =] *PropertyName*  
Nome della proprietà. *PropertyName* è di tipo **nvarchar(256)** .

[@PropertyValue =] *PropertyValue*  
Valore della proprietà. *PropertyValue* è di tipo **nvarchar(max)** .

## <a name="remarks"></a>Remarks
I nomi di proprietà validi sono **DisplayName**, **Description**, **Tags**.

## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  

## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**

## <a name="errors-and-warnings"></a>Errori e avvisi
  Nell'elenco seguente vengono descritte alcune condizioni che possono generare un errore o un avviso:  
  
-   Utente senza autorizzazioni appropriate. 

-   ID agente di lavoro non valido.

-   Nome della proprietà non valido.

-   Valore della proprietà non valido.  
