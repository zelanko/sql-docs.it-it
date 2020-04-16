---
title: Componenti del server del motore OLAP - Documenti Microsoft
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
manager: craigg
ms.openlocfilehash: 535d1e05fc82882e0a2b5ea43ac9b2147e62338b
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388010"
---
# <a name="olap-engine-server-components"></a>Componenti del server del motore OLAP
  Il componente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] server di è l'applicazione **msmdsrv.exe,** che viene eseguita come servizio Windows. Questa applicazione è costituita da componenti di sicurezza, un componente listener XML for Analysis (XMLA), un componente di elaborazione delle query e numerosi altri componenti interni che svolgono le funzioni seguenti:

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
 Il componente listener XMLA gestisce tutte le comunicazioni XMLA tra [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e i relativi client. L'impostazione [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] `Port` di configurazione nel file msmdsrv.ini può [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] essere utilizzata per specificare una porta su cui un'istanza è in ascolto. Un valore 0 in questo file indica che [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] è in ascolto sulla porta predefinita. Se non specificato diversamente, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] userà le porte TCP predefinite seguenti:

|Porta|Descrizione|
|----------|-----------------|
|2383|Istanza predefinita [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]di .|
|2382|Redirector per altre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]istanze di .|
|Assegnata dinamicamente all'avvio del server|Istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|

 Per ulteriori informazioni, vedere [Configurare Windows Firewall per consentire l'accesso ad Analysis Services.](../../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)

## <a name="see-also"></a>Vedere anche
 Regole di denominazione degli [oggetti &#40;Analysis Services&#41;Architettura](object-naming-rules-analysis-services.md) [fisica &#40;Analysis Services - Dati multidimensionali&#41;](understanding-microsoft-olap-physical-architecture.md) Architettura logica &#40;Analysis Services - Dati [multidimensionali&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)


