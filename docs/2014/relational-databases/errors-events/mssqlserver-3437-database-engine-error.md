---
title: MSSQLSERVER_3437 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9999b8536faf87a02cdca3432416e7d12f6b2902
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62914529"
---
# <a name="mssqlserver_3437"></a>MSSQLSERVER_3437
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3437|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|NODTC|  
|Testo del messaggio|Errore durante il recupero del database '%.*ls'. Impossibile connettersi a Microsoft Distributed Transaction Coordinator (MS DTC) per controllare lo stato di avanzamento della transazione %S_XID. Correggere MS DTC, quindi eseguire nuovamente il recupero.|  
  
## <a name="explanation"></a>Spiegazione  
 Una o più transazioni distribuite in cui viene utilizzato [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) sono risultate incomplete alla chiusura del database. Non è stato possibile recuperare il database perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in grado di connettersi a MS DTC per completare le transazioni o eseguirne il rollback.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per recuperare il database, è necessario risolvere dapprima il problema relativo a MS DTC. Per analizzare il problema relativo a MS DTC, esaminare i registri eventi di Windows. Se non è possibile risolvere il problema e recuperare il database, ripristinare un backup del database.  
  
  
