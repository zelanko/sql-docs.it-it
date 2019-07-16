---
title: Condividere feed di dati usando una libreria di Feed di dati (Power Pivot per SharePoint) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f262fe19ba39f217135908173189bf93a7e68817
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163702"
---
# <a name="share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint"></a>Condividere feed di dati usando una libreria di feed di dati (PowerPivot per SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un feed di dati è un flusso di dati XML generato da un servizio o da un'applicazione che espone i dati nel formato wire Atom. Viene utilizzato sempre più frequentemente per trasferire dati tra applicazioni e visualizzatori lato client. In una distribuzione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint i feed di dati vengono usati per popolare un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] con dati provenienti da un'applicazione o da un servizio specifico di Atom.  
  
 In presenza di una combinazione di applicazioni specifiche di Atom, potrebbe non essere mai necessario sapere come i feed vengono generati e utilizzati perché il trasferimento dei dati avviene in modo continuo tra le applicazioni. Tuttavia, le organizzazioni che utilizzano soluzioni personalizzate per pubblicare feed Atom richiedono spesso la possibilità di rendere disponibili i feed agli Information Worker. A tal fine è possibile, ad esempio, creare e condividere file di documenti di servizio dati (con estensione atomsvc) tramite cui vengono fornite le connessioni alle origini online che consentono di produrre i feed. Una libreria specifica, chiamata libreria di feed di dati, supporta la creazione e la condivisione dei documenti di servizio dati in un'applicazione Web di SharePoint.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
 [Prerequisiti](#prereq)  
  
 [Creare un documento di servizio dati](#createdsdoc)  
  
 [Proteggere un documento di servizio dati](#securedsdoc)  
  
 [Modificare un documento di servizio dati](#modifydsdoc)  
  
 [Passaggio successivo: Usare un documento di servizio dati](#usedsdoc)  
  
> [!NOTE]  
>  Anche se i feed di dati vengono usati per aggiungere dati Web a un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] creata in [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], un documento di servizio dati può essere elaborato da qualsiasi applicazione client in grado di leggere un feed Atom.  
  
##  <a name="prereq"></a> Prerequisiti  
 È necessario avere una distribuzione di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint che aggiunga l'elaborazione di query [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a una farm di SharePoint. Il supporto Feed di dati viene distribuito tramite il pacchetto della soluzione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 È necessario disporre di una raccolta di SharePoint che supporti il tipo di contenuto del documento di servizio dati. A tal scopo si consiglia una libreria di feed di dati predefinita, tuttavia è possibile aggiungere manualmente il tipo di contenuto a qualsiasi libreria. Per altre informazioni, vedere [Creare o personalizzare una libreria di feed di dati &#40;PowerPivot per SharePoint&#41;;](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
 È necessario disporre di un servizio dati o di un'origine dati online che consenta di fornire dati tabulari XML in formato Atom 1.0.  
  
 È necessario disporre di autorizzazioni di collaborazione in un sito di SharePoint per creare o gestire un documento di servizio dati in una raccolta di SharePoint.  
  
##  <a name="createdsdoc"></a> Creare un documento di servizio dati  
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
  
 Per utilizzare il documento di servizio dati, è possibile aprire la cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] e scegliere l'opzione **Da feed di dati** nell'importazione guidata dei dati. Quando richiesto, l'utente specificherà l'URL SharePoint del documento di servizio dati per avviare un'operazione di importazione dei dati. Per altre informazioni, vedere [Usare feed di dati &#40;Power Pivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="securedsdoc"></a> Proteggere un documento di servizio dati  
 Un documento di servizio dati eredita le autorizzazioni della libreria che lo contiene. Le autorizzazioni impostate sull'elemento determineranno l'eventuale possibilità di aprire, modificare o eliminare il documento di servizio dati.  
  
 Per usare un documento di servizio dati per l'importazione del feed di dati nell'applicazione client di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , sono necessarie solo autorizzazioni di visualizzazione per il documento. Le autorizzazioni di visualizzazione sono sufficienti per risolvere l'URL nell'importazione guidata.  
  
 Le autorizzazioni di visualizzazione per un documento di servizio dati vengono controllate solo all'inizio di un'operazione di importazione di feed di dati. Dopo l'importazione, le autorizzazioni per il documento non vengono controllate continuamente. I feed aggiunti a un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sono presenti come dati statici, disconnessi dal documento di servizio dati che ha fornito le informazioni di connessione originali.  
  
 Allo stesso modo, nelle operazioni di aggiornamento dei dati pianificate successivamente non è incluso il documento di servizio dati. Al momento dell'importazione, le informazioni di connessione per ogni feed vengono copiate nell'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per l'aggiornamento. Analogamente, le autorizzazioni per un documento di servizio dati non vengono verificate per l'aggiornamento dei dati, perché al documento non viene mai fatto riferimento in un'operazione di aggiornamento.  
  
|Attività|Requisiti relativi all'autorizzazione di SharePoint|  
|----------|----------------------------------------|  
|Importare i feed di dati in una cartella di lavoro abilitata per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|Autorizzazioni di visualizzazione per il documento di servizio dati in una raccolta.|  
|Nell'applicazione client di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aggiornare i dati recuperati precedentemente con il feed.|Non applicabile. L'applicazione client di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa informazioni di connessione HTTP incorporate per connettersi direttamente ai servizi dati e alle applicazioni che forniscono il feed. L'applicazione client di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] non usa il documento di servizio dati.|  
|In una farm di SharePoint, l'aggiornamento dei dati viene eseguito come attività programmata e l'input dell'utente non è richiesto.|Non applicabile. Il servizio di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa informazioni di connessione HTTP incorporate per connettersi direttamente ai servizi dati e alle applicazioni che forniscono il feed. Il servizio di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] non usa il documento di servizio dati.|  
|Eliminare un documento di servizio dati in una libreria|Autorizzazioni di collaborazione nella libreria.|  
  
##  <a name="modifydsdoc"></a> Modificare un documento di servizio dati  
 È possibile aggiungere, modificare o rimuovere singole voci URL-tabella in un documento di servizio dati. Dopo il salvataggio delle modifiche, gli utenti che selezionano il documento di servizio in una nuova operazione di importazione otterranno i feed di dati specificati.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nelle quali era utilizzata una versione precedente del documento. Ciò è dovuto al fatto che un documento di servizio dati viene letto solo una volta durante l'operazione di importazione iniziale. Durante l'importazione, l'URL del servizio e i nomi di tabella vengono copiati e archiviati internamente nella cartella di lavoro. Questi valori interni vengono quindi utilizzati in operazioni di aggiornamento successive per ottenere dati aggiornati.  
  
 Poiché non è disponibile un collegamento persistente tra un documento di servizio dati in un sito di SharePoint e la cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in cui è contenuto il feed importato, la modifica di qualsiasi parte di un documento di servizio dati non ha effetto nelle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] esistenti.  
  
> [!IMPORTANT]  
>  Anche se il documento di servizio dati viene letto una sola volta, l'accesso ai servizi dati tramite cui vengono forniti i dati effettivi può essere eseguito a intervalli regolari per ottenere feed più recenti. Per altre informazioni su come aggiornare i dati, vedere [Aggiornamento dati Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md).  
  
##  <a name="usedsdoc"></a> Passaggio successivo: Usare un documento di servizio dati  
 Per usare un documento di servizio dati creato in una raccolta di SharePoint, usare l'opzione di importazione **Da feed di dati** in un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per istruzioni, vedere [Usare feed di dati &#40;PowerPivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Feed di dati Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  
