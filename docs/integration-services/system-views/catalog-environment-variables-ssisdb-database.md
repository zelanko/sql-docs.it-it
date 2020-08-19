---
description: catalog.environment_variables (database SSISDB)
title: catalog.environment_variables (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b76045d5f901fa1444fd016d1c7673f46170332d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495332"
---
# <a name="catalogenvironment_variables-ssisdb-database"></a>catalog.environment_variables (database SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Vengono visualizzati i dettagli delle variabili di ambiente di tutti gli ambienti nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|Identificatore (ID) univoco della variabile di ambiente.|  
|environment_id|**bigint**|ID univoco dell'ambiente a cui è associata la variabile.|  
|name|**sysname**|Nome della variabile di ambiente.|  
|description|**nvarchar(1024)**|Descrizione della variabile di ambiente.|  
|type|**nvarchar(128)**|Tipo di dati della variabile di ambiente.|  
|sensitive|**bit**|Quando il valore è `1`, la variabile è importante e viene crittografata quando viene archiviata. Quando il valore è `0`, la variabile non è importante e il valore viene archiviato non crittografato.|  
|Valore|**sql_variant**|Valore della variabile di ambiente. Quando sensitive è `0`, viene visualizzato il valore non crittografato. Quando sensitive è `1`, viene visualizzato il valore **NULL**.|  
  
## <a name="remarks"></a>Commenti  
 In questa vista viene visualizzata una riga per ogni variabile di ambiente nel catalogo.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ sull'ambiente corrispondente  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
> [!NOTE]  
>  Quando si dispone delle autorizzazioni per eseguire un'operazione nel server, si dispone anche delle autorizzazioni per visualizzare le informazioni sull'operazione. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
  
