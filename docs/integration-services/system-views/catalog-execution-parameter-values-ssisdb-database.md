---
title: catalog.execution_parameter_values (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ec93e67b-04ce-4aae-ab96-3ad20e9793ad
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8fd328fa1d1112e0bafc8fda98f1fdaa986a3b40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065261"
---
# <a name="catalogexecutionparametervalues-ssisdb-database"></a>catalog.execution_parameter_values (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Vengono visualizzati i valori effettivi del parametro utilizzati dai pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] durante un'istanza di esecuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|execution_parameter_id|**bigint**|Identificatore (ID) univoco del parametro di esecuzione.|  
|execution_id|**bigint**|ID univoco per l'istanza di esecuzione.|  
|object_type|**smallint**|Quando il valore è `20`, il parametro è un parametro del progetto. Quando il valore è `30`, il parametro è un parametro del pacchetto. Quando il valore è `50`, il parametro è uno tra quelli indicati di seguito:<br /><br /> **LOGGING_LEVEL**<br /><br /> **DUMP_ON_ERROR**<br /><br /> **DUMP_ON_EVENT**<br /><br /> **DUMP_EVENT_CODE**<br /><br /> **CALLER_INFO**<br /><br /> **SYNCHRONIZED**|  
|parameter_data_type|**nvarchar(128)**|Tipo di dati del parametro.|  
|parameter_name|**sysname**|Nome del parametro.|  
|parameter_value|**sql_variant**|Valore del parametro. Quando sensitive è `0`, viene visualizzato il valore non crittografato. Quando sensitive è `1`, viene visualizzato il valore **NULL**.|  
|sensitive|**bit**|Quando il valore è `1`, il valore del parametro è importante. In caso contrario, il valore è `0`.|  
|required|**bit**|Quando il valore è `1`, il valore del parametro è necessario per avviare l'esecuzione. In caso contrario, il valore è `0`.|  
|value_set|**bit**|Quando il valore è `1`, il valore del parametro è stato assegnato. In caso contrario, il valore è `0`.|  
|runtime_override|**bit**|Quando il valore è `1`, il valore del parametro è stato modificato rispetto a quello originale prima di avviare l'esecuzione. Quando il valore è `0`, il valore del parametro è il valore originale impostato.|  
  
## <a name="remarks"></a>Remarks  
 In questa vista viene visualizzata una riga per ogni parametro di esecuzione nel catalogo. Un valore del parametro di esecuzione è il valore assegnato al parametro del progetto o a quello del pacchetto durante una singola istanza di esecuzione.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ per l'istanza di esecuzione  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
> [!NOTE]  
>  Quando si dispone delle autorizzazioni per eseguire un'operazione nel server, si dispone anche delle autorizzazioni per visualizzare le informazioni sull'operazione. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
  
