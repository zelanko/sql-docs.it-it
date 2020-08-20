---
description: Nuovo profilo agente
title: Nuovo profilo agente | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: b8bfc5c942c10d141ee57793fa6e7a68fcd30513
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470189"
---
# <a name="new-agent-profile"></a>Nuovo profilo agente
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La finestra di dialogo **Nuovo profilo agente** consente di creare un nuovo profilo. I nuovi profili sono sempre basati su profili esistenti, ma possono essere modificati in base ai requisiti delle applicazioni. Dopo aver creato un profilo, è possibile applicarlo a processi agente esistenti e creati in un secondo momento nella finestra di dialogo **Profili agente** . I valori dei parametri degli agenti possono essere modificati nella finestra di dialogo \<**AgentProfileName>Proprietà **.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di immettere un nome per il profilo.  
  
 **Descrizione**  
 Consente di immettere una descrizione per il profilo.  
  
 **Parametro**  
 I parametri degli agenti inclusi nel profilo. Il profilo su cui è basato il nuovo profilo non contiene necessariamente un valore per ogni parametro. Per visualizzare tutti i parametri validi per un determinato agente, deselezionare la casella di controllo **Mostra solo i parametri utilizzati in questo profilo** . Per una descrizione dei singoli parametri, vedere:  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [Agente lettura log repliche](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Agente di lettura coda repliche](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 **Valore predefinito**  
 Il valore predefinito per ogni parametro degli agenti.  
  
 **Valore**  
 Il valore specificato per il parametro nel profilo su cui è basato il nuovo profilo. Modificare questo campo per qualsiasi valore di parametro che si desidera modificare.  
  
 **Mostra solo i parametri utilizzati in questo profilo**  
 Deselezionare questa casella di controllo per mostrare tutti i parametri validi per un determinato agente.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare i profili agenti di replica](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Profili degli agenti di replica](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
