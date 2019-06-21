---
title: Differenze di funzionamento di Analysis Services Features in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a5525984fa4b1f1823f526097d271780a072bd4
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284805"
---
# <a name="behavior-changes-to-analysis-services-features-in-sql-server-2014"></a>Differenze di funzionamento delle funzionalità di Analysis Services in SQL Server 2014
  Questo argomento descrive le modifiche del comportamento in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per le distribuzioni multidimensionali, tabulari, di data mining e di [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] . Tali modifiche influiscono sulle modalità di utilizzo o di interazione delle funzionalità nella versione corrente rispetto alle versioni precedenti di SQL Server.  
  
> [!NOTE]  
>  Al contrario, una modifica di rilievo impedisce l'esecuzione di un modello di dati o di un'applicazione integrata con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Per altre informazioni, vedere [Breaking Changes to Analysis Services Features in SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md).  
  
 Contenuto dell'argomento:  
  
-   [Modifiche del comportamento in SQL Server 2014](#bkmk_sql2014)  
  
-   [Modifiche del comportamento in SQL Server 2012 SP1](#bkmk_sql2012sp1)  
  
-   [Modifiche del comportamento in SQL Server 2012](#bkmk_sql2012)  
  
##  <a name="bkmk_sql2014"></a> Modifiche del comportamento in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 In questa versione non sono annunciate nuove modifiche del comportamento per le funzionalità tabulari, multidimensionali, di data mining o di [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] .  Tuttavia, considerata l'analogia di  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] con le versioni [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] , le modifiche del comportamento rispetto a entrambe le versioni precedenti sono elencate qui per praticità, nel caso si effettui l'aggiornamento da [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="bkmk_sql2012sp1"></a> Modifiche del comportamento in [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]  
 Questa sezione illustra le modifiche del comportamento riportate per le funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]. Le modifiche si applicano anche a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
|Problema|Descrizione|  
|-----------|-----------------|  
|Tramite le cartelle di lavoro di SQL Server 2008 R2 PowerPivot non verranno aggiornati in modo automatico i modelli quando vengono utilizzati in SQL Server 2012 SP1 PowerPivot per SharePoint 2013. Pertanto, gli aggiornamenti dati pianificati non funzioneranno per le cartelle di lavoro di SQL Server 2008 R2 PowerPivot.|Le cartelle di lavoro della versione 2008 R2 verranno aperte in [!INCLUDE[ssGeminiShortvnext](../includes/ssgeminishortvnext-md.md)], ma gli aggiornamenti pianificati non funzioneranno. Se si esamina la cronologia degli aggiornamenti, verrà visualizzato un messaggio di errore simile al seguente:<br /> "La cartella di lavoro contiene un modello PowerPivot non supportato. Il modello PowerPivot nella cartella di lavoro è nel formato di SQL Server 2008 R2 PowerPivot per Excel 2010. Sono supportati i modelli PowerPivot seguenti: <br />SQL Server 2012 PowerPivot per Excel 2010<br />SQL Server 2012 PowerPivot for Excel 2013"<br /><br /> **Come aggiornare una cartella di lavoro:** Gli aggiornamenti pianificati non funzioneranno finché non viene aggiornata la cartella di lavoro alla relativa versione 2012. Per aggiornare la cartella di lavoro e il modello in essa contenuto, completare una delle operazioni seguenti:<br /><br /> Scaricare e aprire la cartella di lavoro in Microsoft Excel 2010 con il componente aggiuntivo SQL Server 2012 PowerPivot per Excel installato. Successivamente, salvare la cartella di lavoro e ripubblicarla nel server SharePoint.<br /><br /> Scaricare e aprire la cartella di lavoro in Microsoft Excel 2013. Successivamente, salvare la cartella di lavoro e ripubblicarla nel server SharePoint.<br /><br /> <br /><br /> Per altre informazioni sull'aggiornamento della cartella di lavoro, vedere [cartelle di lavoro di eseguire l'aggiornamento e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).|  
|Modifiche del comportamento nella [ALL Function](/dax/all-function-dax)di DAX.|Nelle versioni precedenti a [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)], se si specifica una colonna [Date] in Contrassegna come tabella data per l'utilizzo nelle funzionalità di Business Intelligence per le gerarchie temporali, e tale colonna [Date] viene passata come argomento alla funzione ALL, passata a sua volta come filtro di una funzione CALCULATE, tutti i filtri di tutte le colonne della tabella vengono ignorati, indipendentemente dalla presenza di eventuali filtri dei dati nella colonna data.<br /><br /> Ad esempio,<br /><br /> `= CALCULATE (<expression>, ALL (DateTable[Date]))`<br /><br /> Nelle versioni precedenti a [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)], vengono ignorati tutti i filtri per tutte le colonne DateTable, indipendentemente dalla colonna [Date] passata come argomento alla funzione ALL.<br /><br /> In [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] e in PowerPivot in Excel 2013, il comportamento prevede che i filtri vengano ignorati solo per la colonna specifica passata come argomento alla funzione ALL.<br /><br /> Come alternativa al nuovo comportamento e ignorare tutte le colonne come filtro per l'intera tabella, è possibile escludere la colonna [Date] dall'argomento, ad esempio:<br /><br /> `=CALCULATE (<expression>, ALL(DateTable))`<br /><br /> Ciò produce lo stesso risultato del comportamento precedente a [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)].|  
  
##  <a name="bkmk_sql2012"></a> Modifiche del comportamento in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 In questa sezione sono illustrate le modifiche del comportamento riportate per le funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Le modifiche si applicano anche a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
### <a name="analysis-services-multidimensional-mode"></a>Analysis Services, modalità multidimensionale  
  
#### <a name="nullprocessing-option-set-to-preserve-is-no-longer-supported-for-distinct-count-measures"></a>L'opzione NullProcessing impostata su Preserve non è più supportata per le misure Distinct Count  
 Nelle versioni precedenti a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], è possibile impostare [elemento NullProcessing &#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl) al `Preserve` per le misure distinct count.  Purtroppo questa impostazione produce spesso risultati non validi e a volte causa addirittura l'arresto anomalo del processo di elaborazione. Di conseguenza, questa configurazione non è più valida in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Tentando di usare causerà l'errore di convalida seguente: "Errori nella gestione metadati. Preserve non è un valore valido di NullProcessing per la \<measurename > misura distinct count. "  
  
#### <a name="cube-browser-in-management-studio-and-cube-designer-has-been-removed"></a>Visualizzatore cubi in Management Studio e Progettazione cubi sono stati rimossi  
 Il controllo Visualizzatori cubi, che consente di trascinare campi sulla struttura di una Tabella pivot in Management Studio o in Progettazione cubi, è stato rimosso dal prodotto. Il controllo era un componente OWC (Office Web Control). OWC è stato deprecato da Office e non è più disponibile.  
  
### <a name="powerpivot-for-sharepoint"></a>PowerPivot per SharePoint  
  
#### <a name="higher-permission-requirements-for-using-a-powerpivot-workbook-as-an-external-data-source"></a>Requisiti di autorizzazione elevati per l'utilizzo di una cartella di lavoro di PowerPivot come origine dati esterna  
 In una cartella di lavoro di Excel è possibile eseguire il rendering di dati PowerPivot incorporati all'interno della stessa cartella di lavoro o contenuti in una cartella di lavoro esterna. Nella versione precedente i requisiti relativi alle autorizzazioni sono gli stessi sia per i dati PowerPivot incorporati sia per quelli esterni. Se erano state disposte autorizzazioni di **sola visualizzazione** su una cartella di lavoro di PowerPivot, era possibile l'accesso completo a tutti i dati PowerPivot nella cartella di lavoro per connessioni incorporate ed esterne.  
  
 In questa versione sono cambiati i requisiti relativi alle autorizzazioni per le cartelle di lavoro di Excel che eseguono il rendering di dati PowerPivot da un file esterno. In questa versione è necessario disporre di autorizzazioni di **Lettura** (più specificamente, dell'autorizzazione **Apertura elementi** ) per connettersi a una cartella di lavoro esterna di PowerPivot da un'applicazione client. Tramite le autorizzazioni aggiuntive si specifica che un utente ha diritto a visualizzare i dati di origine incorporati nella cartella di lavoro. La presenza di autorizzazioni aggiuntive è dovuta alla completa disponibilità dei dati del modello per l'applicazione client o la cartella di lavoro a essa collegata, con un conseguente miglioramento dell'allineamento tra i requisiti relativi alle autorizzazioni e il comportamento effettivo della connessione dati.  
  
 Per continuare a utilizzare una cartella di lavoro di PowerPivot come origine dati esterna, è necessario aumentare le autorizzazioni di SharePoint per utenti che si connettono a dati PowerPivot esterni. Fino a quando non si modificano le autorizzazioni, gli utenti riceveranno l'errore seguente se tentano di accedere alle cartelle di lavoro di PowerPivot in una connessione all'origine dati: "Servizio PowerPivot Web restituito un errore (accesso negato. Il documento richiesto non esiste o non è autorizzato ad aprire il file.)"  
  
> [!WARNING]  
>  Nei passaggi seguenti vengono fornite istruzioni per bloccare l'ereditarietà delle autorizzazioni al livello della libreria e per aumentare le autorizzazioni utente da **solo visualizzazione** a **lettura** per documenti specifici nella libreria. Prima di procedere, rivedere attentamente le autorizzazioni e i documenti esistenti e verificare che i passaggi siano appropriati per il sito in uso.  
>   
>  In alternativa, è possibile creare una cartella nella libreria, spostarvi tutti i documenti interessati e impostare autorizzazioni univoche sulla cartella stessa.  
  
> [!NOTE]  
>  Se le cartelle di lavoro vengono archiviate in Raccolta PowerPivot, tramite il blocco dell'ereditarietà delle autorizzazioni su una cartella di lavoro verrà interrotta la generazione dell'immagine di anteprima per quella cartella di lavoro, se configurata per l'aggiornamento dei dati. Per consentire simultaneamente l'accesso a cartelle di lavoro e immagini di anteprima nella raccolta, provare a concedere agli utenti specifici autorizzazioni di **lettura** al livello della libreria, per tutti i documenti in essa contenuti.  
  
 Per modificare le autorizzazioni è necessario essere proprietari del sito.  
  
 **Come aumentare le autorizzazioni a livello di autorizzazione per singole cartelle di lavoro di lettura**  
  
1.  Fare clic sulla freccia GIÙ per aprire il menu per un documento singolo.  
  
2.  Fare clic su **Gestione autorizzazioni**.  
  
3.  Per impostazione predefinita, le autorizzazioni vengono ereditate da una libreria. Per modificare le autorizzazioni di singole cartelle di lavoro in questa libreria, fare clic su **Interrompi ereditarietà autorizzazioni**.  
  
4.  Selezionare la casella di controllo in base ai nomi utente o di gruppi per i quali sono necessarie autorizzazioni aggiuntive sulle cartelle di lavoro di PowerPivot. Le autorizzazioni aggiuntive consentiranno agli utenti di collegarsi ai dati PowerPivot incorporati e di utilizzare tali dati come origine dati esterna in altri documenti.  
  
5.  Fare clic su **Modifica autorizzazioni utente**.  
  
6.  Scegliere le autorizzazioni di **lettura** , quindi fare clic su **OK**.  
  
#### <a name="powerpivot-gallery-new-rules-for-snapshot-generation-for-some-powerpivot-workbooks"></a>Raccolta PowerPivot: Nuove regole per la generazione di snapshot per alcune cartelle di lavoro di PowerPivot  
 Questa versione introduce nuovi requisiti per la generazione di immagini di snapshot in Raccolta PowerPivot, eliminando una potenziale fonte di diffusione di informazioni (vale a dire, mostrando uno snapshot di dati da un'origine dati per la quale non si dispone dell'autorizzazione di visualizzazione). Tali requisiti si applicano solo a cartelle di lavoro di PowerPivot che vengono connesse a origini dati esterne ogni volta che si visualizza la cartella di lavoro. Se si utilizzano solo cartelle di lavoro in cui vengono visualizzati dati PowerPivot incorporati, non sarà visibile alcuna modifica nella modalità di generazione di snapshot in Raccolta PowerPivot.  
  
 Per una cartella di lavoro in cui i dati vengono aggiornati ad ogni apertura, i nuovi requisiti per la generazione di snapshot saranno come indicato di seguito:  
  
-   È necessario che le cartelle di lavoro di PowerPivot utilizzate come origini dati esterne da altre cartelle di lavoro o report siano collocate nella stessa libreria delle cartelle di lavoro in cui vengono utilizzati i dati. Ad esempio, se si dispone di una cartella di lavoro sales-data.xlsx, tramite cui vengono forniti dati a una cartella di lavoro sales-report.xlsx, è necessario che entrambe siano collocate nella raccolta per consentire alle immagini snapshot di essere visualizzate.  
  
-   Per cartelle di lavoro utilizzate insieme, è necessario che le autorizzazioni siano ereditate da un elemento padre comune (ovvero, la Raccolta PowerPivot). Nell'esempio precedente, per entrambe le cartelle di lavoro sales-data.xlsx e sales-report.xlsx le autorizzazioni devono essere ereditate da Raccolta PowerPivot.  
  
 Se per una cartella di lavoro è impossibile soddisfare uno qualsiasi dei criteri suddetti, verrà visualizzata l'icona bloccata seguente anziché l'immagine di anteprima prevista:  
  
 ![GMNI_PowerPivotGalleryIcon_Locked](media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")  
  
#### <a name="new-default-setting-for-load-balancing-requests-changed-from-round-robin-to-health-based"></a>Nuova impostazione predefinita per richieste di bilanciamento del carico modificate da round robin a basato sull'integrità  
 In un'applicazione del servizio PowerPivot sono disponibili impostazioni predefinite tramite cui si determina come le richieste per i dati PowerPivot vengano distribuite attraverso più server PowerPivot per SharePoint in una farm. Nella versione precedente, l'impostazione predefinita era **Round robin**, in cui le richieste erano distribuite in sequenza fra i server disponibili. In questa versione, l'impostazione predefinita è **Basato sull'integrità**. Nell'applicazione del servizio PowerPivot vengono utilizzate statistiche di integrità del server, ad esempio memoria disponibile o CPU, per determinare quale istanza del server otterrà la richiesta xt.  
  
 Se il server è stato aggiornato dalla versione precedente, nell'applicazione del servizio PowerPivot viene mantenuta l'impostazione predefinita precedente (**Round robin**). Per utilizzare l'impostazione del metodo di allocazione **Basato sull'integrità** , è necessario modificare le impostazioni di configurazione. Per altre informazioni, vedere [creare e configurare un'applicazione di servizio PowerPivot in Amministrazione centrale](power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità con le versioni precedenti](../../2014/getting-started/backward-compatibility.md)   
 [Modifiche di rilievo per Analysis Services Features in SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
  
