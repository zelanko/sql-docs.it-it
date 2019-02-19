---
title: Riferimenti alle raccolte predefinite Globals e Users (Generatore report e SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5f5e1149-c967-454d-9a63-18ec4a33d985
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1bdfb2cfca82df57d76c321957bbcb565fb2b058
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56298439"
---
# <a name="built-in-collections---built-in-globals-and-users-references-report-builder"></a>Raccolte predefinite - Riferimenti alle raccolte predefinite Globals e Users (Generatore report)
  La raccolta di campi predefinita, in cui sono incluse le raccolte **Globals** e **User** , rappresenta i valori globali forniti da Reporting Services durante l'elaborazione di un report. La raccolta **Globals** fornisce valori come il nome del report, l'ora di inizio dell'elaborazione e i numeri di pagina correnti per l'intestazione o il piè di pagina. La raccolta **User** fornisce le impostazioni relative a ID utente e lingua. Questi valori possono essere usati nelle espressioni per filtrare i risultati in un report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-globals-collection"></a>Utilizzo della raccolta Globals  
 La raccolta **Globals** contiene le variabili globali per il report. Nell'area di progettazione queste variabili sono precedute dal prefisso & (e commerciale), ad esempio `[&ReportName]`. Nella tabella seguente vengono descritti i membri della raccolta **Globals** .  
  
|**Membro**|**Tipo**|**Descrizione**|  
|----------------|--------------|---------------------|  
|ExecutionTime|**DateTime**|Data e ora di inizio dell'esecuzione del report.|  
|PageNumber|**Integer**|Numero di pagina corrente relativo a interruzioni di pagina che ne determinano la reimpostazione. All'inizio dell'elaborazione del report, il valore è impostato su 1. Il numero di pagina aumenta per ogni pagina di cui è stato eseguito il rendering.<br /><br /> Per numerare le pagine all'interno di interruzioni di pagina per un rettangolo, un'area dati, un gruppo di aree dati o una mappa, nella proprietà PageBreak impostare la proprietà ResetPageNumber su **True**. Non supportato dai gruppi di gerarchie di colonna Tablix.<br /><br /> La proprietà PageNumber può essere usata solo in espressioni presenti in un'intestazione o un piè di pagina.|  
|ReportFolder|**String**|Percorso completo della cartella contenente il report. Non include l'URL del server di report.|  
|ReportName|**String**|Nome del report archiviato nel database del server di report.|  
|ReportServerUrl|**String**|URL del server di report in cui il report è in esecuzione.|  
|TotalPages|**Integer**|Numero totale di pagine relativo alle interruzioni di pagina che determinano la reimpostazione di PageNumber. Se non sono impostate interruzioni di pagina, questo valore corrisponde a OverallTotalPages.<br /><br /> La proprietà TotalPages può essere usata solo in espressioni presenti in un'intestazione o un piè di pagina.|  
|PageName|**String**|Nome della pagina. All'inizio dell'elaborazione del report, il valore viene impostato da una proprietà del report, InitialPageName. Quando ciascun elemento del report viene elaborato, questo valore viene sostituito con il valore corrispondente di PageName da un rettangolo, un'area dati, un gruppo di aree dati o una mappa. Non supportato dai gruppi di gerarchie di colonna Tablix.<br /><br /> La proprietà PageName può essere usata solo in espressioni presenti in un'intestazione o un piè di pagina.|  
|OverallPageNumber|**Valore intero**|Numero della pagina corrente per l'intero report. ResetPageNumber non ha effetto su questo valore.<br /><br /> La proprietà OverallPageNumber può essere usata solo in espressioni presenti in un'intestazione o un piè di pagina.|  
|OverallTotalPages|**Integer**|Numero complessivo di pagine per l'intero report. ResetPageNumber non ha effetto su questo valore.<br /><br /> La proprietà OverallTotalPages può essere usata solo in espressioni presenti in un'intestazione o un piè di pagina.|  
|RenderFormat|**RenderFormat**|Informazioni sulla richiesta di rendering corrente.<br /><br /> Per altre informazioni, vedere "RenderFormat" nella sezione successiva.|  
  
 I membri della raccolta **Globals** restituiscono una variante. Se si desidera usare un membro di questa raccolta in un'espressione che richiede un tipo di dati specifico, è necessario eseguire dapprima il cast della variabile. Per convertire, ad esempio, la variante relativa alla data e all'ora di esecuzione in un formato di data, usare `=CDate(Globals!ExecutionTime)`. Per altre informazioni, vedere [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md).  
  
### <a name="renderformat"></a>RenderFormat  
 Nella tabella seguente vengono descritti i membri per **RenderFormat**.  
  
|Membro|Tipo|Descrizione|  
|------------|----------|-----------------|  
|nome|**String**|Nome del renderer come registrato nel file di configurazione RSReportServer.<br /><br /> Disponibile durante determinate parti del ciclo di elaborazione/rendering del report.|  
|IsInteractive|**Boolean**|Specifica se nella richiesta di rendering corrente è usato un formato di rendering interattivo.|  
|DeviceInfo|Raccolta nome/valore di sola lettura|Coppie chiave/valore per i parametri deviceinfo per la richiesta di rendering corrente.<br /><br /> È possibile specificare i valori stringa usando la chiave o un indice nella raccolta.|  
  
### <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato come usare un riferimento alla raccolta **Globals** in un'espressione:  
  
-   L'espressione seguente, inserita in una casella di testo nel piè di pagina di un report, restituisce il numero di pagina e le pagine totali del report:  
  
     `=Globals.PageNumber & " of " & Globals.TotalPages`  
  
-   Questa espressione restituisce il nome e l'ora di esecuzione del report. Per la formattazione dell'ora viene usata la stringa di formattazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per la data breve:  
  
     `=Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")`  
  
-   Con questa espressione, inserita nella finestra di dialogo **Visibilità colonne** per una colonna selezionata, viene visualizzata la colonna solo quando il report viene esportato in Excel. In caso contrario, è nascosta.  
  
     `EXCELOPENXML` si riferisce al formato di Excel incluso in Office 2007. `EXCEL` si fa riferimento al formato di Excel incluso in Office 2003.  
  
     `=IIF(Globals!RenderFormat.Name = "EXCELOPENXML" OR Globals!RenderFormat.Name = "EXCEL", false, true)`  
  
## <a name="using-the-user-collection"></a>Utilizzo della raccolta User  
 La raccolta **User** contiene i dati relativi all'utente che esegue il report. È possibile usare questa raccolta per filtrare i dati visualizzati in un report, per mostrare, ad esempio, solo quelli dell'utente corrente o visualizzare l'ID utente nel titolo del report. Nell'area di progettazione queste variabili sono precedute dal prefisso & (e commerciale), ad esempio `[&UserID]`.  
  
 Nella tabella seguente vengono descritti i membri della raccolta **User** .  
  
|**Membro**|**Tipo**|**Descrizione**|  
|----------------|--------------|---------------------|  
|**Lingua**|**String**|Lingua dell'utente che esegue il report. Ad esempio, `en-US`.|  
|**UserID**|**String**|ID dell'utente che esegue il report. Se si usa l'autenticazione di Windows, questo valore corrisponde all'account di dominio dell'utente corrente. Il valore è determinato dall'estensione di sicurezza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , che può usare l'autenticazione di Windows o quella personalizzata.|  
 
### <a name="using-locale-settings"></a>Utilizzo delle impostazioni locali  
 È possibile usare espressioni per fare riferimento alle impostazioni locali in un computer client tramite il valore **User.Language** , in modo da determinare la modalità di visualizzazione di un report all'utente. È possibile, ad esempio, creare un report in cui venga usata un'espressione di query diversa basata sul valore delle impostazioni locali. La query può essere modificata per recuperare informazioni localizzate da una colonna diversa, a seconda della lingua restituita. È inoltre possibile usare un'espressione per modificare le impostazioni relative alla lingua del report o degli elementi del report in base a questa variabile.  
  
> [!NOTE]  
>  Benché sia possibile modificare le impostazioni relative alla lingua di un report, è necessario assicurarsi che tale modifica non causi problemi di visualizzazione. La modifica delle impostazioni locali del report potrebbe ad esempio comportare la modifica del formato della data nel report, ma anche la modifica del formato della valuta. A meno che non sia previsto un processo di conversione per la valuta, in questi casi è possibile che nel report venga visualizzato il simbolo di valuta errato. Per evitare tale problema, impostare le informazioni sulla lingua nei singoli elementi da modificare oppure impostare una lingua specifica per l'elemento contenente i dati relativi alla valuta.  
  
### <a name="identifying-userid-for-snapshot-or-history-reports"></a>Identificazione di UserID per i report relativi a snapshot o cronologia  
 Nei report che includono la variabile *User!UserID* è talvolta possibile che non vengano inclusi i dati specifici dell'utente che sta visualizzando il report.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Finestra di dialogo Espressione &#40;Generatore report&#41;](https://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
