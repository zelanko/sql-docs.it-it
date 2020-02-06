---
title: catalog.object_versions (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7dac194c0ceb54eeb716b9cf5ec676e7fe120d8f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296513"
---
# <a name="catalogobject_versions-ssisdb-database"></a>catalog.object_versions (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Vengono visualizzate le versioni di oggetti nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. In questa versione sono supportate solo le versioni di progetto in questa vista.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|Identificatore (ID) univoco della versione dell'oggetto. La sequenzialità di questo numero non è garantita.|  
|object_id|**bigint**|ID univoco dell'oggetto.|  
|object_type|**smallint**|Tipo di oggetto. Per i progetti verrà visualizzato un valore pari a `20`.|  
|object_name|**sysname(nvarchar(128))**|Nome dell'oggetto .|  
|description|**nvarchar(1024)**|Descrizione del progetto.|  
|created_by|**nvarchar(128)**|Nome dell'utente che ha aggiunto l'oggetto al catalogo.|  
|created_time|**datetimeoffset**|Data e ora di aggiunta dell'oggetto al catalogo.|  
|restored_by|**nvarchar(128)**|Nome dell'utente che ha ripristinato l'oggetto.|  
|last_restored_time|**datetimeoffset**|Data e ora dell'ultimo ripristino dell'oggetto.|  
  
## <a name="remarks"></a>Osservazioni  
 In questa vista viene visualizzata una riga per ogni versione di un oggetto nel catalogo.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per visualizzare le righe di questa vista, è necessario disporre di una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ sull'oggetto  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**.  
  
> [!NOTE]  
>  È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
  
