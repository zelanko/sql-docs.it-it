---
title: catalog.environments (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 7014c0e3-65dc-4a46-842e-4decf3737748
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 050ea5dcb0a4bc7b65c739e27389e29d5303e114
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85673258"
---
# <a name="catalogenvironments-ssisdb-database"></a>catalog.environments (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Vengono visualizzati i dettagli relativi all'ambiente di tutti gli ambienti nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Negli ambienti sono contenute variabili che possono fare riferimento ai progetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|environment_id|**bigint**|Identificatore (ID) univoco dell'ambiente.|  
|name|**sysname**|Il nome dell'ambiente.|  
|folder_id|**bigint**|ID univoco della cartella in cui si trova l'ambiente.|  
|description|**nvarchar(1024)**|Descrizione dell'ambiente. Questo valore è facoltativo.|  
|created_by_sid|**varbinary(85)**|ID di sicurezza (SID) dell'utente che ha creato l'ambiente.|  
|created_by_name|**nvarchar(128)**|Nome dell'utente che ha creato l'ambiente.|  
|created_time|**datetimeoffset**|Data e ora di creazione dell'ambiente.|  
  
## <a name="remarks"></a>Osservazioni  
 In questa vista viene visualizzata una riga per ogni ambiente nel catalogo. I nomi degli ambienti sono univoci solo per quanto riguarda la cartella in cui vengono individuati. Ad esempio, un ambiente denominato `E1` può esistere in più cartelle nel catalogo, ma ogni cartella può disporre solo di un ambiente denominato `E1`.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ sull'ambiente  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
> [!NOTE]  
>  È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
  
