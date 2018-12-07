---
title: Specificare la posizione predefinita degli snapshot (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 3aa167df2f75b42cf5612b725cbfd368f4dc4407
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519946"
---
# <a name="specify-the-default-snapshot-location-sql-server-management-studio"></a>Impostazione della posizione predefinita degli snapshot (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Specificare la posizione predefinita degli snapshot nella pagina **Cartella snapshot** della Configurazione guidata distribuzione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md). Se si crea una pubblicazione su un server non configurato come server di distribuzione, specificare una posizione predefinita degli snapshot nella pagina **Cartella snapshot** della Creazione guidata nuova pubblicazione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Creare una pubblicazione](../../relational-databases/replication/publish/create-a-publication.md).  
  
 Modificare la posizione predefinita degli snapshot nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>**. Per altre informazioni, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md). Impostare la cartella snapshot per ogni pubblicazione nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione**. Per altre informazioni, vedere [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>Per modificare la posizione predefinita degli snapshot  
  
1.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>** fare clic sul pulsante delle proprietà (**...**) per il server di pubblicazione di cui si vuole modificare la posizione predefinita degli snapshot.  
  
2.  Nella finestra di dialogo **Proprietà server di pubblicazione - \<Server di pubblicazione>** immettere un valore per la proprietà **Cartella snapshot predefinita**.  
  
    > [!NOTE]  
    >  L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Posizioni alternative della cartella snapshot](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Inizializzare una sottoscrizione con uno snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
