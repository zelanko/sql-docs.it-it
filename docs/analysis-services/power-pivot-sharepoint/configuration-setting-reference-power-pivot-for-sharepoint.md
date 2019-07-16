---
title: Configurazione di impostazione di riferimento (Power Pivot per SharePoint) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e2da78373d8bcb613bb11dca54857bc7b98dfe1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208338"
---
# <a name="configuration-setting-reference-power-pivot-for-sharepoint"></a>Documentazione di riferimento per le impostazioni di configurazione (Power Pivot per SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Questo argomento include la documentazione di riferimento per le impostazioni di configurazione usate dalle applicazioni di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una farm di SharePoint. Nelle informazioni incluse in questo argomento vengono fornite descrizioni dettagliate per gli utenti che utilizzano uno script di PowerShell per configurare un server o che desiderano cercare informazioni per un'impostazione specifica.  
  
 Le impostazioni di configurazione vengono specificate per ogni applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . All'interno di una farm è possibile creare più applicazioni di servizio per configurare istanze logiche indipendenti della stessa istanza fisica del servizio. Le impostazioni di configurazione vengono archiviate nel database dell'applicazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] creato per ogni applicazione di servizio configurata.  
  
 Se si modificano le impostazioni di configurazione, le modifiche vengono accolte immediatamente e utilizzate per le richieste e le connessioni successive. Le operazioni in corso vengono regolate in base alle impostazioni in vigore all'inizio dell'operazione.  
  
 Fare clic sui collegamenti seguenti per informazioni su aree di configurazione specifiche:  
  
 [Timeout caricamento dati](#LoadingData)  
  
 [Pool di connessioni](#ConnectionPool)  
  
 [Bilanciamento del carico](#AllocationScheme)  
  
 [Aggiornamento dei dati](#DataRefresh)  
  
 [Raccolta dati di utilizzo](#UsageData)  
  
 Per altre informazioni su come creare un'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , vedere [Creare e configurare un'applicazione del servizio Power Pivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
##  <a name="LoadingData"></a> Timeout caricamento dati  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] I dati di vengono recuperati e caricati dalle istanze del server Analysis Services nella farm. A seconda della modalità e della data di esecuzione dell'ultimo accesso ai dati, verranno caricati da una raccolta contenuto o da una cache di file locale. I dati vengono caricati in memoria ogni volta che si riceve una query o una richiesta di elaborazione. Per ottimizzare la disponibilità complessiva del server, è possibile impostare un valore di timeout che consente l'arresto di una richiesta di caricamento dati da parte del server se non è possibile completarla entro il tempo stabilito.  
  
|Name|Impostazione predefinita|Valori validi|Descrizione|  
|----------|-------------|------------------|-----------------|  
|Timeout caricamento dati|1800 (in secondi)|Da 1 a 3600|Specifica la durata di attesa di una risposta da un'istanza specifica del server Analysis Services da parte di un'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Per impostazione predefinita, l'applicazione di servizio attende 30 minuti per un payload dei dati dall'istanza del servizio Motore a cui è stata inoltrata una richiesta specifica.<br /><br /> Se non è possibile caricare l'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] entro questo intervallo di tempo, il thread verrà arrestato e ne verrà avviato uno nuovo.|  
  
##  <a name="ConnectionPool"></a> Pool di connessioni  
 L'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] consente di creare e gestire pool di connessioni in modo da abilitare il riutilizzo delle connessioni. Esistono due tipi di pool di connessioni: uno per le connessioni dati ai dati di sola lettura e un secondo per le connessioni ai server.  
  
 I pool di connessioni dati contengono le connessioni memorizzate nella cache per l'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Ogni pool di connessioni è basato sul contesto impostato durante il caricamento del database. In questo contesto sono inclusi l'identità dell'istanza fisica del servizio, l'ID database e l'identità dell'utente di SharePoint che richiede i dati. Viene creato un pool di connessioni distinto per ogni combinazione. Ad esempio, per le richieste inoltrate da utenti diversi dello stesso database in esecuzione sul medesimo server vengono utilizzate connessioni di pool diversi.  
  
 Lo scopo di un pool di connessioni consiste nell'utilizzare le connessioni memorizzate nella cache per le richieste di sola lettura per lo stesso database di Analysis Services da parte del medesimo utente di SharePoint. L'istanza del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è il server in cui sono disponibili i dati caricati in memoria. L'ID database è un identificatore interno per le strutture di dati in memoria del modello di dati (viene creata un'istanza di un modello come database di un cubo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ). Le informazioni sulla versione sono incorporate in modo implicito nell'identificatore.  
  
 I pool di connessioni server contengono le connessioni memorizzate nella cache da un'istanza dell'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in un'istanza del server Analysis Services, in cui l'applicazione di servizio si connette con autorizzazioni Sysadmin di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nel server Analysis Services. Queste connessioni vengono utilizzate per inviare una richiesta di caricamento del database e monitorare l'integrità del sistema.  
  
 Per ogni tipo di pool di connessioni sono previsti dei limiti massimi che è possibile impostare per garantire il miglior utilizzo della memoria di sistema per la gestione delle connessioni.  
  
|Nome|Impostazione predefinita|Valori validi|Descrizione|  
|----------|-------------|------------------|-----------------|  
|Timeout pool di connessioni|1800 (in secondi)|Da 1 a 3600.|Questa impostazione si applica ai pool di connessioni dati.<br /><br /> Consente di specificare per quanto tempo una connessione inattiva può rimanere in un pool di connessioni prima di essere rimossa.<br /><br /> Per impostazione predefinita, una connessione che resta inattiva per più di cinque minuti verrà rimossa tramite l'applicazione del servizio.|  
|Dimensioni massime pool di connessioni utente|1000|-1, 0 o da 1 a 10000.<br /><br /> -1 indica un numero illimitato di connessioni inattive.<br /><br /> 0 indica che non vengono mantenute connessioni inattive. È necessario creare ogni volta nuove connessioni a un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|Questa impostazione si applica al numero di connessioni inattive in tutti i pool di connessioni dati creati per una specifica istanza dell'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Vengono creati pool di connessioni singoli per combinazioni univoche di un utente di SharePoint, dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e un'istanza del servizio. Se molti utenti accedono a più origini dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , le prestazioni del server potrebbero essere migliorate tramite un aumento delle dimensioni del pool di connessioni.<br /><br /> Se sono presenti più di 100 connessioni inattive a un'istanza del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , le connessioni inattive più recenti vengono disconnesse piuttosto che restituite al pool.|  
|Dimensioni massime pool di connessioni di amministrazione|200|-1, 0 o da 1 a 10000.<br /><br /> -1 indica un numero illimitato di connessioni inattive.|Numero massimo di connessioni server inattive in tutti i pool di connessioni amministrative creati per le connessioni dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a un'istanza del server Analysis Services. Le connessioni server vengono utilizzate per le richieste per caricare i database e salvare nuovamente le modifiche nel database di SharePoint.|  
  
##  <a name="AllocationScheme"></a> Bilanciamento del carico  
 Una delle funzioni eseguite tramite il servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] consiste nel determinare dove verranno caricati i dati di Analysis Services tra le istanze del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] disponibili. L'impostazione di **AllocationMethod** specifica i criteri in base ai quali viene selezionata un'istanza del servizio.  
  
|Name|Impostazione predefinita|Valori validi|Descrizione|  
|----------|-------------|------------------|-----------------|  
|Metodo di allocazione|RoundRobin|Round robin<br /><br /> Basato sull'integrità|Schema di allocazione delle richieste di caricamento tra due o più istanze del server Analysis Services.<br /><br /> Per impostazione predefinita, il servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] consentirà di alternare le richieste in base allo stato di integrità del server. La metodologia basata sull'integrità consente di allocare le richieste sul server che dispone della maggior parte delle risorse di sistema utilizzabili in base alla memoria disponibile e all'utilizzo della CPU.<br /><br /> Il round robin consente una rotazione delle richieste tra i vari server disponibili, indipendentemente dal carico corrente o dall'integrità del server.|  
  
##  <a name="DataRefresh"></a> Aggiornamento dei dati  
 Specificare l'intervallo di ore che consente di definire una giornata lavorativa normale o tipica dell'organizzazione. Queste impostazioni di configurazione permettono di determinare l'orario non lavorativo in cui viene eseguita l'elaborazione dati per le operazioni di aggiornamento dei dati. L'elaborazione fuori orario lavorativo può essere avviata in coincidenza con l'ora di fine della giornata lavorativa. L'elaborazione fuori orario lavorativo è un'opzione di pianificazione destinata ai proprietari di documenti che vogliono aggiornare un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] con i dati transazionali generati durante il normale orario lavorativo.  
  
|Nome|Impostazione predefinita|Valori validi|Descrizione|  
|----------|-------------|------------------|-----------------|  
|Ora inizio|4\.00 A.M.|Da 1 a 12 ore, dove il valore è un numero intero valido all'interno di quell'intervallo.<br /><br /> Il tipo è Time.|Consente di impostare il limite inferiore di un intervallo orario lavorativo.|  
|Ora fine|08.00 P.M.|Da 1 a 12 ore, dove il valore è un numero intero valido all'interno di quell'intervallo.<br /><br /> Il tipo è Time.|Consente di impostare il limite superiore di un intervallo orario lavorativo.|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Account di aggiornamento dati automatico|Nessuna|ID dell'applicazione di destinazione|Questo account viene utilizzato per eseguire processi di aggiornamento dati per conto del proprietario di una pianificazione.<br /><br /> È necessario definire prima un'account di aggiornamento dati automatico per potervi fare riferimento nella pagina di configurazione dell'applicazione di servizio. Per altre informazioni, vedere [Configurare l'account di aggiornamento dati automatico di Power Pivot (Power Pivot per SharePoint)](http://msdn.microsoft.com/81401eac-c619-4fad-ad3e-599e7a6f8493).|  
|Consenti agli utenti di immettere credenziali di Windows personalizzate|Enabled|Boolean|Determina se la pagina di configurazione dell'aggiornamento dati pianificato mostra un'opzione che consente a un proprietario di pianificazione di specificare account utente e password per eseguire un processo di aggiornamento dati.<br /><br /> Il servizio di archiviazione sicura deve essere abilitato affinché questa opzione funzioni. Per altre informazioni, vedere [Configurare le credenziali archiviate per l'aggiornamento dati PowerPivot (PowerPivot per SharePoint)](http://msdn.microsoft.com/987eff0f-bcfe-4bbd-81e0-9aca993a2a75).|  
|Lunghezza massima cronologia di elaborazione|365|Da 1 a 5000 giorni|Determina per quanto tempo viene conservata la cronologia dell'aggiornamento dati nel database dell'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per altre informazioni, vedere [Power Pivot Usage Data Collection](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md).|  
  
##  <a name="UsageData"></a> Raccolta dati di utilizzo  
 I report sull'uso visualizzati nel dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] possono fornire informazioni importanti sull'uso delle cartelle di lavoro abilitate per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Le impostazioni di configurazione seguenti consentono di controllare alcuni aspetti della raccolta dei dati di utilizzo per eventi del server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] presentati successivamente nei report relativi all'uso o alle attività.  
  
|Nome|Impostazione predefinita|Valori validi|Descrizione|  
|----------|-------------|------------------|-----------------|  
|Intervallo di report query|300 (in secondi)|Da 1 a n secondi, dove n è qualsiasi numero intero valido.|Per garantire che per la raccolta dei dati sull'utilizzo non venga impegnata una percentuale eccessiva della capacità di trasferimento dati della farm, le statistiche sulle query vengono raccolte in ogni connessione e segnalate come un unico evento. Intervallo di report query consente di determinare la frequenza con cui viene segnalato un evento. Per impostazione predefinita, le statistiche sulle query vengono segnalate ogni 5 minuti.<br /><br /> Poiché le connessioni vengono chiuse immediatamente dopo l'invio di una richiesta, viene generato un numero molto elevato di connessioni anche per un singolo utente che accede a una sola origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per questo motivo, vengono creati pool di connessioni per ogni combinazione di utente e origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in modo che, dopo aver creato una connessione, questa possa essere riutilizzata dallo stesso utente per i medesimi dati. Periodicamente, agli intervalli specificati tramite questa impostazione di configurazione, l'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] genera i report relativi ai dati di utilizzo per ogni connessione del relativo pool.<br /><br /> Se si aumenta il valore dell'intervallo di segnalazione, verrà registrato un numero inferiore di eventi. Se il valore impostato è troppo elevato, tuttavia, si rischia di perdere i dati relativi agli eventi al riavvio del server o alla chiusura di una connessione.<br /><br /> La riduzione del valore determina la registrazione di più eventi con maggiore frequenza, con l'aggiunta di più dati di utilizzo correlati a [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]al sistema di raccolta dati nel database dell'uso di SharePoint.<br /><br /> È in genere opportuno evitare di modificare questa impostazione di configurazione, tranne che durante un tentativo di risoluzione di un problema specifico, ad esempio se le dimensioni del database dell'utilizzo stanno aumentando troppo rapidamente a causa dei dati di utilizzo di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Cronologia dati di utilizzo|365 (in giorni)|0 o da 1 a n giorni, dove n è qualsiasi numero intero valido.<br /><br /> 0 indica che la cronologia viene mantenuta sempre, senza essere mai eliminata.|Per impostazione predefinita, i dati di utilizzo vengono mantenuti per un anno nel database dell'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . I record generati da più di un anno vengono eliminati dal database.<br /><br /> Viene effettuato un controllo giornaliero dei dati cronologici scaduti, durante l'esecuzione del processo di elaborazione dati sull'utilizzo di Microsoft SharePoint Foundation. Tramite il processo timer, questa impostazione verrà letta e verrà attivato un comando di eliminazione dei dati per la cronologia scaduta nel database dell'applicazione di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Limite massimo risposta semplice|500 (in millisecondi)|Da 1 a n millisecondi, dove n è qualsiasi numero intero valido.|Per impostazione predefinita, la soglia per le richieste semplici è di mezzo secondo.<br /><br /> Tra le richieste semplici sono inclusi ping del server, richieste per i metadati e sessioni di avvio.|  
|Limite massimo risposta rapida|1000 (in millisecondi)|Da 1 a n millisecondi, dove n è qualsiasi numero intero valido.|Per impostazione predefinita, la soglia per le richieste rapide è un secondo.<br /><br /> Le richieste rapide dispongono in genere di un set di dati estremamente ridotto oppure corrispondono a richieste per metadati che si estendono tra set con membri di elevate dimensioni.|  
|Limite massimo risposta prevista|3000 (in millisecondi)|Da 1 a n millisecondi, dove n è qualsiasi numero intero valido.|Per impostazione predefinita, la soglia per le richieste previste è tre secondi.<br /><br /> Con questa soglia viene impostato il limite superiore della durata di una query prevista.|  
|Limite massimo risposta lunga|10000 (in millisecondi)|Da 1 a n millisecondi, dove n è qualsiasi numero intero valido.|Per impostazione predefinita, la soglia per le richieste lunghe è dieci secondi.<br /><br /> Si tratta di richieste per la cui esecuzione è necessaria una durata maggiore del previsto e che tuttavia rientrano in un intervallo accettabile.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e configurare un'applicazione del servizio Power Pivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Aggiornamento dati PowerPivot con SharePoint 2010](http://msdn.microsoft.com/01b54e6f-66e5-485c-acaa-3f9aa53119c9)   
 [Configurare la raccolta dati di utilizzo per PowerPivot per SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Configurare gli account del servizio PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Dati di utilizzo e dashboard di gestione PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)  
  
  
