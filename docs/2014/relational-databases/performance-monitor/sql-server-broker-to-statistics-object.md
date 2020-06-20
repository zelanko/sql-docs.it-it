---
title: Oggetto Broker TO Statistics di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker Transmission Object object
- 'SQL Server: Broker Transmission Object'
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 93d9c24a175dedfee171eccfccb34673501660ed
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064699"
---
# <a name="sql-server-broker-to-statistics-object"></a>Oggetto Statistiche Broker TO di SQL Server
  L'oggetto prestazione SQLServer:Broker TO Statistics contiene informazioni sul numero di volte in cui le finestre di dialogo di [!INCLUDE[ssSB](../../includes/sssb-md.md)] richiedono oggetti trasmissione e sulla frequenza di scrittura degli oggetti trasmissione in **tempdb**.  
  
 Gli oggetti di trasmissione registrano lo stato delle trasmissioni di messaggi per una finestra di dialogo [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Poiché vengono archiviati in memoria, Per liberare memoria, [!INCLUDE[ssSB](../../includes/sssb-md.md)] scrive periodicamente batch di oggetti trasmissione inattivi nelle tabelle di lavoro di **tempdb**.  
  
 Nella tabella seguente sono elencati i contatori inclusi nell'oggetto.  
  
|Contatori dell'oggetto Statistiche Broker TO di SQL Server|Descrizione|  
|----------------------------------------------|-----------------|  
|**Byte media scritture in batch**|La quantità media di oggetti di trasmissione salvati in un batch.|  
|**Byte medio scrittura in batch (ms)**|Il tempo medio espresso in millisecondi richiesto per salvare un batch di oggetti di trasmissione.|  
|**Tempo medio tra batch (ms)**|Il tempo medio espresso in millisecondi tra le scritture di batch di oggetti di trasmissione.|  
|**Get TO/sec**|Quante volte le finestre di dialogo richiedono oggetti di trasmissione in un secondo.|  
|**TO dirty/sec**|Quante volte gli oggetti di trasmissione sono stati contrassegnati come dirty in un secondo. Gli oggetti trasmissione sono contrassegnati come dirty dalla prima modifica che rende la copia in memoria diversa dalla copia archiviata in **tempdb**. Gli oggetti trasmissione vengono modificati quando [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve registrare una modifica nello stato della trasmissione di messaggio per la finestra di dialogo.|  
|**Scritture TO/sec**|Il numero di volte al secondo in cui un batch di oggetti trasmissione viene scritto nelle tabelle di lavoro di **tempdb** . Un elevata quantità di scritture può indicare che quella memoria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è sotto sforzo.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server, oggetto metodi di accesso](sql-server-access-methods-object.md)   
 [SQL Server, oggetto Memory Manager](sql-server-memory-manager-object.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
