---
title: Compatibilità con le versioni precedenti della replica | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, backward compatibility
- backward compatibility [SQL Server replication]
- merge replication backward compatibility [SQL Server replication]
- replication [SQL Server], backward compatibility
- backward compatibility [SQL Server], replication
- snapshot replication [SQL Server], backward compatibility
- compatibility [SQL Server replication]
ms.assetid: 091c51dc-8b32-4b4f-847e-b317456c8394
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6b21412bfb6555dbe9c45d411f0b1e7292e79e2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046705"
---
# <a name="replication-backward-compatibility"></a>Compatibilità con le versioni precedenti della replica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

È importante approfondire la compatibilità con le versioni precedenti se si esegue un aggiornamento o se si usa più di una versione di SQL Server in una topologia di replica. 

Le regole generali sono le seguenti: 

-   La versione del server di distribuzione è indifferente, purché superiore o uguale alla versione del server di pubblicazione (in molti casi l'istanza del server di distribuzione è la stessa del server di pubblicazione).    
-   La versione del server di pubblicazione è indifferente, purché inferiore o uguale alla versione del server di distribuzione.    
-   La versione del Sottoscrittore dipende dal tipo di pubblicazione:    
    - La versione di un Sottoscrittore per una pubblicazione transazionale può essere una versione qualsiasi all'interno di un intervallo di due versioni, in base alla versione del server di pubblicazione. Ad esempio: un server di pubblicazione SQL Server 2012 (11.x) può avere sottoscrittori SQL Server 2014 (12.x) e SQL Server 2016 (13.x). Un server di pubblicazione SQL Server 2016 (13.x) può avere sottoscrittori SQL Server 2014 (12.x) e SQL Server 2012 (11.x).     
    - Un sottoscrittore per una pubblicazione di tipo merge può avere una versione inferiore o uguale alla versione del server di pubblicazione supportata nel ciclo di supporto del ciclo di vita delle versioni.  


## <a name="replication-matrix"></a>Matrice di replica
[!INCLUDE[repl matrix](../../includes/replication-compat-matrix.md)]


## <a name="additional-resources"></a>Risorse aggiuntive
 [Funzionalità deprecate nella replica di SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)  
 Funzionalità di replica mantenute in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per la compatibilità con le versioni precedenti, ma che verranno rimosse in una delle prossime versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Modifiche di rilievo alla replica di SQL Server](../../relational-databases/replication/breaking-changes-in-sql-server-replication.md)  
 Modifiche a funzionalità di replica che possono richiedere modifiche alle applicazioni. 

 [Aggiornare database replicati](../../database-engine/install-windows/upgrade-replicated-databases.md)  
 Procedure e considerazioni sull'aggiornamento di istanze di SQL Server appartenenti a una topologia di replica. 
  
  
