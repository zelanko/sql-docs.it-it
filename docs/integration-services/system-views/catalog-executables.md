---
description: catalog.executables
title: catalog.executables | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9c17439cda7e5071c4256be53ae4ec03dc3ccfff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495241"
---
# <a name="catalogexecutables"></a>catalog.executables 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  In questa vista viene visualizzata una riga per ogni eseguibile nell'esecuzione specificata.  
  
 Un eseguibile è un'attività o un contenitore aggiunto al flusso di controllo di un pacchetto.  
  
|Nome colonna|**Tipo di dati**|Descrizione|  
|-----------------|-------------------|-----------------|  
|executable_id|**bigint**|Identificatore univoco per l'eseguibile.|  
|execution_id|**bigint**|Identificatore univoco per l'istanza di esecuzione.|  
|executable_name|**nvarchar(4000)**|Nome dell'eseguibile.|  
|executable_guid|**nvarchar(38)**|GUID dell'eseguibile.|  
|package_name|**nvarchar(260)**|Nome del pacchetto.|  
|package_path|**nvarchar(max)**|Percorso del pacchetto.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ per l'istanza di esecuzione  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
> [!NOTE]  
>  Quando si dispone delle autorizzazioni per eseguire un'operazione nel server, si dispone anche delle autorizzazioni per visualizzare le informazioni sull'operazione. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
## <a name="remarks"></a>Osservazioni  
  
