---
title: catalog.environment_references (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: efec53ef-3e5a-4b76-b71d-a0cf9e11ac00
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1f2bb65c000cc2e355a21b11596dad65b0f8b3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65715333"
---
# <a name="catalogenvironmentreferences-ssisdb-database"></a>catalog.environment_references (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Visualizza i riferimenti all'ambiente per tutti i progetti nel catalogo di **SSISDB**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|reference_id|**bigint**|Identificatore (ID) univoco del riferimento.|  
|project_id|**bigint**|ID univoco del progetto.|  
|reference_type|**char(1)**|Viene indicato se l'ambiente può essere individuato nella stessa cartella del progetto (riferimento relativo) o in una cartella diversa (riferimento assoluto). Quando il valore è `R`, l'ambiente viene individuato tramite un riferimento relativo. Quando il valore è `A`, l'ambiente viene individuato tramite un riferimento assoluto.|  
|environment_folder_name|**sysname**|Nome della cartella se l'ambiente viene individuato tramite un riferimento assoluto.|  
|environment_name|**sysname**|Nome dell'ambiente a cui fa riferimento il progetto.|  
|validation_status|**char(1)**|Stato della convalida.|  
|last_validation_time|**datatimeoffset(7)**|Ora dell'ultima convalida.|  
  
## <a name="remarks"></a>Remarks  
 In questa vista viene visualizzata una riga per ogni riferimento all'ambiente nel catalogo.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ per il progetto corrispondente  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**.  
  
> [!NOTE]  
>  Se si dispone dell'autorizzazione READ per un progetto, si dispone anche dell'autorizzazione READ per tutti i pacchetti e i riferimenti all'ambiente associati a tale progetto. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
## <a name="remarks"></a>Remarks  
 Un progetto può disporre di riferimenti all'ambiente relativi o assoluti. I riferimenti relativi fanno riferimento all'ambiente in base al nome. Per tali riferimenti è necessario che l'ambiente si trovi nella stessa cartella del progetto. I riferimenti assoluti fanno riferimento all'ambiente in base al nome e alla cartella e possono fare riferimento ad ambienti che si trovano in una cartella di destinazione diversa da quella del progetto. Un progetto può fare riferimento a più ambienti.  
  
  
