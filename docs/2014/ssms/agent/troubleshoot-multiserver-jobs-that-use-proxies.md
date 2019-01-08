---
title: Risolvere i problemi relativi a processi multiserver che usano proxy | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 628475d5691969a77d2d0ba4db01441c51b8deae
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818713"
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>Risolvere i problemi relativi a processi multiserver che utilizzano proxy
  I processi distribuiti con passaggi associati a un proxy vengono eseguiti nel contesto dell'account proxy nel server di destinazione. Se si verificano errori quando i passaggi di processo che usano account proxy vengono scaricati dal server master, controllare la colonna **error_message** nella tabella **sysdownloadlist** del database **msdb** per verificare l'eventuale presenza dei messaggi di errore seguenti:  
  
-   "Per questo passaggio del processo è necessario un account proxy, ma l'individuazione dei proxy è disabilitata nel server di destinazione."  
  
     Per risolvere questo problema, impostare la sottochiave del Registro di sistema **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.***\<n*>** \SQLServerAgent\AllowDownloadedJobsToMatchProxyName** su **1 (vero)**. Per impostazione predefinita, questa sottochiave è impostata su **0** (`false`). Il valore di **MSSQL.**\<*n*> è il nome dell'istanza, ad esempio, **MSSQL.1** o **MSSQL.3**.  
  
-   "Impossibile trovare il proxy."  
  
     Per risolvere il problema, verificare che nel server di destinazione sia disponibile un account proxy con lo stesso nome dell'account proxy del server master utilizzato per l'esecuzione del passaggio del processo.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un ambiente multiserver](create-a-multiserver-environment.md)  
  
  
