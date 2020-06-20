---
title: Nuovo profilo agente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0fcdca4d57b21855a959a876c0c9c9344487046b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060673"
---
# <a name="new-agent-profile"></a>Nuovo profilo agente
  La finestra di dialogo **Nuovo profilo agente** consente di creare un nuovo profilo. I nuovi profili sono sempre basati su profili esistenti, ma possono essere modificati in base ai requisiti delle applicazioni. Dopo aver creato un profilo, è possibile applicarlo a processi agente esistenti e creati in un secondo momento nella finestra di dialogo **Profili agente** . I valori dei parametri dell'agente possono essere modificati nella finestra di \<**AgentProfileName> dialogo Proprietà * *.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di immettere un nome per il profilo.  
  
 **Descrizione**  
 Consente di immettere una descrizione per il profilo.  
  
 **Parametro**  
 I parametri degli agenti inclusi nel profilo. Il profilo su cui è basato il nuovo profilo non contiene necessariamente un valore per ogni parametro. Per visualizzare tutti i parametri validi per un determinato agente, deselezionare la casella di controllo **Mostra solo i parametri utilizzati in questo profilo** . Per una descrizione dei singoli parametri, vedere:  
  
-   [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
-   [Agente lettura log repliche](agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](agents/replication-distribution-agent.md)  
  
-   [Replication Merge Agent](agents/replication-merge-agent.md)  
  
-   [Agente di lettura coda repliche](agents/replication-queue-reader-agent.md)  
  
 **Valore predefinito**  
 Il valore predefinito per ogni parametro degli agenti.  
  
 **Valore**  
 Il valore specificato per il parametro nel profilo su cui è basato il nuovo profilo. Modificare questo campo per qualsiasi valore di parametro che si desidera modificare.  
  
 **Mostra solo i parametri utilizzati in questo profilo**  
 Deselezionare questa casella di controllo per mostrare tutti i parametri validi per un determinato agente.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare i profili agenti di replica](agents/work-with-replication-agent-profiles.md)   
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)   
 [Profili degli agenti di replica](agents/replication-agent-profiles.md)  
  
  
