---
title: Esercitazioni sulla replica | Microsoft Docs
description: Queste esercitazioni illustrano come preparare il server per la replica in SQL Server, quindi come configurare la replica transazionale e di tipo merge.
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- walkthroughs [SQL Server replication]
- replication [SQL Server], tutorials
ms.assetid: 19fbd10e-5b59-4cd0-a988-52d5d9206242
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 2706b8a72aea53ef6f7cb37399580722161a4ea4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468782"
---
# <a name="replication-tutorials"></a>Esercitazioni sulla replica
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
La replica è una soluzione avanzata per lo spostamento di dati, o di subset di dati, da un server a un altro. Per replicare dati tra server sempre connessi è possibile usare la replica transazionale. È anche possibile replicare dati tra server e client connessi saltuariamente usando la replica di tipo merge. In questo articolo sono disponibili esercitazioni che consentono di preparare più facilmente il server per la replica e di apprendere quindi come configurare sia la replica transazionale che la replica di tipo merge. 
  
Nelle esercitazioni sulla replica, "server di pubblicazione" indica il server che contiene i dati di origine sottoposti a replica. "Sottoscrittore" indica il server di destinazione. Il server di pubblicazione e il sottoscrittore possono usare la stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma questo non è un requisito. Per altre informazioni, vedere [Panoramica del modello di pubblicazione della replica](../../relational-databases/replication/publish/replication-publishing-model-overview.md).  

Queste esercitazioni usano NODE1\SQL2016 come server di pubblicazione e database di distribuzione. Usano NODE2\SQL2016 come sottoscrittore. 
  
> [!NOTE]  
> La maggior parte delle attività illustrate in queste esercitazioni possono essere eseguite a livello di programmazione. Per altre informazioni, vedere [Documentazione per gli sviluppatori di replica](../../relational-databases/replication/concepts/replication-developer-documentation.md).  
  
## <a name="replication-tutorials"></a>Esercitazioni sulla replica  
[Esercitazione: Preparare SQL Server per la replica: server di pubblicazione, server di distribuzione, sottoscrittore](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
Descrive come preparare i server in modo che la replica possa essere eseguita con privilegi minimi. È necessario completare questa esercitazione prima delle altre esercitazioni sulla replica.  
  
[Esercitazione: Configurare la replica tra due server sempre connessi (replica transazionale)](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

Descrive come configurare la replica transazionale per replicare dati tra server sempre connessi. Questa esercitazione include anche alcuni metodi per la risoluzione di alcuni problemi di base. 

  
[Esercitazione: Configurare la replica tra un server e più client per dispositivi mobili (replica di tipo merge)](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

Descrive come configurare la replica di tipo merge per lo scambio di dati tra un server e uno o più client connessi solo occasionalmente.  
  
## <a name="see-also"></a>Vedere anche  
[Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md) 

[Panoramica della replica transazionale](./transactional/transactional-replication.md) 

[Panoramica della replica di tipo merge](./merge/merge-replication.md)

