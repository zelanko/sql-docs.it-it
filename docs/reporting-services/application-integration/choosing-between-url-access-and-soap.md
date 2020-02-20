---
title: Scegliere tra accesso con URL e SOAP
description: 'È possibile integrare Reporting Services nelle applicazioni personalizzate in due modi: accesso con URL e API SOAP di Reporting Services. La modalità da utilizzare dipende da diversi fattori.'
ms.date: 10/19/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d401c7d95cff5011dffbfaac2ebcc9bfa5ea5c24
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74796917"
---
# <a name="choose-between-url-access-and-soap-in-reporting-services"></a>Scegliere tra accesso con URL e SOAP in Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

L'integrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni personalizzate può risultare complessa. La complessità non è tuttavia dovuta al modello di programmazione o alle API, ma alle numerose modalità di integrazione disponibili. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è stato progettato interamente come piattaforma di sviluppo e, in quanto tale, offre flessibilità di programmazione. Alla flessibilità è associata l'esigenza di prendere decisioni importanti relativamente all'integrazione delle funzionalità di navigazione e gestione dei report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni aziendali esistenti.

> [!NOTE]
> A partire da SQL Server 2017 Reporting Services, è disponibile l'accesso all'API REST per lo sviluppo di soluzioni. L'accesso all'API SOAP è stato deprecato. Per altre informazioni, vedere [Sviluppare con le API REST per Reporting Services](../developer/rest-api.md).
  
 È possibile integrare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni personalizzate in due modi: accesso con URL e API SOAP di Reporting Services. La modalità da utilizzare dipende da diversi fattori. In alcuni casi, l'integrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni aziendali personalizzate richiede l'uso dell'accesso con URL e di SOAP. È necessario porsi le domande seguenti:  
  
-   Quali tipi di funzionalità di creazione di report aziendali sono necessari? È necessario disporre di un modo semplice per avviare e navigare tra i report oppure sono necessarie caratteristiche di gestione del server di report più avanzate per la soluzione aziendale personalizzata?  
  
-   In quale tipo di ambiente operano in genere gli utenti? L'applicazione aziendale è un'applicazione Web o un'applicazione Windows? Con quanta facilità gli utenti finali possono passare da un ambiente Win32 a un ambiente Web? Quale tipo di controllo è necessario sull'ambiente in cui i report vengono eseguiti e gestiti?  
  
 Dopo aver risposto alle domande precedenti, è possibile scegliere come integrare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella propria infrastruttura IT. In genere, l'accesso con URL è preferibile per la visualizzazione e la navigazione di singoli report. L'accesso con URL consente di navigare tra i report in modo semplice e rapido senza l'overhead del servizio Web. L'accesso con URL, inoltre, è attualmente l'unica tecnica di programmazione che utilizza la versione completa del Visualizzatore HTML per la navigazione dei report, che include la barra degli strumenti dei report. L'accesso con URL garantisce inoltre prestazioni migliori rispetto a SOAP in quanto consente di ignorare il marshalling delle richieste SOAP da e verso il server. Negli scenari di integrazione in cui è necessario poter accedere in modo rapido e semplice ai report con gli strumenti predefiniti di visualizzazione e navigazione, l'accesso con URL rappresenta la scelta migliore.  
  
> [!NOTE]  
> L'accesso con URL al server di report supporta il Visualizzatore HTML e la funzionalità estesa della barra degli strumenti dei report. L'API SOAP non supporta questo tipo di report visualizzabile. Se si esegue il rendering dei report usando l'API SOAP, progettare e sviluppare una barra degli strumenti dei report personalizzata.
  
 Per altre informazioni sulla barra degli strumenti dei report, vedere [Visualizzatore HTML e barra degli strumenti dei report](../../reporting-services/html-viewer-and-the-report-toolbar.md).  
  
 Per altre informazioni sull'accesso con URL, vedere [Accesso con URL](../../reporting-services/url-access-ssrs.md).  
  
 L'accesso con URL è utile per la visualizzazione dei report, ma non fornisce le funzionalità di gestione degli spazi dei nomi e dei report che possono essere essenziali per qualsiasi scenario aziendale di creazione di report. In questo caso, è consigliabile utilizzare le ampie e ricche funzionalità dell'API SOAP di Reporting Services. Con l'API SOAP è possibile gestire e distribuire report, creare pianificazioni, configurare le proprietà del server, gestire lo spazio dei nomi del server di report, creare sottoscrizioni e altro ancora. L'API SOAP espone il set completo di funzionalità di gestione in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. L'API SOAP può consentire inoltre la visualizzazione e la navigazione dei report tramite il metodo <xref:ReportExecution2005.ReportExecutionService.Render%2A> dell'API. La visualizzazione dei report tramite l'API SOAP non consente tuttavia l'abilitazione delle funzionalità di visualizzazione predefinite della barra degli strumenti dei report, né la gestione automatica dell'interattività dei report consentite dall'accesso con URL.  
  
 Per altre informazioni sull'API SOAP di Reporting Services, vedere [Servizio Web ReportServer](../../reporting-services/report-server-web-service/report-server-web-service.md).  
  
 Nella maggior parte dei casi, l'accesso con URL e le chiamate SOAP sono entrambi necessari per soddisfare le esigenze in materia di creazione di report. SOAP viene utilizzato durante la connessione iniziale al database del server di report e la visualizzazione dell'elenco di report disponibili in un'interfaccia utente, mentre l'accesso con URL viene utilizzato per l'effettivo accesso e la navigazione dei singoli report.  
  
 Per un esempio di uso dell'accesso con URL in combinazione con il servizio Web per offrire funzionalità di creazione di report integrate, vedere [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (Esempi del prodotto SQL Server Reporting Services).

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
