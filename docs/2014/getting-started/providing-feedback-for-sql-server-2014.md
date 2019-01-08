---
title: Commenti e suggerimenti per SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sending feedback to Microsoft
- errors [SQL Server], feedback reporting
- feedback [SQL Server]
- submitting feedback [SQL Server]
- bug reporting [SQL Server]
- reporting usage information to Microsoft
- reporting errors to Microsoft
- SQL Server, feedback reporting
- documentation feedback [SQL Server]
- usage information reporting [SQL Server]
- product feedback [SQL Server]
- automatic error or usage reporting
ms.assetid: 28f3ebf0-ad71-4816-86a6-18a46f023cfe
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10466721f50dd8b090b5d6b1a06b5bffd6e5289d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376743"
---
# <a name="providing-feedback-for-sql-server-2014"></a>Invio di commenti e suggerimenti su SQL Server 2014
  [!INCLUDE[msCoName](../includes/msconame-md.md)] ringrazia gli utenti per il tempo dedicato e per il contributo che consente di migliorare i prodotti e la documentazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È possibile fornire suggerimenti e report sui bug relativi alle funzionalità del prodotto e all'interfaccia utente, inviare commenti e suggerimenti sulla documentazione e scegliere di inviare automaticamente segnalazioni di errori e dati sull'utilizzo a [!INCLUDE[msCoName](../includes/msconame-md.md)] per l'analisi. Ognuna di queste tre opzioni relative ai commenti e ai suggerimenti viene descritta di seguito.  
  
## <a name="submitting-feedback-about-the-product"></a>Invio di commenti sul prodotto  
 È possibile utilizzare la pagina per i commenti e i suggerimenti su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] disponibile nel sito [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect per inviare suggerimenti e report sui bug relativi alle funzionalità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], inclusi gli strumenti e le utilità, i linguaggi e le interfacce di programmazione.  
  
 È possibile trovare la pagina per i commenti e i suggerimenti su [!INCLUDE[msCoName](../includes/msconame-md.md)] nel sito [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Connect in numerosi modi.  
  
-   Accedere alla [pagina Web](https://go.microsoft.com/fwlink/?linkid=34178) per i commenti e i suggerimenti su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel sito [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect.  
  
-   Nella barra degli strumenti della Guida di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fare clic sul pulsante **Commenti e suggerimenti** oppure scegliere il comando **Community/Commenti e suggerimenti**.  
  
-   Nella barra degli strumenti della Guida di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fare clic sul pulsante **Commenti e suggerimenti**.  
  
-   Nella parte superiore di qualsiasi argomento della documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fare clic sul pulsante **Commenti e suggerimenti**.  
  
 Per visualizzare la barra degli strumenti della Guida in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] o in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], è necessario effettuare una delle operazioni seguenti:  
  
-   Accedere alla Guida dall'utilità.  
  
-   Selezionare il **aiutare** casella di controllo il **barre degli strumenti** scheda della finestra di **strumenti/Personalizza...**  comando.  
  
## <a name="automatic-error-and-usage-reporting"></a>Segnalazione automatica errori e utilizzo caratteristiche  
 È possibile abilitare funzionalità specifiche per la segnalazione automatica degli errori e per inviare informazioni sull'utilizzo del software e dei servizi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Queste informazioni verranno utilizzate da [!INCLUDE[msCoName](../includes/msconame-md.md)] per migliorare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Tutti i dati sono riservati.  
  
### <a name="managing-automatic-usage-reporting"></a>Gestione della segnalazione automatica delle informazioni sull'utilizzo  
 La segnalazione automatica delle informazioni sull'utilizzo consente di decidere se raccogliere e inviare dati a [!INCLUDE[msCoName](../includes/msconame-md.md)]. Per segnalare i dati sull'utilizzo, in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vengono utilizzate due pipeline che inviano dati simili, ma relativi a programmi diversi, e che vengono abilitate e disabilitate separatamente. L'abilitazione o la disabilitazione di una pipeline mediante uno dei programmi consente inoltre di arrestare o di avviare la raccolta di dati da altri programmi che condividono la stessa pipeline.  
  
-   Viene utilizzata una pipeline per segnalare i dati sull'utilizzo relativi a tutti i componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], ad eccezione della documentazione online e di alcuni elementi dell'interfaccia utente basata su [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio negli strumenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Dopo l'installazione, è inoltre possibile disabilitare o abilitare questa pipeline. A tale scopo, in[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] aprire un progetto basato su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], quindi scegliere **Opzioni suggerimenti clienti** dal menu **?**. Questo comando non verrà visualizzato fino a quando non viene aperto un progetto basato su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   L'altra pipeline viene utilizzata per la documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], gli elementi dell'interfaccia utente basata su Visual Studio degli strumenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e Visual Studio. Dopo l'installazione, è inoltre possibile disabilitare o abilitare questa pipeline. A tale scopo, in[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] aprire un progetto basato su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], quindi scegliere **Opzioni suggerimenti clienti** dal menu **?**. Questo comando non verrà visualizzato fino a quando non viene aperto un progetto basato su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="helping-build-a-better-books-online"></a>Contributo al miglioramento della documentazione online  
 Se si sceglie di abilitare la segnalazione utilizzo caratteristiche per la documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], il team responsabile della documentazione sarà in grado di migliorare il materiale offerto. I dati di aggregazione ricevuti indicano le esigenze dei clienti, nonché le modalità di spostamento tra gli argomenti, la frequenza di visualizzazione di argomenti specifici e gli argomenti considerati maggiormente utili.  
  
 I suggerimenti e i commenti inviati dagli utenti consentiranno di identificare le modalità di utilizzo della documentazione in modo che sia in grado di allocare le proprie risorse alla scrittura degli argomenti più importanti e di progettare sistemi di documentazione futuri per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Le informazioni sull'utilizzo dalla documentazione online possono inoltre agevolare l'identificazione di funzionalità per le quali i clienti richiedono spesso assistenza. consentendo in questo modo di individuare le aree per cui è necessario migliorare l'utilizzabilità.  
  
  
