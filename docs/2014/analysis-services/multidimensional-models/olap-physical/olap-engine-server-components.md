---
title: Componenti del server del motore OLAP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- ports [Analysis Services]
- XML/A listener
- server architecture [Analysis Services]
ms.assetid: 5193c976-9dcd-459c-abba-8c3c44e7a7f2
author: minewiskan
ms.author: owend
ms.openlocfilehash: b60d721a69213ad52536830b49b40d6bb82a3811
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545923"
---
# <a name="olap-engine-server-components"></a>Componenti del server del motore OLAP
  Il componente server di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] è l'applicazione **msmdsrv.exe** , che viene eseguita come servizio Windows. Questa applicazione è costituita da componenti di sicurezza, un componente listener XML for Analysis (XMLA), un componente di elaborazione delle query e numerosi altri componenti interni che svolgono le funzioni seguenti:

-   Analisi di istruzioni ricevute dai client

-   Gestione di metadati

-   Gestione di transazioni

-   Elaborazione di calcoli

-   Archiviazione di dati relativi a dimensioni e celle

-   Creazione di aggregazioni

-   Pianificazione di query

-   Memorizzazione di oggetti nella cache

-   Gestione di risorse del server

## <a name="architectural-diagram"></a>Diagramma dell'architettura
 Un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] viene eseguita come un servizio autonomo e la comunicazione con il servizio avviene tramite XML for Analysis (XMLA), usando HTTP o TCP. AMO è un livello tra l'applicazione utente e l'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Questo livello fornisce accesso agli oggetti amministrativi [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. AMO è una libreria di classi che accetta i comandi da un'applicazione client e li converte in messaggi XMLA per l'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . AMO presenta oggetti dell'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] come classi all'applicazione dell'utente finale, coi membri dei metodi che eseguono i comandi e i membri delle proprietà che utilizzano i dati per gli oggetti di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .

 Nell'illustrazione seguente sono mostrati i componenti dell'architettura [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], inclusi tutti gli elementi principali che sono in esecuzione all'interno dell'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e tutti i componenti dell'utente che interagiscono con essa. L'illustrazione mostra anche che il solo modo di accedere all'istanza è tramite il listener di XML for Analysis (XMLA), utilizzando HTTP o TCP.

 ![Diagramma dell'architettura di sistema di Analysis Services](../../../analysis-services/dev-guide/media/analysisservicessystemarchitecture.gif "Diagramma dell'architettura di sistema di Analysis Services")

## <a name="xmla-listener"></a>Listener XMLA
 Il componente listener XMLA gestisce tutte le comunicazioni XMLA tra [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e i relativi client. L' [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] `Port` impostazione di configurazione nel file di msmdsrv.ini può essere utilizzata per specificare una porta su cui un'istanza è in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ascolto. Un valore 0 in questo file indica che [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] è in ascolto sulla porta predefinita. Se non specificato diversamente, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] userà le porte TCP predefinite seguenti:

|Porta|Descrizione|
|----------|-----------------|
|2383|Istanza predefinita di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|
|2382|Redirector per altre istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|
|Assegnata dinamicamente all'avvio del server|Istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|

 Per altri dettagli, vedere [configurare la Windows Firewall per consentire l'accesso Analysis Services](../../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) .

## <a name="see-also"></a>Vedere anche
 [Le regole di denominazione degli oggetti &#40;Analysis Services&#41;](object-naming-rules-analysis-services.md) [architettura fisica &#40;Analysis Services-Dati multidimensionali](understanding-microsoft-olap-physical-architecture.md)&#41;[architettura logica &#40;Analysis Services-Dati multidimensionali](../olap-logical/understanding-microsoft-olap-logical-architecture.md)&#41;


