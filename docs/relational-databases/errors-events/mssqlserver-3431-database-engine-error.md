---
title: MSSQLSERVER_3431 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3431 (Database Engine error)
ms.assetid: 9541217f-e5c6-4a12-a19a-006058f1d3f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 921dde33b466cf9f72a8254f304d2a0abd739f7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132393"
---
# <a name="mssqlserver3431"></a>MSSQLSERVER_3431
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3431|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|UNRESOLVED_XACT|  
|Testo del messaggio|Impossibile recuperare il database '%.*ls' (ID di database %d) perché i risultati di una transazione non sono stati risolti. Le transazioni di Microsoft Distributed Transaction Coordinator (MS DTC) sono state preparate, ma l'applicazione non è stata in grado di determinarne la risoluzione. Per risolvere il problema, correggere MS DTC, eseguire un ripristino da un backup completo oppure correggere il database.|  
  
## <a name="explanation"></a>Spiegazione  
Una o più transazioni distribuite in cui viene utilizzato [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) sono risultate incomplete alla chiusura del database. Non è stato possibile recuperare il database perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in grado di completare le transazioni o di eseguirne il rollback senza disporre di ulteriori informazioni restituite da MS DTC.  
  
## <a name="user-action"></a>Azione dell'utente  
Per recuperare il database, è necessario risolvere dapprima il problema relativo a MS DTC. Per analizzare il problema relativo a MS DTC, esaminare i registri eventi di Windows. Se non è possibile risolvere il problema e recuperare il database, ripristinare un backup del database.  
  
