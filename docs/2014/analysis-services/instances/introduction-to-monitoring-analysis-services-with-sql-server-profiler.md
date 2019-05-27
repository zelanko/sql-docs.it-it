---
title: Introduzione al monitoraggio di Analysis Services con SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 568ec549-5ddc-493a-b9f8-3bdc548b562e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3146f5a9f3e22753cc86c07b609d997be580b9f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079801"
---
# <a name="introduction-to-monitoring-analysis-services-with-sql-server-profiler"></a>Introduzione al monitoraggio di Analysis Services tramite SQL Server Profiler
  Tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] è possibile monitorare eventi generati da un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], è possibile eseguire le operazioni seguenti:  
  
-   Monitorare le prestazioni di un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Eseguire il debug di istruzioni MDX (Multidimensional Expressions).  
  
-   Identificare istruzioni MDX che vengono eseguite lentamente.  
  
-   Verificare il funzionamento di istruzioni MDX nelle fasi di sviluppo di un progetto tramite l'esecuzione passaggio per passaggio delle istruzioni per assicurarsi che il codice funzioni come previsto.  
  
-   Risolvere problemi in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] attraverso l'acquisizione di eventi in un sistema di produzione e la relativa riproduzione in un sistema di prova. Ciò risulta utile per eseguire verifiche e debug e consentire agli utenti di continuare a utilizzare il sistema di produzione senza interferenze.  
  
-   Controllare ed esaminare l'attività verificatasi in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Un amministratore responsabile della sicurezza può rivedere qualsiasi evento controllato, ad esempio l'esito positivo o negativo di un tentativo di accesso e l'esito positivo o negativo dell'accesso a istruzioni e oggetti.  
  
-   Visualizzare dati sugli eventi acquisiti o acquisire e salvare dati su ciascun evento su un file o una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per consentirne l'analisi o l'esecuzione in futuro. Durante la riproduzione dei dati è possibile rieseguire fedelmente gli eventi salvati in tempo reale o passaggio per passaggio.  
  
## <a name="using-sql-server-profiler"></a>Utilizzo di SQL Server Profiler  
 Per creare o riprodurre tracce utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , è necessario essere membro del ruolo di server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se si è membri del ruolo di server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile avviare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] dal gruppo di programmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del menu **Start** .  
  
 Quando si utilizza [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], notare quanto segue:  
  
-   Le definizioni di traccia sono archiviate nel database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] attraverso l'istruzione CREATE.  
  
-   È possibile eseguire più tracce contemporaneamente.  
  
-   Gli eventi di una medesima traccia possono essere ricevuti da più connessioni.  
  
-   Una traccia può continuare anche quando si arresta e riavvia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Le password non sono rivelate negli eventi di traccia, ma vengono sostituite dai \* \* \* \* \* \* nell'evento.  
  
 Per ottenere prestazioni ottimali, utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per monitorare solo gli eventi a cui si è maggiormente interessati. Il monitoraggio di un numero troppo elevato di eventi determina un aumento dell'overhead e può portare alla creazione di una tabella o di un file di traccia di grandi dimensioni, soprattutto quando il monitoraggio viene eseguito per un lungo periodo di tempo. È inoltre consigliabile utilizzare filtri per limitare la quantità di dati raccolta ed evitare che le tracce diventino troppo grandi.  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi di traccia di Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [Creare tracce del profiler per la riproduzione &#40;Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md)  
  
  
