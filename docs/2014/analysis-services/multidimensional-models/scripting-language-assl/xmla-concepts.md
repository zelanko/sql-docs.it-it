---
title: Concetti XMLA | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, concepts
ms.assetid: 816183a7-d2f7-4e14-8e5b-2a4c1798fbc1
author: minewiskan
ms.author: owend
ms.openlocfilehash: b2e18917b56d40f8b813ba10083cc1b408e51a98
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545658"
---
# <a name="xmla-concepts"></a>Concetti XMLA
  Lo standard aperto XMLA (XML for Analysis) supporta l’accesso a origini dati che risiedono sul World Wide Web. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementa XMLA per la specifica XMLA 1,1.  
  
 XML for Analysis (XMLA) è protocollo XML basato su SOAP (Simple Object Access Protocol), progettato in modo specifico per accedere a tutti i dati di qualsiasi origine dati multidimensionale standard disponibile sul Web. XMLA elimina inoltre la necessità di distribuire un componente client che espone Component Object Model (COM) o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] interfacce di .NET Framework. XMLA è ottimizzato per Internet, dove i round trip al server sono costosi in termini di tempo e risorse e quando le connessioni con stato a un'origine dati possono limitare le connessioni utente nel server.  
  
 XMLA è il protocollo nativo per [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , utilizzato per tutte le interazioni tra un'applicazione client e un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] supporta completamente XML for Analysis 1.1 e fornisce anche estensioni per supportare la gestione di metadati, la gestione della sessione e le funzionalità di blocco. Sia la libreria AMO (Analysis Management Objects) che ADOMD.NET utilizzano il protocollo XMLA quando comunicando con un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="handling-xmla-communications"></a>Gestione di comunicazioni XMLA  
 Lo standard aperto XMLA descrive due metodi generalmente accessibili, ovvero `Discover` e `Execute`. Tali metodi utilizzano l'architettura client-server a regime di controllo libero supportata da XML per gestire informazioni in ingresso e in uscita in un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Il metodo `Discover` ottiene le informazioni e i metadati da un servizio Web. Tali informazioni possono includere un elenco di origini dati disponibili nonché informazioni su alcuni dei provider dell'origine dati. Le proprietà definiscono i dati ottenuti da un'origine dati. Il metodo `Discover` è un metodo comune per la definizione di molti tipi di informazioni che un'applicazione client può richiedere dalle origini dati nelle istanze di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Le proprietà e l'interfaccia generica forniscono estensibilità senza che sia necessario riscrivere funzioni esistenti in un'applicazione client.  
  
 Il metodo `Execute` consente alle applicazioni di eseguire comandi specifici del provider in origini dati XMLA.  
  
 Sebbene il protocollo XMLA sia ottimizzato per le applicazioni Web, può essere inoltre utilizzato per applicazioni su reti LAN. Le applicazioni seguenti possono sfruttare i vantaggi di tale API basata su XML:  
  
-   Applicazioni client/server per cui è necessaria tecnologia flessibile tra il client e il server  
  
-   Applicazioni client/server destinate a più sistemi operativi  
  
-   Client per cui non è necessario uno stato significativo per aumentare la capacità del server  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA e modello UDM (Unified Dimensional Model)  
 XMLA è il protocollo utilizzato da applicazioni di Business Intelligence che utilizzano la metodologia del modello UDM (Unified Dimensional Model).  
  
  
