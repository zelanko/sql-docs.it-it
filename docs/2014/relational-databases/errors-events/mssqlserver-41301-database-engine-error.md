---
title: MSSQLSERVER_41301 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41301 (Database Engine error)
ms.assetid: c6127e1e-2846-4ee9-bc42-2d896ea9730e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4283f3bd82af68239052d6184919e0c90ada7f7e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033229"
---
# <a name="mssqlserver_41301"></a>MSSQLSERVER_41301
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|41301|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|COMMIT_DEPENDENCY_FAILURE|  
|Testo del messaggio|Una transazione precedente da cui dipende la transazione corrente è stata interrotta. Impossibile eseguire il commit della transazione corrente.|  
  
## <a name="explanation"></a>Spiegazione  
 La transazione ha rilevato un errore di dipendenza ed è stata eliminata.  
  
 Questo errore può essere causato anche da troppe transazioni dipendenti. Qualsiasi transazione di scrittura può presentare un numero limitato di transazioni dipendenti. Ad esempio, questo errore si può verificare se tramite troppe transazioni di lettura si tenta di accettare una dipendenza dalla transazione di aggiornamento.  
  
## <a name="user-action"></a>Azione dell'utente  
 Non eseguire operazioni sulla transazione. Chiamare ROLLBACK TRAN per eseguire il rollback della transazione. Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
  
