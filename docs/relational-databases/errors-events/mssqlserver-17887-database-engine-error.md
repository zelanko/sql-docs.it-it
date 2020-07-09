---
title: MSSQLSERVER_17887 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cdd998fdf93b12f58022ff345c8ea781f368d068
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780703"
---
# <a name="mssqlserver_17887"></a>MSSQLSERVER_17887
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
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
  
