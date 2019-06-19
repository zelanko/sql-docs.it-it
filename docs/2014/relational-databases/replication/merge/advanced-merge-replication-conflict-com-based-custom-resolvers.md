---
title: Sistemi di risoluzione personalizzati basati su COM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: 94195797-ad7a-4962-a8e3-b259cd13aa38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 27d5be264fc6e6033997babb4a7aac1e8271a39d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63066309"
---
# <a name="com-based-custom-resolvers"></a>COM-Based Custom Resolvers
  I sistemi di risoluzione personalizzati offrono una flessibilità maggiore rispetto al meccanismo di risoluzione predefinito e possono implementare la logica di business richiesta dalle applicazioni che utilizzano i dati replicati. Un sistema di risoluzione personalizzato basato su COM è una libreria di collegamento dinamico (DLL, dynamic-link library) che implementa l'interfaccia COM **ICustomResolver** con i relativi metodi e proprietà e altre interfacce e definizioni di tipi di supporto progettate appositamente per la risoluzione dei conflitti.  
  
> [!NOTE]  
>  Se possibile, è consigliabile utilizzare un gestore della logica di business anziché un sistema di risoluzione personalizzato basato su COM. Per altre informazioni sui gestori della logica di business, vedere [Eseguire logiche di business durante la sincronizzazione di tipo merge](execute-business-logic-during-merge-synchronization.md).  
  
 Per compilare un sistema di risoluzione COM personalizzato, è possibile utilizzare la libreria dei tipi inclusa in replrec.dll. Per impostazione predefinita, questa libreria è installata in [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
 Prima di creare un sistema di risoluzione COM personalizzato, è necessario stabilire i fattori seguenti:  
  
-   I tipi di modifiche alle righe che si desidera risolvere, ad esempio le operazioni di aggiornamento, inserimento ed eliminazione oppure se il sistema di risoluzione deve essere richiamato durante le operazioni di caricamento o di download delle modifiche di tipo merge o durante entrambi i processi. È possibile specificare un tipo di modifica, tutte le modifiche o qualsiasi combinazione di modifiche. Il sistema di risoluzione dei conflitti del processo di merge predefinito gestisce tutti i conflitti non risolti da un sistema di risoluzione personalizzato.  
  
-   Se utilizzare il rilevamento a livello di colonna per la risoluzione dei conflitti. Quando si utilizza il rilevamento a livello di colonna, vengono contrassegnati come conflitti solo i dati delle colonne in cui si verifica un conflitto. Negli altri casi i dati vengono uniti. I conflitti tuttavia vengono risolti in base alle stesse modalità utilizzate per il rilevamento a livello di riga, ovvero il processo che prevale sovrascrive l'intera riga di dati. I dati tuttavia possono essere una combinazione dei valori del server di pubblicazione e dei Sottoscrittori oppure valori alterati che non provengono né dal server di pubblicazione, né dai Sottoscrittori. Per altre informazioni, vedere [Rilevare e risolvere i conflitti tra repliche di tipo merge](advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 Per implementare un sistema di risoluzione dei conflitti personalizzato basato su COM, vedere [Implementazione di un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge](../implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
 Un sistema di risoluzione personalizzato viene specificato per un articolo, non per un'intera pubblicazione. Lo stesso sistema può essere utilizzato con più articoli, ma la logica nei sistemi di risoluzione personalizzati è spesso specifica di una particolare tabella. Se la tabella utilizzata nell'articolo viene modificata dopo la creazione del sistema, ad esempio rinominando la colonna utilizzata nella risoluzione dei conflitti, potrebbe essere necessario modificare e ricompilare il sistema di risoluzione personalizzato.  
  
 Per specificare un sistema di risoluzione personalizzato, vedere [Impostazione di un sistema di risoluzione dei conflitti dell'articolo di merge](../publish/specify-a-merge-article-resolver.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge](advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Microsoft COM-Based Resolvers](advanced-merge-replication-conflict-com-based-resolvers.md)  
  
  
