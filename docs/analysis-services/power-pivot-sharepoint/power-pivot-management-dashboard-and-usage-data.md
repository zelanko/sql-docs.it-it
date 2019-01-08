---
title: Power Pivot Management Dashboard and Usage Data | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7158c0c441c11f87c4cc4989ca66061318a60df4
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419702"
---
# <a name="power-pivot-management-dashboard-and-usage-data"></a>Dati di utilizzo e dashboard di gestione PowerPivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] è una raccolta di report e Web part predefiniti in Amministrazione centrale SharePoint che consente di amministrare una distribuzione di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per SharePoint di SQL Server. Nel dashboard di gestione sono disponibili informazioni relative all'integrità del server, all'attività della cartella di lavoro e all'aggiornamento dati. I dati utilizzati nel dashboard provengono dalla raccolta dati di utilizzo di SharePoint.  
  
  
##  <a name="prereq"></a> Prerequisiti  
 Per aprire il dashboard di gestione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per un'applicazione del servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] gestita, è necessario essere un amministratore del servizio.  
  
##  <a name="items"></a> Panoramica delle sezioni del dashboard  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] sono contenuti Web part e report incorporati che consentono di eseguire il drill-down in categorie di informazioni specifiche. Nell'elenco seguente sono descritte le singole parti del dashboard:  
  
|Dashboard|Descrizione|  
|---------------|-----------------|  
|Infrastruttura: integrità del server|Vengono mostrate le tendenze nel tempo relative all'utilizzo della CPU, al consumo di memoria e ai tempi di risposta delle query in modo che sia possibile valutare se le risorse di sistema vengono impegnate al massimo o rimangono sottoutilizzate.|  
|Azioni|Sono contenuti i collegamenti ad altre pagine in Amministrazione centrale inclusi l'applicazione di servizio corrente, un elenco di applicazioni di servizio e la registrazione utilizzo.|  
|Attività cartella di lavoro: grafico|Viene segnalata la frequenza di accesso ai dati. È possibile acquisire la frequenza delle connessioni alle origini dati [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] su base giornaliera o settimanale.|  
|Attività cartella di lavoro: elenchi|Viene segnalata la frequenza di accesso ai dati. È possibile acquisire la frequenza delle connessioni alle origini dati [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] su base giornaliera o settimanale.|  
|Aggiornamento dati: attività recente|Viene segnalato lo stato dei processi di aggiornamento dei dati, inclusi quelli non eseguiti correttamente. In questo report è disponibile una vista dettagliata delle operazioni di aggiornamento dei dati a livello di applicazione. Gli amministratori possono individuare immediatamente il numero di processi di aggiornamento dei dati definiti per l'intera applicazione del servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .|  
|Aggiornamento dati: errori recenti|Vengono elencate le cartelle di lavoro di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per le quali non è stato completato correttamente l'aggiornamento dati.|  
|Report|Sono inclusi i collegamenti ai report che è possibile aprire in Excel.|  
  
##  <a name="open"></a> Aprire il dashboard di gestione PowerPivot  
 Il dashboard mostra le informazioni relative a un'applicazione del servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per volta. È possibile aprire il dashboard di gestione da due percorsi diversi.  
  
### <a name="open-the-dashboard-from-general-application-settings"></a>Aprire il dashboard da Impostazioni generali applicazione  
  
1.  Nel gruppo **Impostazioni generali applicazione** di Amministrazione centrale fare clic su **Dashboard di gestione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]**.  
  
2.  Nella pagina principale selezionare l'applicazione del servizio PowerPivot di cui visualizzare i dati delle operazioni.  
  
### <a name="open-the-dashboard-from-a-power-pivot-service-application"></a>Aprire il dashboard da un'applicazione del servizio PowerPivot  
  
1.  In **Gestione applicazioni**di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione del servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Nel dashboard di gestione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] vengono visualizzati i dati operativi relativi all'applicazione del servizio corrente.  
  
### <a name="change-the-current-service-application"></a>Modificare l'applicazione di servizio corrente.  
 Per modificare l'applicazione del servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] corrente nel dashboard di gestione:  
  
1.  Nella parte superiore del dashboard di gestione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] si noti il nome dell'applicazione del servizio corrente, ad esempio **Default [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Service Application** (Applicazione del servizio predefinita).  
  
2.  Nel dashboard **Azioni** fare clic su **Elenca applicazioni di servizio**.  
  
3.  Fare clic sul nome dell'applicazione del servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] di cui visualizzare i report del dashboard di gestione.  
  
##  <a name="sourcedata"></a> Dati di origine nei dashboard  
 Nei dashboard, nei report e nelle Web part vengono visualizzati dati provenienti da un modello di dati interno tramite cui è possibile estrarre i dati dal sistema e dai database dell'applicazione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] . Il modello di dati interno è incorporato in una cartella di lavoro di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] ospitata nel sito Amministrazione centrale. La struttura del modello di dati è fissa. Anche se è possibile utilizzare la cartella di lavoro di PowerPivot come origine dati per creare nuovi report, è necessario non modificare la struttura in maniera da causare l'interruzione dei report predefiniti in cui viene utilizzata.  
  
 Per ulteriori informazioni sulla modalità di raccolta dei dati, vedere quanto riportato di seguito:  
  
-   [Raccolta dati di utilizzo di PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)  
  
-   [Configurare la raccolta dati di utilizzo per PowerPivot per SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
 Al fine di acquisire dati sul sistema del server PowerPivot, verificare che siano abilitate la messaggistica degli eventi, la cronologia dell'aggiornamento dati e altre cronologie relative all'utilizzo per ogni applicazione del servizio PowerPivot. I dati di utilizzo e del server raccolti durante il normale funzionamento del server costituiscono i dati di origine che finiscono nel modello di dati interno. **Nota:** Se si disabilita la cronologia degli eventi o dell'utilizzo, i report composti risulteranno incompleti o errati.  
  
##  <a name="edit"></a> Modificare il dashboard PowerPivot  
 Gli utenti esperti nello sviluppo e nella personalizzazione di dashboard potranno modificare il dashboard in modo da includere nuove web part. È possibile modificare anche le proprietà delle web part incluse nel dashboard.  
  
##  <a name="reports"></a> Creare report personalizzati per il dashboard di gestione PowerPivot  
 Ai fini dei report, i dati di utilizzo e la cronologia di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] vengono mantenuti in una cartella di lavoro interna di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] creata e configurata con il dashboard. Se i report predefiniti non forniscono le informazioni necessarie, è possibile creare report personalizzati in Excel in base alla cartella di lavoro. Sia la cartella di lavoro sia eventuali report personalizzati creati dall'utente verranno conservati se si aggiornano o si disinstallano i file della soluzione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] in un secondo momento. La cartella di lavoro e i report sono archiviati nella raccolta di gestione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] all'interno del sito Amministrazione centrale. Questa raccolta non è visibile per impostazione predefinita, ma può essere visualizzata utilizzando l'azione Visualizza tutto il contenuto del sito in Azioni sito.  
  
 Per iniziare a usare la creazione di report personalizzati, il dashboard di gestione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] fornisce un file Office Data Connection (.odc) per la connessione alla cartella di lavoro di origine. Ad esempio, è possibile utilizzare il file con estensione odc in Excel per la creazione di report aggiuntivi.  
  
> [!NOTE]  
>  Modificare il file per evitare l'errore seguente quando si tenta di usare il file con estensione odc in Excel: "Inizializzazione dell'origine dati non riuscita". Nel file con estensione odc generato automaticamente è incluso un parametro che non è supportato dal provider OLE DB MSOLAP. Nelle istruzioni seguenti viene fornita la soluzione alternativa per la rimozione dei parametri.  
  
 Per compilare report basati sulla cartella di lavoro di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] in Amministrazione centrale, è necessario essere l'amministratore di una farm o di un servizio.  
  
1.  Aprire il dashboard di gestione [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .  
  
2.  Scorrere alla sezione **Report** nella parte inferiore della pagina.  
  
3.  Fare clic su **Dati di gestione di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]**.  
  
4.  Salvare il file con estensione odc in una cartella locale.  
  
5.  Aprire il file con estensione odc in un editor di testo.  
  
6.  Nel  **\<odc: ConnectionString >** elemento, scorrere fino alla fine della riga e rimuovere **dati incorporati = False**, quindi rimuovere **Edit Mode = 0**. Se l'ultimo carattere nella stringa è un punto e virgola, rimuoverlo in questo passaggio.  
  
7.  Salvare il file. I passaggi rimanenti dipendono dalla versione di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] ed Excel in uso.  
  
8.  1.  Avviare Excel 2013  
  
    2.  Nella barra multifunzione di **[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]** fare clic su **Gestisci**.  
  
    3.  Fare clic su **Recupera dati esterni** , quindi scegliere **Connessioni esistenti**.  
  
    4.  Fare clic sul file ODC se visualizzato. In caso contrario, fare clic su **Cerca** e, successivamente, nel percorso file specificare il file con estensione odc.  
  
    5.  Fare clic su **Apri**.  
  
    6.  Fare clic su **Test connessione** per verificare che la connessione sia stata stabilita correttamente.  
  
    7.  Digitare un nome per la connessione, quindi fare clic su **Avanti**.  
  
    8.  In specificare una Query MDX fare clic su **Design** per aprire la finestra Progettazione query MDX per assemblare i dati che si desidera utilizzare **se viene visualizzato il messaggio di errore** "il nome della proprietà modalità di modifica non è formattato correttamente.", verificare si modifica il. File con estensione ODC.  
  
    9. Scegliere **OK** , quindi **Fine**.  
  
    10. Creare i report della tabella pivot o del grafico pivot per visualizzare i dati in Excel.  
  
9. 1.  Avviare Excel 2010.  
  
    2.  Nella barra multifunzione di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] fare clic su **Avvia finestra [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]** (Avvia finestra PowerPivot).  
  
    3.  Sulla barra multifunzione Progettazione della finestra [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] fare clic su **Connessioni esistenti**.  
  
    4.  Fare clic su **Cerca**.  
  
    5.  Nel percorso file specificare il file con estensione odc.  
  
    6.  Fare clic su **Apri**. Tramite la stringa di connessione alla cartella di lavoro di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] che contiene dati di utilizzo viene avviata l'importazione guidata tabella.  
  
    7.  Per verificare che sia stato eseguito correttamente l'accesso, fare clic su **Test connessione** .  
  
    8.  Immettere un nome descrittivo per la connessione, quindi fare clic su **Avanti**.  
  
    9. In Specifica di una query MDX fare clic su **Progettazione** per aprire Progettazione query MDX al fine di assemblare i dati che si desidera utilizzare, quindi creare i report della tabella pivot o del grafico pivot per visualizzare i dati in Excel.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dati PowerPivot con SharePoint 2010](http://msdn.microsoft.com/01b54e6f-66e5-485c-acaa-3f9aa53119c9)   
 [Configurare la raccolta dati di utilizzo per PowerPivot per SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
