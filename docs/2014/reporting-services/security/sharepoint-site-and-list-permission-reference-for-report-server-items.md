---
title: Informazioni di riferimento sulle autorizzazioni relative a elenchi e siti di SharePoint per gli elementi del server di report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
- permission sets [Reporting Services]
ms.assetid: 1fcb27bd-4c4a-43f4-bfff-e42a59c87c49
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b3e97899fb58049b04860a564b3769feb13217fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101531"
---
# <a name="sharepoint-site-and-list-permission-reference-for-report-server-items"></a>Informazioni di riferimento sulle autorizzazioni relative a elenchi e siti di SharePoint per gli elementi del server di report
  In questo argomento vengono fornite informazioni di riferimento sulle autorizzazioni disponibili in SharePoint e che possono essere utilizzate per consentire l'accesso alle operazioni di un server di report eseguito in modalità integrata SharePoint. Tali informazioni sono utili per la scelta delle autorizzazioni da utilizzare per creare livelli di autorizzazione personalizzati.  
  
 In SharePoint sono disponibili 33 autorizzazioni che è possibile utilizzare per controllare l'accesso a contenuto e operazioni. Alcune di queste sono applicabili a operazioni e documenti relativi a un server di report basato su [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È possibile utilizzare le tabelle di riferimento per le autorizzazioni disponibili in questo articolo per individuare le autorizzazioni che supportano attività di creazione dei report specifiche.  
  
 Nelle prime colonne di ogni tabella sono riportati un elenco di autorizzazioni di SharePoint e una descrizione. La tabella include anche tre colonne in cui è indicata la modalità di utilizzo di una determinata autorizzazione nei livelli di autorizzazione predefiniti. I livelli di autorizzazione predefiniti includono:  
  
|Livello di autorizzazione|Abbreviazione|  
|----------------------|------------------|  
|Controllo completo|**F**|  
|Collaborazione|**C**|  
|Visitatore|**V**|  
  
 Le autorizzazioni che non interessano i server di report non sono elencate. In questo articolo di riferimento non sono incluse le autorizzazioni relative alla personalizzazione. Sebbene sia possibile includere elementi di un server di report in un sito Web personalizzato, il server di report non gestisce direttamente le operazioni o le richieste di personalizzazione.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità SharePoint &#124; SharePoint 2010 e SharePoint 2013.|  
  
## <a name="list-permissions"></a>Autorizzazioni relative agli elenchi  
 Le autorizzazioni impostate per la raccolta che contiene gli elementi del server di report determinano la modalità con cui gli utenti potranno accedere a tali elementi.  
  
|Autorizzazione|Descrizione|F|c|V|Funzionamento del server di report|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|Gestione elenchi|Consente di creare ed eliminare elenchi, aggiungere o rimuovere colonne in un elenco e aggiungere o rimuovere le visualizzazioni pubbliche di un elenco.|x|||Creazione di una cartella in una raccolta di SharePoint durante un'operazione di pubblicazione eseguita da uno strumento di creazione. Questa autorizzazione è necessaria anche per la gestione della cronologia dei report.|  
|Aggiungi elementi|Consente di aggiungere elementi a un elenco, documenti a raccolte documenti e commenti a discussioni Web.|x|x||Aggiunta di report, modelli di report, origini dati condivise e risorse (file di immagine esterni) a raccolte di SharePoint. Creazione di origini dati condivise. Generazione di modelli di report da origini dati condivise. Avvio di Generatore report e creazione di un nuovo report o caricamento di un modello in Generatore report.|  
|Modifica elementi|Consente di modificare voci di elenco, documenti in raccolte documenti e commenti a discussioni Web nei documenti, nonché di personalizzare pagine web part in raccolte documenti.<br /><br /> Creare sottoscrizioni e modificare quelle create.|x|x||Visualizzazione di versioni precedenti di documenti, tra cui snapshot della cronologia del report. Modifica delle proprietà degli elementi per report e altri documenti. Impostazione delle opzioni relative all'elaborazione dei report. Impostazione dei parametri di un report. Modifica delle proprietà delle origini dati. Creazione di snapshot delle cronologie dei report. Apertura di un modello di report o di un report basato su modello in Generatore report e salvataggio delle modifiche nel file. Assegnazione di report click-through alle entità di un modello. Sostituzione di definizioni di report, origini dati condivise, modelli di report o risorse con una versione più recente (il file viene sostituito ma vengono conservati i metadati). Gestione degli elementi dipendenti a cui viene fatto riferimento da un report o da un modello. Personalizzazione della web part Visualizzatore report per un report specifico.<br /><br /> Creazione, modifica ed eliminazione di sottoscrizioni che utilizzano le estensioni per il recapito di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per recapitare i report ai percorsi di destinazione. Tali operazioni possono essere eseguite solo dal proprietario della sottoscrizione e dagli utenti che dispongono dell'autorizzazione Gestione avvisi.|  
|Eliminazione elementi|Consente di eliminare elementi da un elenco, documenti da una raccolta documenti e commenti a discussioni Web da documenti.|x|x||Eliminazione di report, modelli di report, origini dati condivise e altri documenti da una raccolta.|  
|Visualizzazione elementi|Consente di visualizzare voci di elenco, documenti di raccolte documenti e commenti a discussioni Web.|x|X|x|Consente di aprire report, modelli di report e altri documenti, nonché di elaborare tali elementi sul server di report.|  
|Apertura elementi|Consente di visualizzare l'origine di documenti con gestori di file sul lato server.|x|X|x|Visualizzazione di un elenco di origini dati condivise. Download di una copia del file di origine per una definizione di report o modello di report. Visualizzazione di report click-through che utilizzano modelli di report come origine dei dati.|  
|Visualizzazione versioni|Consente di visualizzare versioni precedenti di una voce di elenco o di un documento.|x|X|x|Visualizzazione di versioni precedenti di documenti e snapshot di report.|  
|Eliminazione versioni|Consente di eliminare versioni precedenti di una voce di elenco o di un documento.|x|x||Eliminazione di versioni precedenti di documenti e snapshot di report.|  
  
> [!NOTE]  
>  Per gli elenchi sono inoltre disponibili le autorizzazioni Ignora estrazione, Approvazione elementi e Visualizzazione pagine applicazione, che non vengono tuttavia valutate dal server di report. Il server di report non gestisce infatti tali operazioni.  
  
## <a name="site-permissions"></a>Autorizzazioni relative ai siti  
 Le autorizzazioni relative ai siti consentono di accedere a operazioni del server di report non direttamente correlate agli elementi archiviati in una raccolta specifica, ad esempio la creazione e la modifica di pianificazioni condivise, che possono essere utilizzate da elementi di più raccolte, e la configurazione della web part Visualizzatore report, che può essere utilizzata in varie aree di un sito.  
  
|Autorizzazione|Descrizione|F|c|V|Funzionamento del server di report|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|Gestione autorizzazioni|Consente di creare e modificare i livelli di autorizzazione nel sito Web e di assegnare autorizzazioni a utenti e gruppi.|x|||Modifica delle autorizzazioni per tutte le operazioni e gli elementi di un server di report. Impostazione della sicurezza a livello di elemento di modello.|  
|Gestione sito web|Consente di eseguire tutte le attività di amministrazione del sito Web, nonché di gestirne il contenuto.|x|||Creazione, modifica ed eliminazione di pianificazioni condivise.|  
|Aggiunta e personalizzazione pagine|Consente di aggiungere, modificare o eliminare pagine HTML o pagine Web part e di modificare il sito Web tramite un editor compatibile con [!INCLUDE[winSPServ](../../includes/winspserv-md.md)].|x|||Aggiunta o rimozione di una web part Visualizzatore report.|  
|Visualizzazione informazioni utenti|Consente di visualizzare informazioni sugli utenti del sito Web.|x|X|x|Visualizzazione di report e altri elementi in siti, raccolte e cartelle diversi. Pubblicazione di report e altri elementi in una raccolta.|  
|Enumerazione autorizzazioni|Consente di enumerare le autorizzazioni relative a siti Web, elenchi, cartelle, documenti o voci di elenco.|x|||Lettura di autorizzazioni per tutti gli elementi di un server di report. Consente di visualizzare un report click-through che utilizza un modello di report contenente impostazioni di sicurezza per gli elementi del modello.|  
|Gestione avvisi|Consente di gestire avvisi per tutti gli utenti del sito Web.|x|||Creazione, modifica ed eliminazione di qualsiasi sottoscrizione su un sito.|  
|Utilizzo interfacce remote|Consente di utilizzare le interfacce SOAP, Web DAV o SharePoint Designer per accedere al sito Web.|x|X|x|Utilizzata per chiamare l'endpoint proxy dell'URL del server di report.|  
|Apertura|Consente di aprire un sito Web, un elenco o una cartella per accedere agli elementi disponibili in tale contenitore.|x|X|x|Lettura delle proprietà di elementi e pianificazioni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Confrontare ruoli e attività di Reporting Services con autorizzazioni e gruppi di SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
