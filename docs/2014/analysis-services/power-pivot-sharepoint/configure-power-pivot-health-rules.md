---
title: 'Configurare regole di integrità di PowerPivot: | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a01e63e6-97dc-43e5-ad12-ae6580afc606
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 180be5fee054ff1afff09191ee6a16707b712257
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071795"
---
# <a name="powerpivot-health-rules---configure"></a>Regole di integrità di PowerPivot: configurazione
  PowerPivot per SharePoint include regole di integrità SharePoint che consentono di monitorare e porre rimedio ai problemi di disponibilità e configurazione. Le regole di analisi dell'integrità che si applicano a PowerPivot per SharePoint vengono visualizzate nella pagina Rivedi definizioni regole.  
  
 Le regole di integrità consentono di rilevare in anticipo problemi relativi al server che potrebbero eventualmente comportare interruzioni del servizio. In PowerPivot per SharePoint sono disponibili diverse regole per l'identificazione e la risoluzione dei problemi prima che questi abbiano un impatto sugli utenti. È possibile personalizzare molte di queste regole per adattarle alle caratteristiche univoche della distribuzione in uso. Se si desidera ad esempio più tempo per risolvere avvisi relativi allo spazio su disco, è possibile aumentare la percentuale di spazio su disco disponibile dal 5% al 10% in modo da ricevere prima l'avviso.  
  
 Le regole che possono essere personalizzate sono quelle che consentono di segnalare l'utilizzo delle risorse o la disponibilità del server. La personalizzazione è utile in queste aree in quanto la capacità del sistema sottostante varia ampiamente tra topologie di distribuzione e server differenti. Non è invece disponibile alcuna personalizzazione per le regole che consentono l'identificazione di problemi riguardanti la sicurezza o la configurazione del server. Tali regole devono essere applicate in modo uniforme in tutte le installazioni.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **Nota:** Impostazioni delle regole di integrità vengono configurate separatamente per l'istanza di SQL Server Analysis Services e l'applicazione di servizio PowerPivot. Utilizzare le istruzioni riportate in questo argomento per configurare le regole di integrità per ogni servizio. Per una distribuzione di SharePoint 2013, in [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] viene utilizzata solo l'applicazione di servizio. Pertanto con [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] vengono installati differenti set di regole di integrità per versioni diverse di SharePoint. Vedere la colonna "version" nell'argomento [riferimento delle regole di integrità &#40;PowerPivot per SharePoint&#41;](health-rules-reference-power-pivot-for-sharepoint.md), oppure è possibile eseguire il comando di Windows PowerShell seguente per visualizzare le regole installate.  
  
```  
Get-SPHealthAnalysisRule | select name, enabled, summary | where {$_.summary -like "*power*"}  | format-table -property * -autosize | out-default  
```  
  
 **Contenuto dell'argomento:**  
  
 [Visualizzare le regole di integrità PowerPivot](#bkmk_view)  
  
 [Configurare le regole di integrità utilizzate per valutare la stabilità del server (SQL Server Analysis Services)](#bkmk_HR_SSAS)  
  
 [Configurare le regole di integrità utilizzate per valutare la stabilità dell'applicazione (applicazione del servizio PowerPivot)](#bkmk_evaluate_application_stability)  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario essere un amministratore dell'applicazione di servizio per modificare le proprietà di configurazione dell'istanza di Analysis Services e dell'applicazione del servizio PowerPivot.  
  
##  <a name="bkmk_view"></a> Visualizzare le regole di integrità PowerPivot  
  
1.  In Amministrazione centrale SharePoint fare clic su **Monitoraggio**e nella sezione **Analizzatore dell'integrità** fare clic su **Controlla definizioni regole**.  
  
2.  Nella sezione Configurazione trovare le regole con il prefisso **PowerPivot:** . Tutte le regole di integrità correlate a PowerPivot presentano questo prefisso per facilitarne la distinzione dalle regole di SharePoint incorporate.  
  
 Queste regole verranno visualizzate nella pagina **Controlla problemi e soluzioni** in caso di problemi.  
  
 Se si sospetta un problema e si desidera controllare immediatamente, per rilevarne l'eventuale presenza è possibile eseguire manualmente una verifica della regola.  
  
 A tale scopo, fare clic sulla regola per aprirne la definizione, quindi fare clic su **Esegui ora** sulla barra multifunzione. Fare clic su **Chiudi** per tornare alla pagina **Controlla problemi e soluzioni** per visualizzare il report. Se tramite la regola viene rilevato un problema, un avviso o un errore sarà segnalato nella pagina. In alcuni casi, la visualizzazione dell'errore o dell'avviso può richiedere alcuni minuti.  
  
##  <a name="bkmk_HR_SSAS"></a> Configurare le regole di integrità utilizzate per valutare la stabilità del server (SQL Server Analysis Services)  
 Nell'istanza di Analysis Services sono incluse regole di integrità tramite cui vengono rilevati problemi a livello di sistema (CPU, memoria e spazio su disco utilizzato per la memorizzazione nella cache). Utilizzare le istruzioni seguenti per modificare le soglie che consentono l'attivazione di regole di integrità specifiche.  
  
1.  Nella sezione **Impostazioni sistema** di Amministrazione centrale SharePoint fare clic su **Gestisci servizi nel server**.  
  
2.  Nella parte superiore della pagina selezionare il server nella farm di SharePoint con un'istanza di Analysis Services (nell'illustrazione seguente il nome del server è AW-SRV033). Nell'elenco dei servizi verrà visualizzato**SQL Server Analysis Services** .  
  
     ![Screenshot di Gestisci pagina servizi nel Server](../media/ssas-centraladmin-servicesonserver.gif "Screenshot di Gestisci pagina servizi nel Server")  
  
3.  Scegliere **SQL Server Analysis Services**.  
  
4.  Nelle pagine delle proprietà del servizio, in Impostazioni regole di analisi dell'integrità modificare le impostazioni seguenti:  
  
     Allocazione di risorse di CPU insufficiente (l'impostazione predefinita è 80%)  
     Questa regola di analisi dell'integrità viene attivata se le risorse CPU utilizzate dal processo del server Analysis Services (msmdsrv.exe) rimangono su un valore uguale o superiore all'80% nell'arco di 4 ore (come specificato dall'impostazione Intervallo raccolta dati).  
  
     Questa impostazione di configurazione corrisponde alla definizione della regola seguente nella **Controlla problemi e soluzioni** pagina: **PowerPivot: Analysis Services non dispone di risorse di CPU sufficienti per eseguire le operazioni richieste.**  
  
     Risorse di CPU insufficienti nel sistema (l'impostazione predefinita è 90%)  
     Questa regola di analisi dell'integrità viene attivata se le risorse di CPU per il server rimangono su un valore uguale o superiore al 90% nell'arco di 4 ore (come specificato dall'impostazione Intervallo raccolta dati). L'utilizzo della CPU complessivo è misurato come parte dell'algoritmo di bilanciamento del carico basato sull'integrità che monitora l'utilizzo della CPU come misura dell'integrità del server.  
  
     Questa impostazione di configurazione corrisponde alla definizione della regola seguente nella **Controlla problemi e soluzioni** pagina: **PowerPivot: Utilizzo della CPU complessivo è troppo alto.**  
  
     Soglia di memoria insufficiente (l'impostazione predefinita è 5%)  
     Un'istanza di SQL Server Analysis Services in un server applicazioni SharePoint deve disporre sempre di una piccola quantità di memoria di riserva inutilizzata. Poiché il server è associato alla memoria per la maggior parte delle operazioni, funziona meglio se non viene eseguito fino al limite massimo. Il 5% di memoria inutilizzata viene calcolato come percentuale della memoria allocata ad Analysis Services. Se, ad esempio, si dispone di 200 GB di memoria totale e per Analysis Services ne viene allocato l'80% (o 160 GB), il 5% di memoria inutilizzata corrisponde al 5% di 160 GB (o 8 GB).  
  
     Questa impostazione di configurazione corrisponde alla definizione della regola seguente nella **Controlla problemi e soluzioni** pagina: **PowerPivot: Analysis Services non ha memoria sufficiente per eseguire le operazioni richieste.**  
  
     Numero massimo di connessioni (l'impostazione predefinita è 100)  
     Questa regola di analisi dell'integrità viene attivata se il numero di connessioni all'istanza di Analysis Services rimane su un valore uguale o superiore a 100 nell'arco di 4 ore (come specificato dall'impostazione Intervallo raccolta dati). Questo valore predefinito è arbitrario (non è basato sulle specifiche hardware del server o sull'attività utente), pertanto è possibile aumentare o diminuire il valore a seconda della capacità del server e dell'attività utente nell'ambiente.  
  
     Questa impostazione di configurazione corrisponde alla definizione della regola seguente nella **Controlla problemi e soluzioni** pagina: **PowerPivot: L'elevato numero di connessioni indica che devono essere distribuiti più server per gestire il carico corrente.**  
  
     Spazio su disco insufficiente (l'impostazione predefinita è 5%)  
     Lo spazio su disco è utilizzato per memorizzare nella cache i dati PowerPivot ogni volta che viene richiesto un database. Questa regola consente di sapere quando lo spazio su disco è insufficiente. Per impostazione predefinita, questa regola di integrità viene attivata quando lo spazio su disco è minore del 5% sull'unità disco in cui si trova la cartella di backup. Per altre informazioni sull'uso del disco, vedere [configurare l'uso di spazio su disco &#40;PowerPivot per SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md).  
  
     Questa impostazione di configurazione corrisponde alla definizione della regola seguente nella **Controlla problemi e soluzioni** pagina: **PowerPivot: Spazio su disco insufficiente sull'unità in cui viene memorizzato nella cache i dati PowerPivot.**  
  
     Intervallo di raccolta dati (in ore)  
     È possibile specificare il periodo di raccolta dei dati utilizzato per calcolare i numeri utilizzati per l'attivazione delle regole di analisi dell'integrità. Benché il sistema sia monitorato costantemente, le soglie utilizzate per attivare gli avvisi delle regole di analisi dell'integrità vengono calcolate utilizzando dati generati in un intervallo predefinito. L'intervallo predefinito è di 4 ore. Il server recupera dati di sistema e di utilizzo raccolti nelle 4 ore precedenti per valutare il numero di connessioni utente, l'utilizzo dello spazio su disco e i tassi di utilizzo della CPU e della memoria.  
  
##  <a name="bkmk_evaluate_application_stability"></a> Configurare le regole di integrità utilizzate per valutare la stabilità dell'applicazione (applicazione del servizio PowerPivot)  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Nella pagina Applicazioni di servizio fare clic su **Applicazione di servizio PowerPivot predefinita**.  
  
     ![Pagina screenshot di gestione delle applicazioni](../media/ssas-centraladmin-app.gif "pagina Screenshot di gestione delle applicazioni")  
  
3.  Verrà visualizzato il dashboard di gestione PowerPivot. Nell'elenco **Azioni** fare clic su **Configura impostazioni dell'applicazione di servizio** per aprire la pagina delle impostazioni dell'applicazione del servizio.  
  
     ![Screenshot del dashboard, concentrarsi sull'elenco azioni](../media/ssas-centraladmin-actionslist.gif "Screenshot del dashboard, concentrarsi sull'elenco azioni")  
  
4.  Nelle impostazioni delle regole di integrità modificare le impostazioni seguenti:  
  
     Rapporto tra carico e connessione (l'impostazione predefinita è 20%)  
     Questa regola di integrità viene attivata se il numero di eventi di caricamento è elevato rispetto al numero di eventi di connessione, segnalando che lo scaricamento dei database potrebbe essere eseguito troppo rapidamente da parte del server o che le impostazioni di riduzione della cache sono troppo rigide.  
  
     Questa impostazione di configurazione corrisponde alla definizione della regola seguente nella **Controlla problemi e soluzioni** pagina: **PowerPivot: Il rapporto tra eventi di caricamento e connessioni è troppo alto.**  
  
     Intervallo di raccolta dati (l'impostazione predefinita è 4 ore)  
     È possibile specificare il periodo di raccolta dei dati utilizzato per calcolare i numeri utilizzati per l'attivazione delle regole di analisi dell'integrità. Benché il sistema sia monitorato costantemente, le soglie utilizzate per attivare gli avvisi delle regole di analisi dell'integrità vengono calcolate utilizzando dati generati in un intervallo predefinito. L'intervallo predefinito è di 4 ore. Il server recupera dati di sistema e di utilizzo raccolti nelle 4 ore precedenti per valutare il rapporto tra carico e connessione.  
  
     Verificare gli aggiornamenti di PowerPivot Management Dashboard.xlsx (l'impostazione predefinita è 5 giorni)  
     Il file PowerPivot Management Dashboard.xlsx è un'origine dati utilizzata dai report in Dashboard di gestione di PowerPivot. In una configurazione server predefinita, il file con estensione xlsx viene aggiornato quotidianamente, tramite i dati di utilizzo raccolti da SharePoint e dal servizio di sistema PowerPivot. Nel caso in cui il file non venga aggiornato, tale problema viene segnalato da una regola di analisi dell'integrità. Per impostazione predefinita, la regola viene attivata se il timestamp del file non viene modificato da 5 giorni.  
  
     Per altre informazioni sulla raccolta dati di utilizzo, vedere [Configure Usage Data Collection per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
     Questa impostazione di configurazione corrisponde alla definizione della regola seguente nella **Controlla problemi e soluzioni** pagina: **PowerPivot: I dati di utilizzo non aggiornati con la frequenza prevista.**  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'utilizzo di spazio su disco &#40;PowerPivot per SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md)   
 [Dati di utilizzo e dashboard di gestione PowerPivot](power-pivot-management-dashboard-and-usage-data.md)  
  
  
