---
title: Replica di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01027aaa813cb3859dfd6d8459b7138a071c0f2d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352969"
---
# <a name="sql-server-replication"></a>Replica di SQL Server
  La replica è costituita da un set di tecnologie per la copia e la distribuzione di dati e oggetti di database da un database a un altro e la successiva sincronizzazione dei database in modo che risultino consistenti. Grazie alla replica è possibile distribuire dati a diverse posizioni e a utenti remoti o mobili tramite reti locali e WAN, connessioni remote, connessioni wireless e Internet.  
  
 La replica transazionale viene in genere utilizzata negli scenari server-server con esigenze di elevata velocità effettiva, inclusi il miglioramento delle caratteristiche di scalabilità e disponibilità, funzionalità di data warehouse e di creazione di report, integrazione di dati da più siti, integrazione di dati eterogenei e ripartizione del carico di lavoro dell'elaborazione batch. La replica di tipo merge è principalmente progettata per le applicazioni mobili o server distribuite con possibili conflitti di dati. Tra gli scenari comuni sono inclusi lo scambio di dati con utenti mobili, applicazioni POS e integrazione di dati da più siti. La replica snapshot viene utilizzata per fornire il set di dati iniziale per la replica di tipo merge o transazionale, nonché nel caso sia necessario un aggiornamento completo dei dati. Con questi tre tipi di replica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] costituisce un sistema potente e flessibile per la sincronizzazione dei dati aziendali. La replica in SQLCE 3.5 e SQLCE 4.0 è supportata sia in [!INCLUDE[win8srv](../../includes/win8srv-md.md)] sia in [!INCLUDE[win8](../../includes/win8-md.md)].  
  
 In alternativa alla replica, è possibile sincronizzare i database utilizzando Microsoft Sync Framework. Sync Framework include componenti e una API intuitiva e flessibile che facilitano la sincronizzazione fra i database di SQL Server, SQL Server Express, SQL Server Compact e SQL Azure. Sync Framework include anche classi che possono essere adattate per la sincronizzazione tra un database di SQL Server e un qualsiasi altro database compatibile con ADO.NET. Per la documentazione dettagliata dei componenti per la sincronizzazione di Sync Framework, vedere [Sincronizzazione di database](https://go.microsoft.com/fwlink/?LinkId=209079). Per una panoramica su Sync Framework, vedere la pagina relativa al [centro per sviluppatori di Microsoft Sync Framework](https://go.microsoft.com/fwlink/?LinkId=209078). Per un confronto tra Sync Framework e la replica di tipo merge, vedere [Panoramica sulla sincronizzazione di database](https://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  
 **Ricerca di contenuto per area**  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") [novità](what-s-new-replication.md)  
  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") [compatibilità con le versioni precedenti](replication-backward-compatibility.md)  
  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") [attività e funzionalità di replica](replication-features-and-tasks.md)  
  
 ![Icona cartella File piccola](../../integration-services/media/filefolder-small.gif "icona cartella File piccola") [riferimento tecnico](technical-reference-replication.md)  
  
  
