---
title: HTTP_STORAGE_OBJECT di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9a70b6c8093b48ce2f258fdfbfaf7f1d4c466561
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066947"
---
# <a name="sql-server-http_storage_object"></a>SQL Server, HTTP_STORAGE_OBJECT
  L'oggetto prestazione **SqlServer: HTTP_STORAGE_OBJECT** è costituito da contatori delle prestazioni che consentono di monitorare l'account di archiviazione di Azure. Usando [SQL Server file di dati in Azure](../databases/sql-server-data-files-in-microsoft-azure.md) , è possibile archiviare i file di database nei BLOB del servizio di archiviazione di Azure. Questo oggetto prestazione considera ogni account di Archiviazione di Azure come unità diversa.  
  
|Nome contatore|Descrizione|  
|------------------|-----------------|  
|**Byte letti/sec**|Quantità di dati trasferiti dalla risorsa di archiviazione HTTP al secondo durante le operazioni di lettura.|  
|**Byte scritti/sec**|Quantità di dati trasferiti dalla risorsa di archiviazione HTTP al secondo durante le operazioni di scrittura.|  
|**Totale byte/sec**|Quantità di dati trasferiti dalla risorsa di archiviazione HTTP al secondo durante le operazioni di lettura o scrittura.|  
|**Letture/sec**|Numero di operazioni di lettura al secondo sulla risorsa di archiviazione HTTP.|  
|**Scritture/sec**|Numero di operazioni di scrittura al secondo sulla risorsa di archiviazione HTTP.|  
|**Trasferimenti/sec**|Numero di operazioni di lettura e scrittura al secondo sulla risorsa di archiviazione HTTP.|  
|**Media byte/lettura**|Numero medio di byte trasferiti dalla risorsa di archiviazione HTTP per operazione di lettura.|  
|**Media byte/scrittura**|Numero medio di byte trasferiti dalla risorsa di archiviazione HTTP per operazione di scrittura.|  
|**Media byte/trasferimento**|Numero medio di byte trasferiti dalla risorsa di archiviazione HTTP durante le operazioni di lettura o scrittura.|  
|**Microsec. medi/lettura**|Numero medio di microsecondi impiegati per effettuare ogni operazione di lettura dalla risorsa di archiviazione HTTP.|  
|**Microsec. medi/scrittura**|Numero medio di microsecondi impiegati per effettuare ogni operazione di scrittura nella risorsa di archiviazione HTTP.|  
|**Microsec. medi/trasferimento**|Numero medio di microsecondi impiegati per effettuare ogni operazione di trasferimento nella risorsa di archiviazione HTTP.|  
|**I/O in attesa su risorsa di archiviazione HTTP**|Numero totale di operazioni di I/O in attesa di invio su una risorsa di archiviazione HTTP.|  
|**Archiviazione HTTP tentativi di I/O/sec**|Numero di richieste di nuovi tentativi inviate alla risorsa di archiviazione HTTP al secondo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
