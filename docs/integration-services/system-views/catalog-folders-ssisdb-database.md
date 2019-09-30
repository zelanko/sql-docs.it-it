---
title: catalog.folders (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14930bfd90b242f30a8b3f265f6ed3b367bd07f9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296534"
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Vengono visualizzate le cartelle nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|id|**bigint**|Identificatore univoco della cartella.|  
|NAME|**sysname(nvarchar(128)**|Nome della cartella che è univoco all'interno del catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
|description|**nvarchar(1024)**|Descrizione della cartella.|  
|created_by_sid|**varbinary(85)**|ID di sicurezza (SID) dell'utente che ha creato la cartella.|  
|created_by_name|**nvarchar(128)**|Nome dell'utente che ha creato la cartella.|  
|created_time|**datetimeoffset(7)**|Data e ora di creazione della cartella.|  
  
## <a name="remarks"></a>Remarks  
 In questa vista viene visualizzata una riga per ogni cartella nel catalogo.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ sulla cartella  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
> [!NOTE]  
>  Quando si dispone delle autorizzazioni per eseguire un'operazione nel server, si dispone anche delle autorizzazioni per visualizzare le informazioni sull'operazione. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
  
