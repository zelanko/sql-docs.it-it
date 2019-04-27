---
title: Esempi di URL per elementi di Report pubblicati in un Server di Report in modalità SharePoint (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 54cb861a-8cec-445c-875d-599fb9bd1973
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1b958a1552bf979abfcebd16345768ea2f7f5fed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657438"
---
# <a name="url-examples-for-published-report-items-on-a-report-server-in-sharepoint-mode-ssrs"></a>Esempi di URL per elementi di report pubblicati in un server di report in modalità SharePoint (SSRS)
  Per pubblicare report ed elementi correlati in una raccolta di SharePoint, è possibile pubblicare il contenuto mediante gli strumenti di creazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], ad esempio Progettazione report, oppure caricare il contenuto tramite le azioni sito di SharePoint.  
  
 Per i siti di SharePoint vengono usati indirizzi Web diversi rispetto a un server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa. In una gerarchia Web di un sito di SharePoint sono inclusi l'applicazione Web di SharePoint, un sito principale, eventuali siti secondari e raccolte. È necessario conoscere la procedura per la creazione di un indirizzo URL che specifichi il server di SharePoint, nonché il percorso nella gerarchia dei siti di SharePoint in cui si desidera pubblicare un report o elementi correlati.  
  
 Gli elementi correlati a un report includono origini dati condivise, sottoreport, report drill-through e risorse quali file di immagine Web. In un report pubblicato in una raccolta di SharePoint questi elementi correlati devono essere specificati tramite il percorso nella raccolta di SharePoint.  
  
 Utilizzare gli esempi di questo argomento per creare URL per report ed elementi correlati nelle soluzioni di report.  
  
## <a name="site-hierarchy"></a>Gerarchia dei siti  
 Quando si configura un server di report per l'esecuzione in modalità integrata SharePoint, per fare riferimento agli elementi elaborati e gestiti in un server di report viene utilizzata la gerarchia Web di SharePoint.  
  
 Per accedere al contenuto del server di report e proteggerlo, è possibile utilizzare gli elementi della gerarchia Web indicati di seguito. Altri oggetti, quali elenchi e pagine, non vengono utilizzati per accedere al contenuto del server di report e non sono pertanto descritti nella tabella seguente.  
  
|Object|Descrizione|  
|------------|-----------------|  
|Applicazione Web di SharePoint|Le applicazioni Web di SharePoint possono essere installate come server autonomi o in una farm contenente una raccolta di server virtuali. Un'applicazione Web dispone di un URL, ad esempio http:*//nomeserver*, e può contenere più siti.|  
|Sito|Un sito può essere un sito padre o un sito secondario di un'applicazione Web.|  
|Raccolta di SharePoint|Una raccolta contiene documenti o cartelle. Gli unici oggetti di un sito nei quali possono essere archiviati report, origini dei dati condivise e immagini esterne sono le raccolte o le cartelle.|  
|Elemento|Gli elementi del server di report ai quali è possibile fare riferimento in un URL includono definizione di report o sottoreport, modelli di report, origini dei dati condivise o immagini esterne.|  
  
## <a name="url-syntax-and-rules"></a>Sintassi e regole per gli URL  
 Ogni elemento del server di report incluso in una raccolta viene identificato da un URL completo che include un prefisso di protocollo, il nome del server, il sito, la raccolta, il nome file e la relativa estensione.  
  
### <a name="url-for-a-sharepoint-server"></a>URL per un server di SharePoint  
 Quando si distribuisce un progetto modello di report o server di report da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] al server di report, è necessario utilizzare un URL del server di SharePoint.  
  
 Per trovare il nome del server da utilizzare, aprire un browser e individuare la raccolta di SharePoint in cui si desidera pubblicare un report. Il nome del server si trova immediatamente dopo il prefisso del protocollo, ad esempio http:*//nomeserver*.  
  
 L'utilizzo dell'endpoint proxy dell'URL di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è supportato. Gli endpoint proxy includono un numero di porta, ad esempio http:*//nomeserver:8080/reportserver*.  
  
### <a name="url-for-a-sharepoint-server-site-or-subsite"></a>URL per un sito o un sito secondario di SharePoint Server  
 Quando si distribuisce un report o un'origine dati del report, è necessario utilizzare un URL del sito e dell'eventuale sito secondario di SharePoint. Nell'URL il nome del sito si trova immediatamente dopo il nome del server, ad esempio http://*nomeserver/sito* o http://*nomeserver/sito/sitosecondario*.  
  
 In un'applicazione Web di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] il sito e il sito secondario corrispondono spesso alle schede nel sito principale. Per trovare il nome del sito o del sito secondario, fare clic su **Home**e quindi su **Tutto il contenuto del sito**. Scorrere fino alla fine e cercare **Siti e aree di lavoro**. L'elenco dei siti si trova in questa sezione.  
  
### <a name="url-for-a-sharepoint-library"></a>URL di una raccolta di SharePoint  
 Quando si distribuisce un report o un elemento correlato in una raccolta di SharePoint, è necessario utilizzare l'URL di quest'ultima. L'URL da utilizzare per una raccolta varia a seconda della versione di SharePoint in uso.  
  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 o [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]la raccolta è indicata dopo il nome del server, ad esempio http://*nomeserver/* Documenti condivisi.  
  
 In [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]la raccolta è invece indicata dopo il sito e il sito secondario. Ad esempio, http://*nomeserver/sito/* Documenti.  
  
 Per trovare le informazioni sul percorso di una nuova raccolta di SharePoint o per un sito con cui non si ha familiarità, aprire un browser e individuare la raccolta di SharePoint in cui si desidera pubblicare i report. Se la raccolta è vuota, caricare uno o più file. Fare clic con il pulsante destro del mouse sul file e scegliere **Proprietà** per aprire la finestra **Proprietà** . L'indirizzo del file include i valori dell'URL necessari per l'operazione di pubblicazione.  
  
### <a name="fully-qualified-urls-for-items-on-a-sharepoint-site"></a>URL completi per gli elementi di un sito di SharePoint  
 Agli elementi archiviati in una raccolta di SharePoint sono sempre associati indirizzi rappresentati da URL completi che iniziano con l'applicazione Web (http://*server*) in qualità di nodo radice e terminano con il nome del file a cui si fa riferimento.  
  
 I nomi file nell'URL devono includere l'estensione.  
  
 Non è possibile utilizzare URL relativi per elementi dipendenti di report che si pubblicano in un sito di SharePoint. Ad esempio, non è possibile utilizzare un URL relativo per fare riferimento a un'origine dei dati condivisa, un modello di report o un sottoreport. È sempre necessario specificare l'URL completo di una raccolta di SharePoint per ogni elemento. Non esiste alcun modo per prevedere la posizione di un file dipendente, poiché non esiste una gerarchia predefinita dei siti da utilizzare per analizzare un formato URL.  
  
 Quando si pubblica o carica un report contenente elementi dipendenti, è necessario impostare i riferimenti agli elementi dipendenti dopo la pubblicazione del report. Non è garantito che i riferimenti che funzionavano correttamente nella modalità di anteprima di Progettazione report funzionino anche dopo la pubblicazione del report. Per altre informazioni, vedere [Pubblicazione da uno strumento di creazione in una raccolta di SharePoint](#publishingToDocLib) in questo argomento.  
  
### <a name="urls-for-external-images"></a>URL per immagini esterne  
 Una definizione di report può includere un file di immagine archiviato come file esterno. È possibile fare riferimento al file nella definizione del report impostando l'URL completo del file di immagine. Il file può essere archiviato in un sito di SharePoint o in un computer remoto.  
  
> [!IMPORTANT]  
>  Se l'URL esterno è per un'immagine in un sito di SharePoint, verrà visualizzata l'icona di immagine interrotta quando si visualizza in anteprima il report in Generatore report. Quando si carica il report nel sito di SharePoint e si esegue il rendering del report nella modalità connessa, verrà visualizzata l'icona di immagine interrotta se si dispone solo delle autorizzazioni `View Items`.  
  
 Indipendentemente dalla modalità del server di report, i riferimenti a un file di immagine esterno inclusi in un report devono essere rappresentati da URL completi. Inoltre, in genere il riferimento a un file di immagine esterno richiede la configurazione dell'account per l'esecuzione automatica del report.  
  
### <a name="specifying-subreports-and-drillthrough-reports"></a>Specifica di sottoreport e report drill-through  
 I sottoreport devono trovarsi nella stessa cartella del report principale. Non è possibile specificare una cartella relativa.  
  
 Per specificare un report drill-through, includere l'URL in un'espressione. Ad esempio per specificare il report denominato SalesDetails come report drill-through, nell'azione per la casella di testo o il testo segnaposto, impostare ReportName sull'espressione seguente:  
  
```  
="http://site/subsite/documentlibrary/SalesDetails.rdl"  
```  
  
### <a name="reserved-names-on-sharepoint-sites"></a>Nomi riservati in siti di SharePoint  
 Se si crea o si costruisce l'URL di un elemento che si trova in un sito di SharePoint, tenere presente che le parole **Personale** e **Siti** sono entrambe nomi riservati nel sito predefinito.  
  
## <a name="examples-of-urls"></a>Esempi di URL  
 Quando si pubblicano elementi in una raccolta di SharePoint, è necessario specificare gli URL completi della raccolta di destinazione. Negli URL completi di SharePoint sono inclusi l'applicazione Web, il sito, la raccolta, la cartella (facoltativo), il nome file e la relativa estensione. Nell'esempio seguente vengono illustrati vari esempi della sintassi che è necessario utilizzare:  
  
|Destinazione|URL di esempio|  
|------------|-----------------|  
|Un server di SharePoint.|http://TestServer|  
|Un sito o sito secondario del server di SharePoint.|http://TestServer/toplevelsite/subsite|  
|Il report di esempio Company Sales in **Documenti condivisi** in una distribuzione di [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] o [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] .|http://TestServer/TestSite/Shared%20Documents/Company%20Sales.rdl|  
|Il report di esempio Company Sales nella cartella **Documents/Doc** in un'istanza di [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] .|http://TestServer/TestSite/Documents/Doc/Company%20Sales.rdl|  
|Il report di esempio Company Sales in un **Centro report** in un'istanza di [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] .|http://TestServer/TestSite/Reports/Doc/Company%20Sales.rdl|  
  
##  <a name="publishingToDocLib"></a> Pubblicazione da uno strumento di creazione in una raccolta di SharePoint  
 Quando per pubblicare in una raccolta i report e i file correlati si utilizza uno strumento di creazione dei report, i file vengono convalidati prima di essere aggiunti. Se invece si caricano i report e i file correlati usando l'azione **Carica** in una raccolta di SharePoint, non viene eseguito alcun controllo di convalida. In questo caso, non sarà possibile sapere se il file è valido fino a quando non si accederà al report per gestirlo, modificarlo o eseguirlo.  
  
> [!NOTE]  
>  Per pubblicare i report in un sito di SharePoint da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], potrebbe essere necessario aggiungere il sito di SharePoint all'elenco dei siti attendibili nel browser Internet Explorer.  
  
### <a name="shared-data-sources"></a>Origini dati condivise  
 Quando si pubblica un'origine dati condivisa da uno strumento di creazione report, si imposta la proprietà di progetto `TargetDataSourceFolder`. La cartella dell'origine dei dati di destinazione deve corrispondere a un URL di una raccolta di SharePoint. A differenza di quanto avviene in modalità nativa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , non è possibile specificare una cartella relativa. I percorsi relativi non sono validi. Se nel percorso Raccolta documenti non è presente alcuna cartella, ne verrà creata una.  
  
 Quando si pubblica un file dell'origine dei dati condivisa (con estensione rds) in un sito di SharePoint, l'estensione del file viene cambiata in rsds. Non è possibile salvare il file con estensione rsds in locale da un sito di SharePoint né importarlo in un progetto di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] esistente. Le origini dei dati condivise con estensione rds e rsds non sono interscambiabili.  
  
#### <a name="shared-data-sources-from-report-designer"></a>Origini dei dati condivise da Progettazione report  
 Se si pubblicano origini dei dati condivise da un progetto di Progettazione report, è possibile utilizzare un URL che indichi la raccolta di destinazione oppure lasciare vuota tale proprietà. A differenza di quanto avviene in modalità nativa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , non è possibile specificare una cartella relativa. I percorsi relativi non sono validi. Se nel percorso Raccolta documenti non è presente alcuna cartella, ne verrà creata una. Se si lascia vuota la cartella dell'origine dei dati di destinazione, l'origine dati verrà pubblicata nella cartella del report di destinazione.  
  
### <a name="file-names"></a>Nomi file  
 I nomi file inclusi negli URL degli elementi di report devono includere l'estensione. L'estensione del nome file determina il tipo di file. Quando si pubblicano elementi del report da uno strumento di creazione, l'estensione viene automaticamente aggiunta al nome file. Se si carica un elemento di report in una raccolta di SharePoint, è necessario aggiungere un'estensione al nome file.  
  
 In caso contrario, si verificherà l'errore `rsInvalidDataSourceReference`. I nomi di file non possono includere caratteri non riconosciuti come validi per i nomi di file dalle applicazioni di SharePoint. Non includere i seguenti caratteri: # % & *: \< >? / { | }.  
  
## <a name="differences-between-uploading-and-publishing"></a>Differenze tra caricamento e pubblicazione  
 Quando per pubblicare in una raccolta i report e i file correlati si utilizza Progettazione report o Generatore report, i file vengono convalidati prima di essere aggiunti. Se invece si caricano i report e i file correlati usando l'azione **Carica** in una raccolta di SharePoint, non viene eseguito alcun controllo di convalida. In questo caso, non sarà possibile sapere se il file è valido fino a quando non si accederà al report per gestirlo, modificarlo o eseguirlo.  
  
## <a name="updating-a-published-item"></a>Aggiornamento di un elemento pubblicato  
 Dopo aver pubblicato o caricato un elemento in una raccolta di SharePoint, è consigliabile estrarre l'elemento dalla raccolta prima di aggiornarlo. L'utente da cui è estratto il report sarà l'unico a disporre delle autorizzazioni per modificarlo. Al termine delle modifiche, è consigliabile archiviare nuovamente il report.  
  
 Se si carica o pubblica un report senza prima estrarlo (ad esempio, caricando un elemento con lo stesso nome di uno già esistente), il server di report lo estrarrà per l'utente, aggiungerà il report aggiornato come nuova versione dell'elemento esistente, quindi lo archivierà nuovamente.  
  
## <a name="external-images-as-resources"></a>Immagini esterne come risorse  
 Un server di report eseguito in modalità nativa supporta il concetto di risorsa, ovvero qualsiasi file archiviato e protetto nel server di report ma non elaborato da tale server. In modalità nativa, una risorsa può essere un file di qualsiasi tipo.  
  
 Quando un server di report viene eseguito in modalità integrata SharePoint, il concetto di risorsa è più limitato. In questo caso il concetto di risorsa viene utilizzato per l'archiviazione di report che fanno riferimento a un'immagine esterna. Ciò è valido se il report è uno snapshot o una copia mantenuta per uso interno.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare un report in una raccolta di SharePoint](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [Pubblicare un'origine dati condivisa in una raccolta di SharePoint](../reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Finestra di dialogo Pagine delle proprietà del progetto](project-property-pages-dialog-box.md)  
  
  
