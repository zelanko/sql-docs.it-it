---
title: Amministrare più server tramite server di gestione centrale
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
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
ms.custom: seo-lt-2019
ms.openlocfilehash: a2e2da55bd04ba29cf1c6ef81757488f8d50fd24
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74055613"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Amministrare più server tramite server di gestione centrale
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile amministrare più server designando server di gestione centrale e creando gruppi di server.  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>Che cos’è un server di gestione centrale e cosa sono i gruppi di server?  
 Un'istanza di SQL Server definita come server di gestione centrale gestisce i gruppi di server che contengono le informazioni sulla connessione per una o più istanze. Le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] e i criteri della gestione basata su criteri possono essere eseguiti contemporaneamente in più gruppi di server. È inoltre possibile visualizzare i file di log in istanze gestite tramite un server di gestione centrale. 
 
 Un server di gestione centrale è essenzialmente un repository centrale contenente un elenco di server gestiti. Le versioni precedenti a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] non possono essere designate come server di gestione centrale.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] le istruzioni possono inoltre essere eseguite su gruppi di server locali nella finestra Server registrati.  
  
## <a name="create-central-management-server-and-server-groups"></a>Creare un server di gestione centrale e gruppi di server 
 Per creare un server di gestione centrale e gruppi di server, usare la finestra **Server registrati** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Notare che il server di gestione centrale non può essere un membro di uno dei gruppi che gestisce. 
 
 Per altre informazioni su come creare server di gestione centrale e gruppi di server, vedere [Creazione di un server di gestione centrale e di un gruppo di server &#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
