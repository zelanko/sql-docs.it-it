---
title: Funzionalità di SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], about SQL Server Management Studio
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: e75504b9-7968-4e3b-8411-fd79fe09021e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 790e02374fe209576c963c5f1e9c6e63e8e2d16b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779789"
---
# <a name="features-in-sql-server-management-studio"></a>Caratteristiche in SQL Server Management Studio
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] comprende le caratteristiche generali seguenti:  
  
-   Supporta la maggior parte delle attività amministrative per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Offre un singolo ambiente integrato per la gestione e creazione del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] .  
  
-   Finestre di dialogo per la gestione di oggetti in [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]che consentono di eseguire immediatamente le azioni, di inviarle a un editor del codice o di creare script per eseguirle in seguito.  
  
-   Finestre di dialogo non a scelta obbligatoria e ridimensionabili consentono di accedere a più strumenti mentre sono aperte.  
  
-   Una normale finestra di dialogo per le pianificazioni che consente di eseguire in un secondo momento l'azione delle finestre di dialogo per la gestione.  
  
-   Esportazione e importazione della registrazione server [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] da un ambiente [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] a un altro.  
  
-   Consente di salvare o stampare file XML Showplan o Deadlock generati da SQL Server Profiler, esaminarli in seguito o inviarli agli amministratori per l'analisi.  
  
-   Una nuova e più completa finestra per i messaggi informativi e sugli errori consente di inviare a [!INCLUDE[msCoName](../includes/msconame-md.md)] un commento sui messaggi, copiare messaggi negli Appunti e inviarli facilmente tramite posta elettronica al team di supporto tecnico.  
  
-   Un browser integrato per l'esplorazione rapida di MSDN o della Guida.  
  
-   Integrazione della Guida tramite le community online.  
  
-   Un'esercitazione su [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per sfruttare le numerose nuove funzionalità e aumentare da subito la produttività.  
  
-   Nuova versione di Monitoraggio attività con filtri e aggiornamento automatico.  
  
-   Interfacce di Posta elettronica database integrate.  
  
## <a name="new-scripting-capabilities"></a>Nuove funzionalità di scripting  
 Il componente Editor del codice di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] contiene editor di script integrati per la creazione di script [!INCLUDE[tsql](../includes/tsql-md.md)], MDX, DMX e XML/A. Comprende le caratteristiche seguenti:  
  
-   Guida dinamica per l'accesso immediato a informazioni specifiche mentre si lavora.  
  
-   Un set completo di modelli per la creazione di modelli personalizzati.  
  
-   Supporto per la scrittura e modifica di query o script senza che sia necessario collegarsi a un server.  
  
-   Supporto di scripting per query e script SQLCMD.  
  
-   Una nuova interfaccia per la visualizzazione dei risultati XML.  
  
-   Controllo del codice sorgente integrato per i progetti script e di soluzione, con supporto dell'archiviazione e gestione di copie degli script man mano che si evolvono.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Supporto IntelliSense per istruzioni MDX.  
  
## <a name="object-explorer-features"></a>Caratteristiche di Esplora oggetti  
 Il componente Esplora oggetti di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] è uno strumento integrato che consente di visualizzare e gestire gli oggetti in qualsiasi tipo di server. Comprende le caratteristiche seguenti:  
  
-   Applicazione di filtri in base a nome, schema o data o a parte di essi.  
  
-   Popolamento asincrono di oggetti con la possibilità di filtrarli in base ai loro metadati.  
  
-   Accesso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent su server di replica per l'amministrazione.  
  
 Per altre informazioni, vedere [Esplora oggetti](../ssms/object/object-explorer.md).  
  
## <a name="extensibility"></a>Estendibilità  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] è basato sulla shell isolata di Visual Studio che supporta implicitamente l'estendibilità (componenti aggiuntivi/plug-in). È possibile attingere ai servizi di estendibilità di Visual Studio per rendere disponibili funzionalità personalizzate in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]; tale estendibilità non è tuttavia supportata.  
  
 Ci sono utenti e terze parti che hanno sviluppato estensioni per [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Anche se questa pratica non viene sconsigliata, tenere comunque presente che tale estendibilità non è supportata, per cui potrebbero sorgere dei problemi di compatibilità con le versioni precedenti e successive. Microsoft non pubblica documentazione per l'estensione [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Tuttavia, esistono blog di comunità e codici di esempio online che potrebbero risultare molto utili a questo proposito.  
  
 Microsoft non supporta le installazioni di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] con estensioni a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , pertanto se sono state installate estensioni a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , è necessario rimuoverle prima di chiamare il Supporto tecnico relativamente a un problema [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)  
  
  
