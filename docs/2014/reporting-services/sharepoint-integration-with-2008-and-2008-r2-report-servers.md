---
title: Integrazione di SharePoint con server di report 2008 e 2008 R2 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9f51c37-b071-45d0-baec-f82fa6db366f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d29d41069d5daca25d53477326e864720aa87ca1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101199"
---
# <a name="sharepoint-integration-with-2008-and-2008-r2--report-servers"></a>Integrazione di SharePoint con server di report 2008 e 2008 R2
  Nella versione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] viene introdotta un'architettura in cui la modalità SharePoint è basata su un servizio SharePoint Shared. La gestione della nuova funzionalità viene eseguita nelle pagine **Gestisci servizi** e **Gestisci applicazioni di servizio** di Amministrazione centrale SharePoint. L' [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] architettura precedente per l'integrazione con SharePoint è ancora supportata [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] con il componente aggiuntivo per i prodotti SharePoint 2010, pertanto è possibile integrare SharePoint 2010 con le versioni precedenti di un server di report.  
  
 Le pagine di Amministrazione centrale SharePoint da utilizzare per amministrare l'architettura precedente sono disponibili come indicato di seguito:  
  
1.  Da Amministrazione centrale SharePoint fare clic su **Impostazioni generali applicazione**.  
  
2.  Il gruppo **SQL Server Reporting Services (2008 e 2008 R2)** contiene i collegamenti e le pagine di gestione per l'architettura precedente.  
  
## <a name="server-integration-architecture"></a>Architettura di integrazione del server  
 Quando si integra un server di report con un'istanza di un prodotto SharePoint, gli elementi e le proprietà vengono archiviati nei database del contenuto di SharePoint. Ciò consente di ottenere un livello di integrazione superiore tra le tecnologie server, che influisce sulle modalità di archiviazione, accesso e sicurezza del contenuto.  
  
 Poiché gli elementi e le proprietà dei report vengono archiviati nei database del contenuto di SharePoint, è possibile esplorare i tipi di contenuto del server di report tramite le raccolte di SharePoint, proteggere gli elementi utilizzando gli stessi livelli di autorizzazione e lo stesso provider di autenticazione che controlla l'accesso agli altri documenti aziendali ospitati in un sito di SharePoint, utilizzare le funzionalità per la collaborazione e la gestione dei documenti per l'archiviazione e l'estrazione dei report per la modifica, utilizzare gli avvisi per determinare se un determinato elemento è stato modificato, nonché incorporare o personalizzare la web part Visualizzatore report nelle pagine e nei siti dell'applicazione. Se si dispone di autorizzazioni sufficienti in un sito di SharePoint, è possibile generare anche modelli di report da origini dati condivise e utilizzare Generatore report per creare report.  
  
 Il server di report continua a svolgere tutte le attività di recapito, rendering ed elaborazione dei dati. Supporta inoltre tutte le attività di elaborazione pianificata dei report per snapshot e cronologia dei report. Quando si apre un report da un sito di SharePoint, l'endpoint del server di report consente di stabilire una connessione a un server di report, di creare una sessione, di preparare il report per l'elaborazione, di recuperare i dati, di unire il report nel layout di report e di visualizzare il report nella web part del visualizzatore di report. Dopo avere aperto il report è possibile esportarlo in vari formati di applicazione oppure interagire con i dati, eseguendo il drill-down ai valori sottostanti o facendo clic su un report correlato. Le interazioni con il report e le operazioni di esportazione vengono eseguite sul server di report.  
  
 Il server di report sincronizza dati e operazioni con SharePoint e tiene traccia delle informazioni relative ai file elaborati. Quando si modificano le proprietà o le impostazioni di un elemento del server di report, la modifica viene archiviata in un database di SharePoint e quindi copiata in un database del server di report, che viene utilizzato per l'archiviazione interna per il server di report.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Attivare le funzionalità di integrazione per Power View e server di report in SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)  
 Viene descritto come attivare la funzionalità Report Server necessaria per l'integrazione con i server di report da versioni precedenti.  
  
  
