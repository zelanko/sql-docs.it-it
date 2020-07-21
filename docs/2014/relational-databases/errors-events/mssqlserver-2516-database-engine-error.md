---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a963119e19bf1561d3d14bf11cdec3271af1ffb0
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552096"
---
# <a name="mssqlserver_2516"></a>MSSQLSERVER_2516
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2516|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|Testo del messaggio|La correzione ha invalidato la mappa di bit differenziale per il database NAME. La catena di backup differenziale è stata interrotta. Prima di eseguire un backup differenziale è necessario eseguire un backup completo del database.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo messaggio informativo viene restituito quando si corregge l'errore MSSQLEngine_2515.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eseguire un backup completo del database.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un backup completo del database &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)  
  
  
