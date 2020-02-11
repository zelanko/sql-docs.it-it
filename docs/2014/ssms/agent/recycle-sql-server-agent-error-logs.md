---
title: Ricicla log degli errori di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0654dcc83e757751ac055192775c0ee958f26e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62753068"
---
# <a name="recycle-sql-server-agent-error-logs"></a>Ricicla log degli errori di SQL Server Agent
  Utilizzare questa pagina per riciclare i [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log degli errori di Agent. Il riciclo dei log chiude il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e avvia un nuovo registro errori senza riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Si noti che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantiene gli ultimi nove log degli errori. Se esistono già nove log degli errori, il riciclo causa l'eliminazione del log degli errori meno recente da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="see-also"></a>Vedere anche  
 [Log degli errori di SQL Server Agent](sql-server-agent-error-log.md)  
  
  
