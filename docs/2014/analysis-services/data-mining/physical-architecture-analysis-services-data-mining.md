---
title: Architettura fisica (Analysis Services-Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- server architecture [Analysis Services]
- architecture [Analysis Services]
ms.assetid: 25eeecf0-6e85-4527-b94d-5503d27edaed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81c9ee3db0a05107913d3b75fba20ebe8607f941
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083202"
---
# <a name="physical-architecture-analysis-services---data-mining"></a>Architettura fisica (Analysis Services – Data mining)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa componenti server e client per fornire data mining funzionalità per le applicazioni business intelligence:  
  
-   Il componente server viene implementato come un servizio di Microsoft Windows. È possibile avere più istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sullo stesso computer, ognuna delle quali viene implementata come istanza separata del servizio di Windows.  
  
-   I client comunicano con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante lo standard pubblico XML for Analysis (XMLA), un protocollo basato su SOAP per l'esecuzione di comandi e la ricezione di risposte che viene esposto come un servizio Web. Tramite XMLA vengono inoltre offerti modelli a oggetti client a cui è possibile accedere usando un provider gestito, ad esempio ADOMD.NET, o un provider OLE DB nativo.  
  
-   I comandi di query possono essere eseguiti utilizzando il linguaggio DMX (Data Mining Extensions), un linguaggio di query standard orientato al data mining, e il linguaggio ASSL (Analysis Services Scripting Language), che consente di gestire gli oggetti di database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="architectural-diagram"></a>Diagramma dell'architettura  
 Un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene eseguita come un servizio autonomo e la comunicazione con il servizio avviene tramite XML for Analysis (XMLA), usando HTTP o TCP.  
  
 AMO è un livello tra l'applicazione utente e l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che fornisce accesso agli oggetti amministrativi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . AMO è una libreria di classi che accetta i comandi da un'applicazione client e li converte in messaggi XMLA per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . AMO presenta oggetti dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] come classi all'applicazione dell'utente finale, coi membri dei metodi che eseguono i comandi e i membri delle proprietà che utilizzano i dati per gli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Nell'illustrazione seguente sono illustrati i componenti dell'architettura [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , inclusi i servizi nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e i componenti utente che interagiscono con essa.  
  
 L'illustrazione mostra inoltre che il solo modo di accedere all'istanza è tramite il listener di XML for Analysis (XMLA), utilizzando HTTP o TCP.  
  
> [!WARNING]  
>  DSO è deprecato. Non utilizzare DSO per sviluppare soluzioni.  
  
 ![Diagramma dell'architettura di sistema di Analysis Services](../dev-guide/media/analysisservicessystemarchitecture.gif "Diagramma dell'architettura di sistema di Analysis Services")  
  
## <a name="server-configuration"></a>Configurazione server  
 Un'istanza del server è in grado di supportare più database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ognuno con la propria istanza del servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che risponde alle richieste client ed elabora oggetti.  
  
 È necessario installare istanze separate se si desidera utilizzare sia modelli tabulari sia modelli di data mining e/o multidimensionali. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta l'installazione side-by-side di istanze in esecuzione in modalità tabulare, che usa il motore di analisi in memoria xVelocity (VertiPaq), e istanze in esecuzione in una delle configurazioni OLAP, MOLAP o ROLAP convenzionali. Per altre informazioni, vedere [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Per tutte le comunicazioni tra un client e il server Analysis Services viene utilizzato XMLA, un protocollo indipendente da piattaforma e linguaggio. Quando viene ricevuta una richiesta da un client, Analysis Services determina se tale richiesta è correlata a OLAP o al data mining, quindi la indirizza nel modo appropriato. Per altre informazioni sui componenti server, vedere [Componenti del server del motore OLAP](../multidimensional-models/olap-physical/olap-engine-server-components.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Architettura logica &#40;Analysis Services-&#41;di data mining](logical-architecture-analysis-services-data-mining.md)  
  
  
