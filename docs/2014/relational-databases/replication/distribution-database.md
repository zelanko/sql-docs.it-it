---
title: Database di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.distributiondatabase.f1
ms.assetid: 5b42a083-7a11-41d8-9e3f-320c7c907237
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 283fd67d14d57c3d1d5d60dd9d8de2a159ca6d5e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52752423"
---
# <a name="distribution-database"></a>Database di distribuzione
  Nel database di distribuzione vengono archiviati i metadati e i dati di cronologia relativi a tutti i tipi di replica, nonché le transazioni per la replica transazionale.  
  
 In molti casi, è sufficiente un singolo database di distribuzione. Tuttavia, nel caso in cui più server di pubblicazione utilizzino un unico server di distribuzione, valutare l'opportunità di creare un database di distribuzione per ogni server di pubblicazione. in modo da garantire che il flusso di dati di ogni database di distribuzione risulti distinto. È possibile specificare un database di distribuzione per il server di distribuzione utilizzando la Configurazione guidata distribuzione. Se necessario, specificare database di distribuzione aggiuntivi nella finestra di dialogo **Proprietà server di distribuzione** .  
  
## <a name="options"></a>Opzioni  
 **Nome database di distribuzione**  
 Consente di immettere un nome per il database di distribuzione. Il nome predefinito del database di distribuzione è 'distribution'. Se si specifica un nome, questo può avere una lunghezza massima di 128 caratteri, deve essere univoco nell'ambito di un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e conforme alle regole per gli identificatori. Per altre informazioni, vedere [Identificatori del database](../databases/database-identifiers.md).  
  
 **Cartella per il file del database di distribuzione** e **Cartella per il file di log del database di distribuzione**  
 Immettere il percorso del database di distribuzione e dei file di log. I percorsi devono fare riferimento a dischi locali del server di distribuzione e iniziare con una lettera di unità locale seguita da due punti, ad esempio C:. Le lettere di unità mappate e i percorsi di rete non sono consentiti.  
  
> [!NOTE]  
>  è possibile ridurre il tempo necessario per la scrittura di transazioni e ottenere un miglioramento delle prestazioni della replica inserendo il log di distribuzione in un'unità disco distinta da quella del database di distribuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](configure-distribution.md)   
 [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md)  
  
  
