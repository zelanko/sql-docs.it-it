---
title: Specificare la posizione predefinita degli snapshot (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], default locations
- default snapshot locations
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd41dabe1554bc3f80adc4fdb6d8433f8aac9e7f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807333"
---
# <a name="specify-the-default-snapshot-location-sql-server-management-studio"></a>Impostazione della posizione predefinita degli snapshot (SQL Server Management Studio)
  Specificare la posizione predefinita degli snapshot nella pagina **Cartella snapshot** della Configurazione guidata distribuzione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md). Se si crea una pubblicazione su un server non configurato come server di distribuzione, specificare una posizione predefinita degli snapshot nella pagina **Cartella snapshot** della Creazione guidata nuova pubblicazione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Creare una pubblicazione](publish/create-a-publication.md).  
  
 Modificare la posizione predefinita degli snapshot nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>**. Per altre informazioni, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md). Impostare la cartella snapshot per ogni pubblicazione nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione**. Per altre informazioni, vedere [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>Per modificare la posizione predefinita degli snapshot  
  
1.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>** fare clic sul pulsante delle proprietà (**...**) per il server di pubblicazione di cui si vuole modificare la posizione predefinita degli snapshot.  
  
2.  Nella finestra di dialogo **Proprietà server di pubblicazione - \<Server di pubblicazione>** immettere un valore per la proprietà **Cartella snapshot predefinita**.  
  
    > [!NOTE]  
    >  L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Posizioni alternative della cartella snapshot](alternate-snapshot-folder-locations.md)   
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)  
  
  
