---
title: Risolvere i problemi di rendering del report di Reporting Services | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: 1e0fb399-4c16-438a-92cb-db3e877896d0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3f8c5029d66a068d43ebc659592697fd2914fd2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574690"
---
# <a name="troubleshoot-reporting-services-report-rendering-issues"></a>Risolvere i problemi di rendering del report di Reporting Services
Dopo che le informazioni sul layout e i dati del report sono stati combinati, il report compilato viene inviato a un renderer di report. Ad esempio, quando si visualizza in anteprima un report in locale, si utilizza il renderer HTML per visualizzare il report compilato. Utilizzare le informazioni riportate in questo argomento per risolvere i problemi specifici del rendering del report.   
  
## <a name="why-do-i-have-extra-white-space-including-blank-pages-in-my-report"></a>Nel report è presente spazio vuoto aggiuntivo, incluse pagine vuote  
Gli elementi del report vengono regolati automaticamente durante l'elaborazione del report per conservare lo spazio vuoto definito come parte del report. Lo spazio vuoto viene conservato nella visualizzazione Progettazione del report. Nell'area di progettazione del report, lo sfondo bianco rappresenta spazio vuoto che verrà mantenuto durante la visualizzazione, l'esportazione o la stampa di un report, a seconda del supporto di destinazione.  
  
### <a name="white-space-and-page-breaks-interact-during-rendering"></a>Lo spazio vuoto e le interruzioni di pagina interagiscono durante l'esecuzione il rendering  
Quando si visualizza un report o si esporta il report in un formato di file, l'estensione per il rendering associata elabora il report e lo salva nel formato di file specificato. Ogni estensione per il rendering elabora lo spazio vuoto in un report sulla base di regole specifiche. Lo spazio vuoto varia anche in base alle proprietà dell'impostazione di pagina, alle interruzioni di pagina impostate per gli elementi del report, alla posizione relativa degli elementi del report nel corpo del report, alla proprietà KeepTogether per determinati elementi del report e agli elementi del report se sono nei contenitori padre.   
  
Per eliminare eventuali pagine aggiuntive a causa della larghezza del report, trascinare il bordo dell'area di progettazione del report per allinearlo con l'elemento del report più esterno. Per un layout del report da sinistra verso destra, trascinare il bordo destro da allineare con l'elemento del report più esterno. Per altre informazioni, vedere [Tipi di rendering](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
### <a name="white-space-is-not-preserved-at-the-end-of-a-report"></a>Lo spazio vuoto non è mantenuto alla fine di un report  
Reporting Services fornisce un'opzione che consente di controllare se mantenere o eliminare lo spazio vuoto alla fine di un report.   
  
Per mantenere lo spazio vuoto alla fine di un report, selezionare il report e nel riquadro Proprietà, scorrere fino a ConsumeContainerWhitespace e digitare False.   
  
## <a name="why-do-my-reports-look-different-when-exported-to-different-formats"></a>Perché i report hanno un aspetto diverso quando vengono esportati in formati diversi?  
Dopo aver eseguito un report, è possibile esportarlo in un altro formato, ad esempio Excel, Word o PDF. A seconda del formato nel quale si esporta il report, potrebbero applicarsi determinate regole e limitazioni. È possibile superare molte limitazioni semplicemente tenendole presenti durante la creazione del report. Potrebbe essere necessario usare un layout leggermente diverso nel report, allineare con cura gli elementi all'interno del report, limitare i piè di pagina del report a una sola riga di testo e così via. È inoltre possibile utilizzare l'elemento globale predefinito RenderFormat per applicare in modo condizionale un layout del report diverso per renderer diversi. Altre variabili globali predefinite possono consentire di gestire la paginazione nel formato esportato e di denominare le schede del foglio di lavoro in Excel. Per altre informazioni, vedere [Esportazione di report](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) e [Riferimenti alle raccolte predefinite Globals e Users](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
## <a name="how-can-i-view-all-my-report-data-on-one-page"></a>Modalità di visualizzazione di tutti i dati del report in una pagina  
Per una visualizzazione interattiva dei report in cui non sono presenti quantità di dati elevate, è possibile che si desideri visualizzare tutti i dati in una pagina.   
  
Per i renderer con interruzioni di pagina automatiche, per visualizzare tutti i dati in una pagina, impostare InteractiveHeight su 0 nelle proprietà Report. Nei renderer con interruzioni di pagina automatiche, le interruzioni di pagina esistenti vengono ignorate.   
  
> [!NOTE]  
> Quando un report non contiene interruzioni di pagina, è necessario elaborare l'intero report prima che la prima pagina venga visualizzata.   
  
Per altre informazioni sulle categorie di renderer, vedere [Tipi di rendering](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="reports-do-not-run-when-your-browser-is-configured-to-prompt-for-credentials"></a>I report non vengono eseguiti quando il browser è configurato per richiedere per le credenziali  
La visualizzazione dei report potrebbe non riuscire determinando la visualizzazione di un messaggio di errore quando il browser è configurato per richiedere le credenziali e l'origine dati viene configurata per l'autenticazione di Windows integrata. Questa situazione si verifica quando l'origine dati si trova in un computer separato dal server di report, l'origine dati è configurata per utilizzare Autenticazione di Windows e il browser è impostato per richiedere per le credenziali. Di seguito sono riportati alcuni esempi dei messaggi che verranno visualizzati.  
  
Quando l'origine dati è configurata per un tipo di connessione Microsoft SQL Server:  
`An error has occurred during report processing.`  
`Cannot create a connection to data source 'localhost'.`  
`Login failed for user '(null)'. Reason: Not associated with a trusted SQL Server connection.`  
  
Quando l'origine dati è configurata per un tipo di connessione Elenco Microsoft SharePoint:  
`An error occurred during client rendering.`   
`An error has occurred during report processing.`   
`Query execution failed for dataset 'DataSet1'.`   
`The request failed with HTTP status 401: Unauthorized.`  
  
**Per risolvere questo problema:** modificare l'origine dati per l'uso delle credenziali archiviate anziché delle credenziali di Windows.  
  
**Questo problema si applica a:** browser configurati per richiedere le credenziali.  
  
## <a name="see-also"></a>Vedere anche  
[Errori ed eventi (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Risolvere i problemi di recupero dei dati con i report di Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Risolvere i problemi di sottoscrizioni e recapito di Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

