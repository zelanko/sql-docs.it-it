---
title: catalog.projects (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4102ee4dc551a02a8b6853062e19d448ab414e7b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296523"
---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Visualizza i dettagli per tutti i progetti visualizzati nel catalogo di **SSISDB**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|Identificatore (ID) univoco del progetto.|  
|folder_id|**bigint**|ID univoco della cartella in cui si trova il progetto.|  
|name|**sysname**|Nome del progetto.|  
|description|**nvarchar(1024)**|Descrizione del progetto (facoltativa).|  
|project_format_version|**int**|Versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzata per lo sviluppo del progetto.|  
|deployed_by_sid|**varbinary(85)**|ID di sicurezza (SID) dell'utente che ha installato il pacchetto.|  
|deployed_by_name|**nvarchar(128)**|Nome dell'utente che ha installato il progetto.|  
|last_deployed_time|**datetimeoffset(7)**|Data e ora di distribuzione o ridistribuzione del progetto.|  
|created_time|**datetimeoffset(7)**|Data e ora di creazione del progetto.|  
|object_version_lsn|**bigint**|Versione del progetto. La sequenzialità di questo numero non è garantita.|  
|validation_status|**char(1)**|Stato di convalida.|  
|last_validation_time|**datetimeoffset(7)**|Ora dell'ultima convalida.|  
  
## <a name="remarks"></a>Osservazioni  
 In questa vista viene visualizzata una riga per ogni progetto nel catalogo.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ per il progetto  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**.  
  
> [!NOTE]  
>  Se si dispone dell'autorizzazione READ per un progetto, si dispone anche dell'autorizzazione READ per tutti i pacchetti e i riferimenti all'ambiente associati a tale progetto. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
  
