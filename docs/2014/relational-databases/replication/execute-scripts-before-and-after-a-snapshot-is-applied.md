---
title: Eseguire script prima e dopo aver applicato uno Snapshot (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f74130040c7344f881775b75718e1513f8879636
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754043"
---
# <a name="execute-scripts-before-and-after-a-snapshot-is-applied-sql-server-management-studio"></a>Esecuzione di script prima e dopo l'applicazione di uno snapshot (SQL Server Management Studio)
  Specificare uno script facoltativo da eseguire prima o dopo l'applicazione dello snapshot nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**. Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Queste opzioni non sono disponibili se l'opzione **Formato snapshot** è impostata su **Carattere**.  
  
### <a name="to-execute-a-script-before-or-after-a-snapshot-is-applied"></a>Per eseguire uno script prima o dopo l'applicazione di uno snapshot  
  
1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**:  
  
    -   Per specificare uno script da eseguire prima dell'applicazione dello snapshot, fare clic su **Sfoglia** per passare allo script oppure immettere un percorso per lo script nella casella di testo **Prima di applicare lo snapshot, esegui lo script seguente** .  
  
        > [!NOTE]  
        >  È necessario che l'agente di distribuzione o l'agente di merge disponga delle autorizzazioni di lettura per la directory specificata. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\script\scriptpersonali.sql.  
  
    -   Per specificare uno script da eseguire dopo l'applicazione dello snapshot, fare clic su **Sfoglia** per passare allo script oppure immettere un percorso UNC per lo script nella casella di testo **Dopo l'applicazione dello snapshot, esegui lo script seguente** .  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà dello snapshot &#40;programmazione Transact-SQL della replica&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Modificare le proprietà di pubblicazioni e articoli](publish/change-publication-and-article-properties.md)   
 [Eseguire gli script prima e dopo l'applicazione dello snapshot](execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)  
  
  
