---
title: Proprietà SQL Server Agent (pagina Sistema processi) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8dceeba78e639ecbe2fd81fbdb1021293e75cf8a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63246074"
---
# <a name="sql-server-agent-properties-job-system-page"></a>Proprietà SQL Server Agent (pagina Sistema processi)
  Utilizzare questa pagina per visualizzare e modificare il modo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui il servizio Agent gestisce i processi.  
  
## <a name="options"></a>Opzioni  
 **Intervallo di timeout di arresto (in secondi)**  
 Consente di specificare il numero di secondi di attesa del completamento dei processi prima che questi vengano chiusi da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se il processo è ancora in esecuzione dopo la scadenza dell'intervallo specificato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent lo arresterà in modo forzato.  
  
 **Usare un account proxy non amministratore**  
 Imposta un account proxy non amministratore per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive supportano più proxy, pertanto questa opzione è applicabile solo quando si gestiscono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versioni di Agent [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]precedenti a.  
  
 **Nome utente**  
 Digitare il nome dell'utente per l'account proxy non amministratore. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta più proxy, pertanto questa opzione è applicabile unicamente quando si gestiscono versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 **Password**  
 Digitare la password dell'utente per l'account proxy non amministratore. 
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive supportano più proxy, pertanto questa opzione è applicabile unicamente quando si gestiscono le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent precedenti a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 **Dominio**  
 Digitare il dominio dell'utente per l'account proxy non amministratore. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta più proxy, pertanto questa opzione è applicabile unicamente quando si gestiscono versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di processi](implement-jobs.md)  
  
  
