---
title: Rilevare e risolvere i conflitti tra repliche di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- conflict resolution [SQL Server replication]
- viewing merge replication conflicts
- resolving merge replication conflicts
- articles [SQL Server replication], conflict resolution
- merge replication conflict resolution [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 0d033c76-e8c9-4e35-ab95-4d335abb18c1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8d29ccc697bb34b0872f0a75b0b03c7db82faea4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786053"
---
# <a name="detect-and-resolve-merge-replication-conflicts"></a>Rilevamento e risoluzione di conflitti tra repliche di tipo merge
  Se un server di pubblicazione e un Sottoscrittore sono connessi e viene eseguita la sincronizzazione, l'agente di merge rileva l'eventuale presenza di conflitti. Se si verificano conflitti, l'agente di merge utilizza un sistema di risoluzione dei conflitti per determinare quali dati verranno accettati e propagati agli altri siti.  
  
> [!NOTE]  
>  Sebbene un Sottoscrittore esegua la sincronizzazione con il server di pubblicazione, i conflitti in genere si verificano tra gli aggiornamenti effettuati in diversi Sottoscrittori, anziché tra gli aggiornamenti effettuati in un Sottoscrittore e nel server di pubblicazione.  
  
 La replica di tipo merge prevede diversi metodi per rilevare e risolvere i conflitti. Il metodo predefinito è appropriato alla maggior parte delle applicazioni:  
  
-   Se si verifica un conflitto tra un server di pubblicazione e un Sottoscrittore, la modifica nel server di pubblicazione viene confermata e quella nel Sottoscrittore viene ignorata.  
  
-   Se si verifica un conflitto tra due Sottoscrittori che utilizzano sottoscrizioni client (tipo predefinito per le sottoscrizioni pull), verrà confermata la modifica del primo Sottoscrittore che eseguirà la sincronizzazione con il server di pubblicazione e la modifica del secondo Sottoscrittore verrà ignorata. Per informazioni sulla scelta delle sottoscrizioni client e server, vedere [Specificare una sottoscrizione di tipo merge e la priorità per la risoluzione dei conflitti &#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
-   Se si verifica un conflitto tra due Sottoscrittori che utilizzano sottoscrizioni server (tipo predefinito per le sottoscrizioni push), verrà confermata la modifica del Sottoscrittore con valore di priorità più alto e la modifica del secondo Sottoscrittore verrà ignorata. Se i valori di priorità sono uguali, verrà confermata la modifica del primo Sottoscrittore che eseguirà la sincronizzazione con il server di pubblicazione.  
  
 Per ulteriori informazioni sul rilevamento e la risoluzione dei conflitti per la replica di tipo merge, vedere [Advanced Merge Replication Conflict Detection and Resolution](advanced-merge-replication-conflict-detection-and-resolution.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni degli articoli per la replica di tipo merge](article-options-for-merge-replication.md)   
 [Sottoscrivere le pubblicazioni](../subscribe-to-publications.md)  
  
  
