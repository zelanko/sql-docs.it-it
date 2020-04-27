---
title: Condividere feed di dati usando una libreria di feed di dati (PowerPivot per SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data feeds [Analysis Services with SharePoint]
ms.assetid: 4ec98dec-0cd2-4727-bb79-5bf6f8a865d6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00ecb4487119251f1b86c2daf29b7481966f09f7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071147"
---
# <a name="share-data-feeds-using-a-data-feed-library-powerpivot-for-sharepoint"></a>Condividere feed di dati utilizzando una libreria di feed di dati (PowerPivot per SharePoint)
  Un feed di dati è un flusso di dati XML generato da un servizio o da un'applicazione che espone i dati nel formato wire Atom. Viene utilizzato sempre più frequentemente per trasferire dati tra applicazioni e visualizzatori lato client. In una distribuzione PowerPivot per SharePoint, i feed di dati vengono utilizzati per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] popolare un'origine dati con dati provenienti da un'applicazione o un servizio in grado di riconoscere Atom.  
  
 In presenza di una combinazione di applicazioni specifiche di Atom, potrebbe non essere mai necessario sapere come i feed vengono generati e utilizzati perché il trasferimento dei dati avviene in modo continuo tra le applicazioni. Tuttavia, le organizzazioni che utilizzano soluzioni personalizzate per pubblicare feed Atom richiedono spesso la possibilità di rendere disponibili i feed agli Information Worker. A tal fine è possibile, ad esempio, creare e condividere file di documenti di servizio dati (con estensione atomsvc) tramite cui vengono fornite le connessioni alle origini online che consentono di produrre i feed. Una libreria specifica, chiamata libreria di feed di dati, supporta la creazione e la condivisione dei documenti di servizio dati in un'applicazione Web di SharePoint.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Prerequisiti](#prereq)  
  
 [Creare un documento di servizio dati](#createdsdoc)  
  
 [Proteggere un documento di servizio dati](#securedsdoc)  
  
 [Modificare un documento di servizio dati](#modifydsdoc)  
  
 [Passaggio successivo: usare un documento di servizio dati](#usedsdoc)  
  
> [!NOTE]  
>  Anche se i feed di dati vengono usati per aggiungere dati Web a un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] creata in [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], un documento di servizio dati può essere elaborato da qualsiasi applicazione client in grado di leggere un feed Atom.  
  
##  <a name="prerequisites"></a><a name="prereq"></a> Prerequisiti  
 È necessario disporre di una distribuzione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] di PowerPivot per SharePoint che [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aggiunga l'elaborazione di query a una farm di SharePoint. Il supporto Feed di dati viene distribuito tramite il pacchetto della soluzione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 È necessario disporre di una raccolta di SharePoint che supporti il tipo di contenuto del documento di servizio dati. A tal scopo si consiglia una libreria di feed di dati predefinita, tuttavia è possibile aggiungere manualmente il tipo di contenuto a qualsiasi libreria. Per ulteriori informazioni, vedere [creare o personalizzare una libreria di feed di dati &#40;PowerPivot per SharePoint&#41;](create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
 È necessario disporre di un servizio dati o di un'origine dati online che consenta di fornire dati tabulari XML in formato Atom 1.0.  
  
 È necessario disporre di autorizzazioni di collaborazione in un sito di SharePoint per creare o gestire un documento di servizio dati in una raccolta di SharePoint.  
  
##  <a name="create-a-data-service-document"></a><a name="createdsdoc"></a> Creare un documento di servizio dati  
 Un documento di servizio dati è una richiesta permanente di trasmissione dei dati in base alle richieste di un'origine dati online o di un'applicazione tramite cui vengono forniti dati in un formato di feed. Quando si crea un documento di servizio dati, si specifica un indicatore di misura a uno o più servizi dati indirizzabili tramite URL che forniscono dati tabulari XML in formato diffuso Atom.  
  
 In un documento singolo possono essere specificati più feed di dati. Ciò si rivela utile quando si desidera recuperare un set di payload dei dati dallo stesso servizio, o anche da servizi diversi, con un'unica operazione di importazione.  
  
1.  In un sito di SharePoint aprire la libreria di feed di dati o un'altra raccolta documenti in cui è stato aggiunto e configurato il tipo di contenuto del servizio dati. Per trovare una libreria di feed di dati precedentemente creata, selezionare **Visualizza tutto** dalla barra di avvio veloce.  
  
2.  Nella barra multifunzione all'inizio della pagina fare clic su **Documenti**in Strumenti documento.  
  
3.  Scegliere **Nuovo documento** , quindi selezionare **Documento di servizio dati**.  
  
4.  Nella pagina Nuovo documento di servizio dati immettere le informazioni seguenti:  
  
    1.  Nome e descrizione per il documento di servizio dati. Assicurarsi di fornire dettagli sufficienti affinché gli utenti possano stabilire se utilizzare il feed.  
  
    2.  In Feed di dati immettere un URL di un servizio dati o di un'applicazione Web tramite cui vengono forniti dati in formato Atom 1.0.  
  
         L'URL deve essere risolto in un servizio che restituisce dati strutturati o semistrutturati in righe e colonne. Il servizio deve restituire i dati in modo anonimo o tramite le credenziali di sicurezza dell'utente corrente.  
  
         L'URL deve essere risolto in un servizio che supporta l'autenticazione di Windows, l'autenticazione di base o l'accesso anonimo. L'utente che importa il feed specifica quale combinazione utilizzare. La sicurezza integrata è selezionata per impostazione predefinita.  
  
         In un URL del feed di dati possono essere inclusi i parametri. Diversi tipi di tecnologie dei servizi di dati supportano schemi di indirizzamento URL avanzati che consentono di selezionare con precisione i dati che si desidera utilizzare. Una istanza di ADO.NET Data Services, ad esempio, fornisce parametri URL per la specifica di entità, associazioni e percorsi di navigazione nei dati sottostanti. Se si specifica un URL complesso come origine del feed di dati, è possibile indicare con precisione il set di dati che si desidera utilizzare.  
  
    3.  Per lo stesso feed di dati, immettere un nome di tabella che consenta di identificare successivamente il set di dati in un'applicazione client. In [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], ciascun feed di dati importato viene posizionato nel relativo controllo della tabella in un'origine dati di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . È necessario specificare il nome della tabella che riceve i dati importati quando si configura il feed di dati.  
  
5.  Fare clic su "Aggiungi altro feed di dati" per ripetere i passaggi precedenti in modo da specificare feed aggiuntivi dallo stesso servizio o da un servizio diverso.  
  
     Ogni documento di servizio dati viene elaborato con un'operazione singola. Tutti i feed di dati nel documento verranno generati in modo asincrono e restituiti a un'applicazione client nella stessa operazione. Per questa ragione, specificare coppie URL-tabella solo per i feed di dati che si desidera utilizzare insieme.  
  
     Poiché gli schemi di autenticazione vengono impostati a livello del documento di servizio dati, ogni feed di dati aggiuntivo deve provenire da un servizio o da un'applicazione che supporti lo stesso schema di autenticazione del primo feed. Tutti i feed all'interno dello stesso documento di servizio dati saranno autenticati in fase di esecuzione con lo stesso metodo.  
  
6.  Salvare il documento. Il documento di servizio dati viene archiviato come file fisico (con estensione atomsvc) in una raccolta contenuto configurata per questo tipo di contenuto.  
  
 Per utilizzare il documento di servizio dati, è possibile aprire la cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] e scegliere l'opzione **Da feed di dati** nell'importazione guidata dei dati. Quando richiesto, l'utente specificherà l'URL SharePoint del documento di servizio dati per avviare un'operazione di importazione dei dati. Per altre informazioni, vedere [usare feed di dati &#40;PowerPivot per SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="secure-a-data-service-document"></a><a name="securedsdoc"></a>Proteggere un documento di servizio dati  
 Un documento di servizio dati eredita le autorizzazioni della libreria che lo contiene. Le autorizzazioni impostate sull'elemento determineranno l'eventuale possibilità di aprire, modificare o eliminare il documento di servizio dati.  
  
 Per utilizzare un documento di servizio dati per l'importazione del feed di dati nell'applicazione client di PowerPivot, sono necessarie solo autorizzazioni di visualizzazione nel documento. Le autorizzazioni di visualizzazione sono sufficienti per risolvere l'URL nell'importazione guidata.  
  
 Le autorizzazioni di visualizzazione per un documento di servizio dati vengono controllate solo all'inizio di un'operazione di importazione di feed di dati. Dopo l'importazione, le autorizzazioni per il documento non vengono controllate continuamente; i feed aggiunti a un'origine dati PowerPivot sono presenti come dati statici, disconnessi dal documento di servizio dati in cui venivano fornite le informazioni di connessione originali.  
  
 Allo stesso modo, nelle operazioni di aggiornamento dei dati pianificate successivamente non è incluso il documento di servizio dati. Al momento dell'importazione, le informazioni di connessione per ogni feed vengono copiate nell'origine dati PowerPivot per l'aggiornamento. Analogamente, le autorizzazioni per un documento di servizio dati non vengono verificate per l'aggiornamento dei dati, perché al documento non viene mai fatto riferimento in un'operazione di aggiornamento.  
  
|Attività|Requisiti relativi all'autorizzazione di SharePoint|  
|----------|----------------------------------------|  
|Importare i feed di dati in una cartella di lavoro abilitata per PowerPivot.|Autorizzazioni di visualizzazione per il documento di servizio dati in una raccolta.|  
|Nell'applicazione client PowerPivot, aggiornare i dati recuperati precedentemente tramite feed.|Non applicabile. Nell'applicazione client PowerPivot vengono utilizzate informazioni di connessione HTTP incorporate per connettersi direttamente ai servizi dati e alle applicazioni tramite cui viene fornito il feed. Nell'applicazione client PowerPivot non viene utilizzato il documento di servizio dati.|  
|In una farm di SharePoint, l'aggiornamento dei dati viene eseguito come attività programmata e l'input dell'utente non è richiesto.|Non applicabile. Nel servizio PowerPivot vengono utilizzate informazioni di connessione HTTP incorporate per connettersi direttamente ai servizi dati e alle applicazioni tramite cui viene fornito il feed. Nel servizio PowerPivot non viene utilizzato il documento di servizio dati.|  
|Eliminare un documento di servizio dati in una libreria|Autorizzazioni di collaborazione nella libreria.|  
  
##  <a name="modify-a-data-service-document"></a><a name="modifydsdoc"></a> Modificare un documento di servizio dati  
 È possibile aggiungere, modificare o rimuovere singole voci URL-tabella in un documento di servizio dati. Dopo il salvataggio delle modifiche, gli utenti che selezionano il documento di servizio in una nuova operazione di importazione otterranno i feed di dati specificati.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nelle quali era utilizzata una versione precedente del documento. Ciò è dovuto al fatto che un documento di servizio dati viene letto solo una volta durante l'operazione di importazione iniziale. Durante l'importazione, l'URL del servizio e i nomi di tabella vengono copiati e archiviati internamente nella cartella di lavoro. Questi valori interni vengono quindi utilizzati in operazioni di aggiornamento successive per ottenere dati aggiornati.  
  
 Poiché non è disponibile un collegamento persistente tra un documento di servizio dati in un sito di SharePoint e la cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in cui è contenuto il feed importato, la modifica di qualsiasi parte di un documento di servizio dati non ha effetto nelle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] esistenti.  
  
> [!IMPORTANT]  
>  Anche se il documento di servizio dati viene letto una sola volta, l'accesso ai servizi dati tramite cui vengono forniti i dati effettivi può essere eseguito a intervalli regolari per ottenere feed più recenti. Per ulteriori informazioni sull'aggiornamento dei dati, vedere [aggiornamento dati PowerPivot](power-pivot-data-refresh.md).  
  
##  <a name="next-step-use-a-data-service-document"></a><a name="usedsdoc"></a> Passaggio successivo: Utilizzo di un documento di servizio dati  
 Per utilizzare un documento di servizio dati creato in una raccolta di SharePoint, è possibile utilizzare l'opzione **di importazione da feed di dati** in un'origine dati PowerPivot. Per istruzioni, vedere [usare feed di dati &#40;PowerPivot per SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Feed di dati PowerPivot](power-pivot-data-feeds.md)  
  
  
