---
title: Proprietà SQL Server Agent (pagina Cronologia) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10796dde3513e5c4b7970d1e4f6c4eedcad3c6c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245602"
---
# <a name="sql-server-agent-properties-history-page"></a>Proprietà SQL Server Agent (pagina Cronologia)
  Utilizzare questa pagina per visualizzare e modificare le impostazioni per la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestione del log della cronologia del servizio Agent.  
  
## <a name="options"></a>Opzioni  
 **Limitare le dimensioni del log di cronologia processi**  
 Consente di impostare limiti sulla quantità di informazioni sulla cronologia processo che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantiene nel log.  
  
 **Dimensioni massime log cronologia processi (righe)**  
 Consente di impostare il numero massimo di righe che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantiene nel log. Quando il log raggiunge dimensioni tali da contenere questo numero di righe, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent rimuove le righe meno recenti per consentire l'inserimento delle nuove.  
  
 **Numero massimo di righe di cronologia per processo**  
 Consente di impostare il numero massimo di righe che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantiene per ogni processo. Quando la cronologia di un determinato processo si estende fino a contenere questo numero di righe, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent consente di rimuovere le righe meno recenti per consentire l'inserimento delle nuove.  
  
 **Rimuovi cronologia dell'agente**  
 Viene indicato che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent consentirà di rimuovere le voci presenti nel log da più tempo rispetto a quanto specificato. Si tratta di un'esecuzione singola che consente di rimuovere la cronologia. Se è necessario un processo ricorrente, creare e pianificare un piano di manutenzione con un processo di pulizia.  
  
 **Più vecchio di**  
 Consente di impostare il periodo di tempo per cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent manterrà le voci.  
  
## <a name="see-also"></a>Vedere anche  
 [Log degli errori di SQL Server Agent](sql-server-agent-error-log.md)  
  
  
