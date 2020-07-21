---
title: MSSQLSERVER_17887 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b889779da7f48ffd52d55c63e2ddb0742c065e59
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553506"
---
# <a name="mssqlserver_17887"></a>MSSQLSERVER_17887
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|17887|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SRV_IO_COMP_LISTENER_NONYIELDING|  
|Testo del messaggio|Listener completamento I/O (0x%lx) È possibile che il thread di lavoro 0x%p non ceda la precedenza del nodo %ld. Utilizzo CPU (circa): kernel %I64d ms, utente %I64d ms, intervallo: %I64d.|  
  
## <a name="explanation"></a>Spiegazione  
 Indica l'esistenza di un possibile problema con il Listener porta completamento I/O sul nodo specificato durante l'esecuzione della routine Completamento I/O per un evento di lettura/scrittura di rete. Questo errore non viene più visualizzato quando viene restituito il Listener della porta di completamento I/O in seguito all'esecuzione della routine Completamento I/O.  
  
## <a name="user-action"></a>Azione dell'utente  
 Contattare il Servizio Supporto Tecnico Microsoft.  
  
  
