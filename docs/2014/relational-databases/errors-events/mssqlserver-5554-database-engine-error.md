---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a3d8ac3a04094c285622a5b91ce57cb1152d9b8a
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551176"
---
# <a name="mssqlserver_5554"></a>MSSQLSERVER_5554
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|MSSQLSERVER|  
|ID evento|5554|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|FS_MINIVER_OVERFLOW|  
|Testo del messaggio|È stato raggiunto il limite massimo di versioni totali per un singolo supportato dal file system.|  
  
## <a name="explanation"></a>Spiegazione  
 In scenari MARS (Multiple Active Result Set) o con presenza di trigger, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la miniversione specificata dal sistema operativo.  
  
## <a name="user-action"></a>Azione dell'utente  
 Tentare di evitare aggiornamenti ripetuti ai dati nella stessa transazione.  
  
  
