---
title: Oggetto Plan Cache di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Plan Cache object
- SQLServer:Plan Cache
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ff1acb1fb3af2708b14b31eeb82aa0989685630c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210811"
---
# <a name="sql-server-plan-cache-object"></a>Oggetto Plan Cache di SQL Server
  L'oggetto **Plan Cache** include contatori che consentono di monitorare il modo in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la memoria per archiviare oggetti quali stored procedure, istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc e preparate e trigger. È possibile monitorare contemporaneamente più istanze dell'oggetto **Plan Cache** , che rappresentano diversi tipi di piani da monitorare.  
  
 Nella tabella seguente sono descritti i contatori **SQLServer:Plan Cache**.  
  
|Contatori di Plan Cache di SQL Server|Descrizione|  
|------------------------------------|-----------------|  
|**Percentuale riscontri cache**|Rapporto tra riscontri e ricerche nella cache.|  
|**Numero oggetti nella cache**|Numero di oggetti disponibili nella cache.|  
|**Pagine cache**|Numero di pagine da 8 KB usate dagli oggetti della cache.|  
|**Oggetti cache in uso**|Numero di oggetti della cache in uso.|  
  
 Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Istanza di Plan Cache|Descrizione|  
|-------------------------|-----------------|  
|**_Total**|Informazioni relative a tutti i tipi di istanze della cache.|  
|**Piani SQL**|Piani di query prodotti da una query [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, incluse le query con parametri automatici, oppure da istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] preparate tramite **sp_prepare** o **sp_cursorprepare**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memorizza nella cache i piani delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc per poterli riusare nel caso venga rieseguita la stessa istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . Anche le query con parametri dell'utente, sebbene non siano state preparate esplicitamente, vengono monitorate come piani SQL preparati.|  
|**Piani per gli oggetti**|Piani di query generati creando una stored procedure, una funzione o un trigger.|  
|**Alberi associati**|Alberi normalizzati per viste, regole, colonne calcolate e vincoli CHECK.|  
|**Stored procedure estese**|Informazioni di catalogo relative alle stored procedure estese.|  
|**Tabelle temporanee e variabili tabella**|Informazioni della cache relative a tabelle temporanee e variabili tabella.|  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server Server Memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Oggetto di Gestione buffer di SQL Server](sql-server-buffer-manager-object.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
