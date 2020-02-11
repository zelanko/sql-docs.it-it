---
title: Aggiornamento dati PowerPivot con SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 34f03407-2ec4-4554-b16b-bc9a6c161815
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4076e27a800f9c9653e8a191c1fd53467cba9f75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071228"
---
# <a name="powerpivot-data-refresh-with-sharepoint-2013"></a>Aggiornamento dati PowerPivot con SharePoint 2013
  La progettazione per l'aggiornamento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] dei modelli di dati in SharePoint 2013 utilizza Excel Services come componente principale per caricare e aggiornare i modelli di dati in un' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza di in esecuzione in modalità SharePoint. Il server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene eseguito esternamente alla farm di SharePoint.  
  
 L'architettura di aggiornamento dati utilizzata in precedenza era basata esclusivamente sul servizio di sistema PowerPivot per il caricamento e l'aggiornamento dei modelli di dati in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint. L'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] veniva eseguita localmente nel server applicazioni PowerPivot. Con la nuova architettura, inoltre, è stato introdotto un nuovo metodo per gestire le informazioni di pianificazione, ad esempio i metadati dell'elemento della cartella di lavoro nella raccolta documenti. L'architettura in SharePoint 2013 Excel Services supporta sia l' **aggiornamento dati interattivo** che l' **aggiornamento dati pianificato**.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013  
  
 **In questo argomento**  
  
-   [Aggiornamento dati interattivo](#bkmk_interactive_refresh)  
  
-   [Autenticazione di Windows con connessioni dati della cartella di lavoro e aggiornamento dati interattivo](#bkmk_windows_auth_interactive_data_refresh)  
  
-   [Aggiornamento dati pianificato](#bkmk_scheduled_refresh)  
  
-   [Architettura dell'aggiornamento dati pianificato in SharePoint 2013](#bkmk_refresh_architecture)  
  
-   [Considerazioni aggiuntive sull'autenticazione](#datarefresh_additional_authentication)  
  
-   [Altre informazioni](#bkmk_moreinformation)  
  
## <a name="background"></a>Background  
 SharePoint Server 2013 Excel Services gestisce l'aggiornamento dei dati per le cartelle di lavoro di Excel 2013 e attiva l' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elaborazione del modello di dati in un server in esecuzione in modalità SharePoint. In caso di cartelle di lavoro di Excel 2010, tramite Excel Services è inoltre possibile gestire il caricamento e il salvataggio delle cartelle di lavoro e dei modelli di dati. Tuttavia, Excel Services si basa sul servizio di sistema PowerPivot per inviare i comandi di elaborazione al modello di dati. Nella tabella seguente sono riepilogati i componenti mediante i quali vengono inviati i comandi di elaborazione per l'aggiornamento dati in base alla versione della cartella di lavoro. L'ambiente considerato è una farm di SharePoint 2013 configurata per usare un server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Analysis Services in modalità SharePoint.  
  
||||  
|-|-|-|  
||Cartelle di lavoro di Excel 2013|Cartelle di lavoro di Excel 2010|  
|Attivazione dell'aggiornamento dati|**Interattivo:** Utente autenticato<br /><br /> **Pianificato:** Servizio di sistema PowerPivot|servizio di sistema PowerPivot|  
|Caricamento della cartella di lavoro da database di contenuto|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|Caricamento del modello di dati in un'istanza di Analysis Services|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|Invio dei comandi di elaborazione all'istanza di Analysis Services|SharePoint 2013 Excel Services|servizio di sistema PowerPivot|  
|Aggiornamento dei dati della cartella di lavoro|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|Salvataggio della cartella di lavoro e del modello di dati nel database di contenuto|**Interattivo:** N/A<br /><br /> **Pianificato:** SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
  
 Nella tabella seguente sono riepilogate le funzionalità di aggiornamento supportate in una farm di SharePoint 2013 configurata per usare un server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Analysis Services in modalità SharePoint:  
  
|Cartella di lavoro creata in|aggiornamento dati pianificato|Aggiornamento interattivo|  
|-------------------------|----------------------------|-------------------------|  
|SQL Server 2008 R2 PowerPivot per Excel|Non supportato. Aggiornare la cartella di lavoro **(\*)**|Non supportato. Aggiornare la cartella di lavoro **(\*)**|  
|2012 PowerPivot per Excel|Supportato|Non supportato. Aggiornare la cartella di lavoro **(\*)**|  
|Excel 2013|Supportato|Supportato|  
  
 **(\*)** Per altre informazioni sugli aggiornamenti delle cartelle di lavoro, vedere [aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_interactive_refresh"></a>Aggiornamento dati interattivo  
 L'aggiornamento dati interattivo o manuale in SharePoint Server Excel Services 2013 consente di aggiornare i modelli di dati con dati dell'origine dati originale. L'aggiornamento dati interattivo è disponibile dopo la configurazione di un'applicazione Excel Services registrando un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità SharePoint. Per altre informazioni, vedere [Gestire le impostazioni del modello di dati di Excel Services (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx).  
  
> [!NOTE]  
>  L'aggiornamento dati interattivo è disponibile solo per cartelle di lavoro create in Excel 2013. Se si tenta di aggiornare una cartella di lavoro di Excel 2010, in Excel Services viene visualizzato un messaggio di errore simile a "operazione PowerPivot non riuscita: la cartella di lavoro è stata creata in una versione precedente di Excel e PowerPivot non può essere aggiornato finché il file non viene aggiornato". Per altre informazioni sull'aggiornamento delle cartelle di lavoro, vedere [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
 **Punto chiave di interesse dell'aggiornamento interattivo:**  
  
-   L'aggiornamento dati interattivo viene eseguito solo per i dati nella sessione utente corrente. I dati non vengono salvati di nuovo automaticamente nell'elemento della cartella di lavoro nel database del contenuto di SharePoint.  
  
-   **Credenziali:** L'aggiornamento dati interattivo può utilizzare l'identità dell'utente attualmente connesso come credenziali o credenziali archiviate per la connessione all'origine dati. Le credenziali utilizzate dipendono dalle impostazioni di autenticazione di Excel Services definite per la connessione della cartella di lavoro all'origine dati esterna.  
  
-   **Cartelle di lavoro supportate:**  Cartelle di lavoro create in Excel 2013.  
  
 **Per aggiornare i dati:**  
  
-   Vedere i passaggi nell'illustrazione riportata di seguito.  
  
1.  In una raccolta documenti di SharePoint aprire la cartella di lavoro di PowerPivot nel browser.  
  
2.  Nella finestra del browser fare clic sul menu **Dati** , quindi scegliere **Aggiorna connessione selezionata** o **Aggiorna tutte le connessioni**.  
  
3.  Tramite Excel Services il database PowerPivot viene caricato, elaborato e successivamente sottoposto a query per aggiornare la cache della cartella di lavoro di Excel.  
  
4.  **Nota:** La cartella di lavoro aggiornata non viene salvata di nuovo automaticamente nella raccolta documenti.  
  
 ![aggiornamento dati interattivo](../media/as-interactive-datarefresh-sharepoint2013.gif "aggiornamento dati interattivo")  
  
###  <a name="bkmk_windows_auth_interactive_data_refresh"></a>Autenticazione di Windows con connessioni dati della cartella di lavoro e aggiornamento dati interattivo  
 Tramite Excel Services viene inviato al server Analysis Services un comando di elaborazione per fare in modo che il server rappresenti un account utente. Per ottenere diritti di sistema sufficienti per eseguire il processo di delega di rappresentazione utente, è necessario il privilegio **Agire come parte del sistema operativo** nel server locale per l'account del servizio Analysis Services. Tramite il server Analysis Services deve inoltre essere possibile delegare le credenziali dell'utente alle origini dati. Il risultato della query viene inviato a Excel Services.  
  
 Esperienza utente tipica: quando un cliente seleziona "Aggiorna tutte le connessioni" in una cartella di lavoro di Excel 2013 che contiene un modello PowerPivot, viene visualizzato un messaggio di errore simile al seguente:  
  
-   **Aggiornamento dati esterno non riuscito:** Si è verificato un errore durante l'utilizzo del modello di dati nella cartella di lavoro. Riprovare. Non è possibile aggiornare i dati per una o più connessioni dati nella cartella di lavoro.  
  
 A seconda del provider di dati utilizzato, è possibile che vengano visualizzati messaggi simili ai seguenti nel log ULS.  
  
 **Con la SQL Native Client:**  
  
-   Non è possibile creare una connessione esterna o eseguire una query. Messaggio provider - L'oggetto out-of-line "DataSource", che fa riferimento all'ID "20102481-39c8-4d21-bf63-68f583ad22bb", è stato specificato ma non è stato utilizzato. Errore OLE DB o ODBC:  Errore OLE DB oppure ODBC - Si è verificato un errore specifico dell'istanza o relativo alla rete durante il tentativo di stabilire una connessione a SQL Server. Server non trovato o non accessibile. Verificare che il nome dell'istanza sia corretto e che il server sia configurato in modo da consentire connessioni remote. Per ulteriori informazioni, vedere la documentazione online di SQL Server; 08001; Provider SSL - Il pacchetto di sicurezza richiesto non esiste; 08001; Il client non è in grado di effettuare la connessione; 08001; Crittografia non supportata dal client; 08001.  , ConnectionName: ThisWorkbookDataModel, cartella di lavoro: book1.xlsx.  
  
 **Con il provider di Microsoft OLE DB per SQL Server:**  
  
-   Non è possibile creare una connessione esterna o eseguire una query. Messaggio provider: l'oggetto out-of-line "DataSource", che fa riferimento all'ID "6e711bfa-b62f-4879-a177-c5dd61d9c242", è stato specificato ma non è stato utilizzato. Errore OLE DB o ODBC, , ConnectionName: ThisWorkbookDataModel, cartella di lavoro: OLEDB Provider.xlsx.  
  
 **Con il .NET Framework provider di dati per SQL Server:**  
  
-   Non è possibile creare una connessione esterna o eseguire una query. Messaggio provider - L'oggetto out-of-line "DataSource", che fa riferimento all'ID "f5fb916c-3eac-4d07-a542-531524c0d44a", è stato specificato ma non è stato utilizzato.  Errori nel motore relazionale di alto livello. Durante l'utilizzo dell'interfaccia gestita IDbConnection si è verificata l'eccezione seguente: impossibile caricare il file o l'assembly "System.Transactions, Version=4.0.0.0, Culture=neutral PublicKeyToken=b77a5c561934e089" o una delle relative dipendenze. Non è stato fornito il livello richiesto di rappresentazione di client oppure il livello di rappresentazione fornito non è valido. Eccezione da HRESULT: 0x80070542.  , ConnectionName: ThisWorkbookDataModel, cartella di lavoro: NETProvider.xlsx.  
  
 **Riepilogo dei passaggi di configurazione** Per configurare **Act come parte del privilegio del sistema operativo** nel server locale:  
  
1.  In Analysis Services server in esecuzione in modalità SharePoint aggiungere l'account del servizio Analysis Services al privilegio "**Agisci come parte del sistema operativo**":  
  
    1.  Eseguire "`secpol.msc`"  
  
    2.  Fare clic su **Criteri di sicurezza locali**, selezionare **Criteri locali**, quindi scegliere **Assegnazione diritti utente**.  
  
    3.  Aggiungere l'account del servizio.  
  
2.  Riavviare Excel Services e il server Analysis Services.  
  
3.  La delega dall'account del servizio Excel Services o da Attestazioni del servizio token Windows (C2WTS) all'istanza di Analysis Services non è richiesta. Pertanto, non è necessaria alcuna configurazione per KCD da Excel Services o C2WTS al servizio Analysis Services per PowerPivot. Se l'origine dati back-end si trova nello stesso server di un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , la delega vincolata Kerberos non è necessaria. Tuttavia, l'account del servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve disporre del privilegio Agisci come parte del sistema operativo.  
  
 ![as_interactive_data_refresh2012SP1_windowsauth](../media/as-interactive-data-refresh2012sp1-windowsauth.gif "as_interactive_data_refresh2012SP1_windowsauth")  
  
 Per altre informazioni, vedere [agire come parte del sistema operativo](https://technet.microsoft.com/library/cc784323\(WS.10\).aspx).  
  
##  <a name="bkmk_scheduled_refresh"></a>Aggiornamento dati pianificato  
 **Punti chiave di interesse dell'aggiornamento dati pianificato:**  
  
-   È richiesta la distribuzione del componente aggiuntivo PowerPivot per SharePoint. Per ulteriori informazioni, vedere [installare o disinstallare il componente aggiuntivo PowerPivot per SharePoint &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
-   Un utente configura una pianificazione dell'aggiornamento per una cartella di lavoro. All'ora pianificata, tramite il servizio di sistema PowerPivot viene inviata una richiesta a Excel Services per:  
  
    -   Caricare ed elaborare il database PowerPivot.  
  
    -   Aggiornare la cartella di lavoro.  
  
    -   Salvare di nuovo la cartella di lavoro nel database di contenuto.  
  
-   **Credenziali:** Usa le credenziali archiviate. Non usare l'identità dell'utente corrente.  
  
-   **Cartelle di lavoro supportate:** Cartelle di lavoro create utilizzando [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] il componente aggiuntivo PowerPivot per Excel 2010 o utilizzando Excel 2013. Le cartelle di lavoro create in Excel 2010 con il componente aggiuntivo [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] PowerPivot non sono supportate. Aggiornare la cartella di lavoro almeno al formato [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot. Per altre informazioni sugli aggiornamenti delle cartelle di lavoro, vedere [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
 Per visualizzare la pagina **Gestisci aggiornamento dati** :  
  
-   Vedere i passaggi nell'illustrazione riportata di seguito.  
  
1.  In una raccolta documenti di SharePoint fare clic su **Menu Apri** (**...**) per una cartella di lavoro di PowerPivot.  
  
2.  Fare clic sul secondo **Menu Apri** , quindi scegliere **Gestisci aggiornamento dati PowerPivot**.  
  
3.  Nella pagina **Gestisci aggiornamento dati** fare clic su **Abilita** , quindi configurare la pianificazione dell'aggiornamento.  
  
4.  All'ora specificata, tramite il servizio di sistema PowerPivot viene inviata una richiesta a Excel Services per:  
  
    -   Caricare ed elaborare il modello di dati PowerPivot.  
  
    -   Aggiornare la cartella di lavoro.  
  
    -   Salvare di nuovo la cartella di lavoro nel database di contenuto.  
  
 ![menu di scelta rapida Gestisci aggiornamento dati](../media/as-manage-datarefresh-sharepoint2013.gif "menu di scelta rapida Gestisci aggiornamento dati")  
  
> [!TIP]  
>  Per informazioni sull'aggiornamento delle cartelle di lavoro da SharePoint Online, vedere [aggiornamento delle cartelle di lavoro di Excel con modelli PowerPivot incorporati da SharePoint Online (white paper)](https://technet.microsoft.com/library/jj992650.aspx) (https://technet.microsoft.com/library/jj992650.aspx).  
  
##  <a name="bkmk_refresh_architecture"></a>Architettura dell'aggiornamento dati pianificato in SharePoint 2013  
 Nell'illustrazione seguente è riepilogata l'architettura dell'aggiornamento dati in SharePoint 2013 e SQL Server 2012 SP1.  
  
 ![architettura dell'aggiornamento dati di SQL Server 2012 SP1](../media/as-scheduled-data-refresh2012sp1-architecture.gif "architettura dell'aggiornamento dati di SQL Server 2012 SP1")  
  
||Descrizione||  
|-|-----------------|-|  
|**(1)**|Motore Analysis Services|Server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità SharePoint. Il server viene eseguito esternamente alla farm di SharePoint.|  
|**2**|Interfaccia utente|L'interfaccia utente è costituita da due pagine: una per definire la pianificazione, l'altra per visualizzare la cronologia aggiornamento. L'accesso ai database dell'applicazione del servizio PowerPivot non viene effettuato direttamente dalle pagine ma tramite il servizio di sistema PowerPivot.|  
|**(3)**|servizio di sistema PowerPivot|Il servizio viene installato durante la distribuzione del componente aggiuntivo PowerPivot per SharePoint. Viene utilizzato per le operazioni seguenti:<br /><br /> Hosting del motore di pianificazione dell'aggiornamento mediante il quale vengono chiamate le API Excel Services per l'aggiornamento dati delle cartelle di lavoro di Excel 2013. In caso di cartelle di lavoro di Excel 2010, l'elaborazione del modello di dati viene effettuata direttamente dal servizio mediante il quale si continua però a rispondere in Excel Services per il caricamento del modello di dati e l'aggiornamento della cartella di lavoro.<br /><br /> Fornitura di metodi per componenti come le pagine dell'interfaccia utente per la comunicazione con il servizio di sistema.<br /><br /> Gestione delle richieste per l'accesso esterno a cartelle di lavoro come origine dati, ricevute tramite il servizio Web PowerPivot.<br /><br /> Gestione delle richieste di aggiornamento dati pianificato per i processi timer e le pagine di configurazione. Tramite il servizio vengono gestite le richieste per leggere i dati in ingresso e in uscita dal database dell'applicazione di servizio e per attivare l'aggiornamento dati con Excel Services.<br /><br /> Utilizzo dell'elaborazione e processo timer correlato.|  
|**(4)**|Servizi di calcolo Excel|Utilizzati per il caricamento dei modelli di dati.|  
|**5**|Servizio di archiviazione sicura|Se le impostazioni di autenticazione nella cartella di lavoro sono configurate per **l'utilizzo dell'account utente autenticato** o **Nessuna**, per l'aggiornamento dati vengono utilizzate le credenziali archiviate nell'ID dell'applicazione di destinazione di archiviazione sicura. Per altre informazioni, vedere la sezione [Considerazioni aggiuntive sull'autenticazione](#datarefresh_additional_authentication) contenuta in questo argomento.|  
|**6**|Processo timer di aggiornamento dati PowerPivot|Imposta la connessione del servizio di sistema PowerPivot con Excel Services per l'aggiornamento dei modelli di dati.|  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono necessari librerie client e provider di dati appropriati affinché sia possibile accedere alle origini dati tramite il server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint.  
  
> [!NOTE]  
>  Dal momento che tramite il servizio di sistema PowerPivot non viene più eseguito il caricamento o il salvataggio dei modelli PowerPivot, a una farm di SharePoint 2013 non viene applicata la maggior parte delle impostazioni per memorizzare i modelli nella cache di un server applicazioni.  
  
## <a name="data-refresh-log-data"></a>Dati del log di aggiornamento dati  
 **Dati di utilizzo:** È possibile visualizzare i dati di utilizzo dell'aggiornamento dati nel dashboard di gestione PowerPivot. Per visualizzare i dati di utilizzo:  
  
1.  Nel gruppo **Impostazioni generali applicazione** di Amministrazione centrale SharePoint fare clic su **Dashboard di gestione PowerPivot** .  
  
2.  Nella parte inferiore del dashboard, vedere **aggiornamento dati-attività recente** e **aggiornamento dati-errori recenti**.  
  
3.  Per altre informazioni sui dati di utilizzo e sulla relativa abilitazione, vedere [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
 **Dati del log di diagnostica:** È possibile visualizzare i dati del log di diagnostica di SharePoint correlati all'aggiornamento dati. Innanzitutto, verificare la configurazione della registrazione dei dati di diagnostica per il **servizio PowerPivot** nella pagina **Monitoraggio** di Amministrazione centrale SharePoint. Potrebbe essere necessario aumentare il livello di registrazione per l'evento meno critico da registrare. Impostare, ad esempio, temporaneamente il valore su **Dettagliato** , quindi eseguire di nuovo le operazioni di aggiornamento dati.  
  
 Tra le voci di log sono incluse:  
  
-   L' **area** del **servizio PowerPivot**.  
  
-   La categoria **Aggiornamento dati**.  
  
 Controllare **Configura registrazione diagnostica**. Per ulteriori informazioni, vedere [configurare e visualizzare i file di log di SharePoint e la registrazione diagnostica &#40;PowerPivot per SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
##  <a name="datarefresh_additional_authentication"></a>Considerazioni aggiuntive sull'autenticazione  
 Tramite le impostazioni della finestra di dialogo **Impostazioni autenticazione Excel Services** in Excel 2013 è possibile stabilire l'identità Windows utilizzata da Excel Services e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per l'aggiornamento dati.  
  
-   **Usa l'account utente autenticato**: Excel Services esegue l'aggiornamento dei dati con l'identità dell'utente attualmente connesso.  
  
-   **Usa account archiviato**: presuppone un ID applicazione di SharePoint servizio di archiviazione sicura, che viene usato da Excel Services per recuperare il nome utente e la password per autenticare l'autenticazione dell'aggiornamento dati.  
  
-   **None**: viene usato l' **account del servizio automatico** di Excel Services. L'account del servizio è associato a un proxy dell'archiviazione sicura. Configurare le impostazioni nella sezione **Dati esterni** della pagina **Impostazioni applicazioni Excel Services** .  
  
 Per aprire la finestra di dialogo delle impostazioni di autenticazione:  
  
1.  Fare clic sulla scheda **Dati** in Excel 2013.  
  
2.  Fare clic su **Connessioni** nella barra multifunzione.  
  
3.  Nella finestra di dialogo **Connessioni cartella di lavoro**selezionare la connessione e fare clic su **Proprietà**.  
  
4.  Nella finestra di dialogo **Proprietà connessione** fare clic su **definizione**, quindi fare clic sul pulsante **impostazioni di autenticazione** .  
  
 ![Impostazioni autenticazione Excel Services](../media/as-authentication-settings-4-ecs-in-excel2013.gif "Impostazioni autenticazione Excel Services")  
  
 Per altre informazioni sull'autenticazione dell'aggiornamento dati e sull'utilizzo di credenziali, vedere il post del blog sull' [aggiornamento dei dati PowerPivot in SharePoint 2013](https://blogs.msdn.com/b/analysisservices/archive/2012/12/21/refreshing-powerpivot-data-in-sharepoint-2013.aspx).  
  
##  <a name="bkmk_moreinformation"></a> Ulteriori informazioni  
 [Risoluzione dei problemi relativi all'aggiornamento dati PowerPivot](https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 [Excel Services in SharePoint 2013](https://www.enjoysharepoint.com/configure-excel-service-application-in-sharepoint-2013/). 
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)   
 [PowerPivot for SharePoint 2013 Installation](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
