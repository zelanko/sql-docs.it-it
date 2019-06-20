---
title: Amministrare più server tramite server di gestione centrale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f47eec543c21e74565d750035d20fbcee9baa82e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62877311"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Amministrare più server tramite server di gestione centrale
  È possibile amministrare più server designando server di gestione centrale e creando gruppi di server.  
  
## <a name="benefits-of-central-management-servers-and-server-groups"></a>Vantaggi del server di gestione centrale e di gruppi di server  
 Un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] definita come server di gestione centrale gestisce i gruppi di server che contengono le informazioni sulla connessione per una o più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] e i criteri della gestione basata su criteri possono essere eseguiti contemporaneamente in più gruppi di server. È inoltre possibile visualizzare i file di log di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in istanze gestite tramite un server di gestione centrale. Le versioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] non possono essere designate come server di gestione centrale.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] le istruzioni possono inoltre essere eseguite su gruppi di server locali nella finestra Server registrati.  
  
### <a name="related-tasks"></a>Attività correlate  
 Per creare un server di gestione centrale e gruppi di server, usare la finestra **Server registrati** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Notare che il server di gestione centrale non può essere un membro di uno dei gruppi che gestisce. Per altre informazioni su come creare server di gestione centrale e gruppi di server, vedere [Creazione di un server di gestione centrale e di un gruppo di server &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
