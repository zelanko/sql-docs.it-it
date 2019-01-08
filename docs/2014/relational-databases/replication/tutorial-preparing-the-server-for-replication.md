---
title: 'Esercitazione: Preparazione del Server per la replica | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e82c71834a2d41a7620f549bc6335fa15df84bf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813993"
---
# <a name="tutorial-preparing-the-server-for-replication"></a>Esercitazione: Preparazione del server per la replica
  È importante pianificare la sicurezza prima di configurare la topologia di replica. In questa esercitazione viene illustrato come proteggere la topologia di replica e come configurare la distribuzione, ovvero il primo passaggio nella replica dei dati. È necessario completare questa esercitazione prima delle altre esercitazioni sulla replica.  
  
> [!NOTE]  
>  Per eseguire in modo protetto la replica dei dati tra server, è consigliabile seguire le indicazioni riportate in [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md).  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 In questa esercitazione verranno descritte le procedure per preparare i server in modo che la replica possa essere eseguita in modo protetto con privilegi minimi. Nella prima lezione viene illustrato come creare gli account di servizio Windows utilizzati per l'esecuzione degli agenti di replica. Nella seconda lezione viene illustrato come configurare la cartella utilizzata per creare e archiviare gli snapshot di pubblicazione. Nella terza lezione viene illustrato come configurare la distribuzione e impostare le autorizzazioni.  
  
## <a name="requirements"></a>Requisiti  
 Questa esercitazione è destinata agli utenti esperti nelle operazioni di database fondamentali ma con una limitata conoscenza della replica.  
  
 Per utilizzare l'esercitazione è necessario che nel sistema siano installati i componenti seguenti:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita.  
  
 **Tempo stimato per completare questa esercitazione: 30 minuti.**  
  
## <a name="lessons-in-this-tutorial"></a>Lezioni dell'esercitazione  
  
-   [Lezione 1: Creazione di Windows account per la replica](lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lezione 2: Preparazione della cartella Snapshot](lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lezione 3: Configurazione della distribuzione](lesson-3-configuring-distribution.md)  
  
 [Avviare l'esercitazione](lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](configure-distribution.md)   
 [Sicurezza e protezione #40;replica&#41;](security/security-and-protection-replication.md)  
  
  
