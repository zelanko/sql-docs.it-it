---
title: catalog.execution_data_taps | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4a94d4ab27e8e92e4ec35b899485bb33962c0fde
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912584"
---
# <a name="catalogexecution_data_taps"></a>catalog.execution_data_taps 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Visualizza le informazioni per ogni scelta dei dati definita in un'esecuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|Identificatore univoco (ID) della scelta dei dati.|  
|execution_id|**bigint**|Identificatore univoco (ID) per l'istanza di esecuzione.|  
|package_path|**nvarchar(max)**|Percorso del pacchetto per l'attività Flusso di dati in cui vengono scelti i dati.|  
|dataflow_path_id_string|**nvarchar(4000)**|Stringa di identificazione del percorso del flusso di dati.|  
|dataflow_task_guid|**uniqueidentifier**|ID univoco dell'attività Flusso di dati.|  
|max_rows|**int**|Numero di righe da acquisire. Se questo valore non è specificato, verranno acquisite tutte le righe.|  
|filename|**nvarchar(4000)**|Nome del file dump di dati. Per altre informazioni, vedere [Generazione di file di dump per l'esecuzione del pacchetto](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).|  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ per l'istanza di esecuzione  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
> [!NOTE]  
>  Quando si dispone delle autorizzazioni per eseguire un'operazione nel server, si dispone anche delle autorizzazioni per visualizzare le informazioni sull'operazione. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Generazione di file di dump per l'esecuzione dei pacchetti](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
