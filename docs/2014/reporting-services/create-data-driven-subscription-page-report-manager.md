---
title: Pagina Creazione di una sottoscrizione guidata dai dati (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 814b4653-572a-48c7-847f-b310ba0f3046
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 130027d60f5458b451d4f853a79228510c5e7d66
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109622"
---
# <a name="create-data-driven-subscription-page-report-manager"></a>Pagine Creazione di una sottoscrizione guidata dai dati (Gestione report)
  Le pagine Creazione di una sottoscrizione guidata dai dati consentono di compilare o modificare una sottoscrizione che esegue una query su un database sottoscrittore per ottenere informazioni sulla sottoscrizione ogni volta che la sottoscrizione viene eseguita. Le sottoscrizioni guidate dai dati utilizzano i risultati della query per determinare i destinatari della sottoscrizione, le impostazioni di recapito e i valori dei parametri del report. In fase di esecuzione, il server di report esegue una query per recuperare i valori utilizzati per le impostazioni di sottoscrizione. È possibile utilizzare queste pagine per definire la query e assegnare i valori della query alle impostazioni della sottoscrizione. I valori e le opzioni che è possibile impostare per una sottoscrizione guidata dai dati sono suddivisi in più pagine, in modo simile a una procedura guidata. La procedura è composta da un totale di sette pagine.  
  
 Per creare una sottoscrizione guidata dai dati è necessario sapere come scrivere una query o un comando per il recupero dei dati per la sottoscrizione. È inoltre necessario disporre di un archivio dati contenente i dati del sottoscrittore, ad esempio, nomi e indirizzi di posta elettronica, da utilizzare per la sottoscrizione.  
  
 Questa pagina è disponibile per gli utenti con autorizzazioni avanzate. Se si utilizzano le impostazioni di sicurezza predefinite, le sottoscrizioni guidate dai dati non possono essere utilizzate per i report inclusi nelle cartelle Report personali.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-data-driven-subscription-page"></a>Per aprire la pagina Sottoscrizione guidata dai dati  
  
1.  Aprire Gestione report e individuare il report per il quale si desidera creare una sottoscrizione guidata dai dati.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà **generale** per il report.  
  
4.  Selezionare la scheda **Sottoscrizioni** , quindi fare clic su **Nuova sottoscrizione guidata dai dati**.  
  
    > [!NOTE]  
    >  Questo pulsante è abilitato solo se l'origine dati del report utilizza credenziali archiviate.  
  
## <a name="start-a-subscription-page-1"></a>Creazione di una sottoscrizione (pagina 1)  
 **Descrizione**  
 Consente di specificare una descrizione per la sottoscrizione. La descrizione viene visualizzata negli elenchi delle sottoscrizioni in **Sottoscrizioni personali** e nella scheda **Sottoscrizioni** del report.  
  
 **Specificare la modalità di notifica ai destinatari**  
 Consente di selezionare l'estensione per il recapito da utilizzare per la distribuzione del report. Per ogni sottoscrizione è possibile utilizzare una sola estensione per il recapito. Sono disponibili le opzioni seguenti:  
  
-   Selezionare **Condivisione file Server report** per recapitare i report in una condivisione file. Il report verrà recapitato come file statico, disconnesso dal server di report. Per ulteriori informazioni, vedere [File Share Delivery in Reporting Services](subscriptions/file-share-delivery-in-reporting-services.md).  
  
-   Selezionare **Messaggio di posta elettronica da Server report** per recapitare i report nella posta in arrivo. Per altre informazioni, vedere [Recapito tramite posta elettronica in Reporting Services](subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   Selezionare **Provider recapito Null** per recapitare i report nel database del server di report. Questa opzione consente di creare snapshot del report. Selezionare questa opzione se si desidera precaricare nel server di report snapshot del report specifici degli utenti o con parametri in base a una pianificazione specifica. Per altre informazioni, vedere [Memorizzazione dei report nella cache &#40;SSRS&#41;](report-server/caching-reports-ssrs.md).  
  
 **Specificare un'origine dei dati che contenga informazioni sui destinatari**  
 Consente di specificare la modalità di impostazione della connessione all'origine dati. È possibile selezionare un'origine dati condivisa se è già disponibile un'origine dati contenente le informazioni di connessione necessarie. Si possono inoltre impostare direttamente le informazioni di connessione per la sottoscrizione.  
  
 L'origine dei dati fornisce i dati del Sottoscrittore. Tali dati possono includere nomi e ID dei dipendenti, indirizzi di posta elettronica e preferenze per i formati di esportazione (come HTML o PDF). Se si utilizza l'estensione per il recapito tramite posta elettronica del server di report, è necessario che l'origine dati includa indirizzi di posta elettronica.  
  
## <a name="specify-a-connection-page-2"></a>Impostazione della connessione (pagina 2)  
 Se nella pagina precedente è stata selezionata l'opzione per l'utilizzo di un'origine dati condivisa, selezionare tale origine dati condivisa in questa pagina. È possibile utilizzare il controllo albero per individuare e selezionare l'origine dati. Se si sta impostando una connessione per questa sottoscrizione, specificare le opzioni seguenti in questa pagina:  
  
 **Tipo di connessione**  
 Consente di selezionare l'estensione per l'elaborazione dati da utilizzare con l'origine dei dati.  
  
 **Stringa di connessione**  
 Consente di digitare la stringa di connessione da utilizzare per connettersi all'origine dei dati.  
  
 **Connetti tramite**  
 Consente di digitare le credenziali da utilizzare per la connessione all'origine dei dati. Le credenziali vengono archiviate come valori crittografati nel database del server di report.  
  
 Se l'origine dati utilizza l'autenticazione di Windows, selezionare **Usa come credenziali di Windows** quando si specifica la connessione.  
  
 Se si utilizza un'origine dati che non prevede l'autenticazione delle connessioni utente, ad esempio se l'origine dati è un file XML, selezionare Credenziali non richieste. Per questa opzione è necessario che sia stato configurato l'account di esecuzione automatica. Per altre informazioni, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="specify-a-query-page-3"></a>Impostazione della query (pagina 3)  
 Utilizzare questa pagina per immettere la query che consente di recuperare i dati del Sottoscrittore. Per ottenere risultati migliori, eseguire la query in SQL Server Management Studio prima di utilizzarla nella sottoscrizione guidata dai dati. È quindi possibile analizzare i risultati per verificare che contengano le informazioni necessarie. Gli aspetti importanti da tenere presenti nei risultati della query sono i seguenti:  
  
-   Le colonne nel set di risultati determinano i valori che è possibile specificare per le opzioni di recapito e i parametri del report. Se, ad esempio, si sta creando una sottoscrizione guidata dai dati per il recapito tramite posta elettronica, è necessario disporre di una colonna di indirizzi di posta elettronica.  
  
-   Le righe nel set di risultati determinano il numero di recapiti del report generati. Se sono presenti 10.000 righe, il server di report genererà 10.000 notifiche e recapiti.  
  
 **Query**  
 Specificare una query o un comando SQL per il recupero di un set di risultati contenente una sola riga per ogni destinatario della sottoscrizione. Nelle pagine successive, il set di risultati viene utilizzato per popolare le impostazioni relative all'estensione guidata dai dati.  
  
 **Timeout**  
 Consente di specificare un valore di timeout per la query. Questo valore deve essere sufficiente per consentire il completamento dell'elaborazione della query.  
  
 **Convalida**  
 Fare clic su **Convalida** per verificare la query. Per continuare è necessario che la query generi risultati validi. Se non si fa clic su **Convalida**, la query viene comunque convalidata quando si fa clic su **Avanti**.  
  
## <a name="set-delivery-options-page-4"></a>Impostazione delle opzioni di recapito (pagina 4)  
 Nella quarta pagina è possibile specificare le opzioni dell'estensione per il recapito. Le opzioni disponibili dipendono dall'estensione per il recapito. Le modalità di impostazione di tali opzioni possono variare in modo significativo a seconda di come le opzioni vengono presentate dall'estensione per il recapito. Se l'estensione non prevede impostazioni particolari, in questa pagina non verrà visualizzata alcuna opzione.  
  
|Opzione|Per|  
|-----------------|----------------|  
|**Specificare un valore statico**|Utilizzare un valore costante per l'impostazione del recapito. Alcune estensioni per il recapito rendono disponibili valori statici tra i quali selezionare quello desiderato. Ad esempio, per il recapito tramite posta elettronica del server di report vengono visualizzati valori per **Includi report**, **Formato di rendering**, **Priorità**e **Includi collegamento**.|  
|**Estrai il valore dal database**|Utilizzare un valore dal set di risultati. Le colonne del set di risultati possono essere utilizzate per fornire dati del Sottoscrittore e valori dei parametri del report.|  
|**Nessun valore**|Omettere l'impostazione nella sottoscrizione.|  
  
#### <a name="set-delivery-options-for-file-share-delivery"></a>Impostazione delle opzioni di recapito per il recapito alla condivisione file  
 L'estensione per il recapito alla condivisione file viene utilizzata spesso in quanto non richiede una configurazione preventiva. Se si utilizza l'estensione per il recapito alla condivisione file, nella tabella seguente sono descritte le opzioni che è possibile impostare:  
  
 **Nome file**  
 Specificare un nome file per il report. L'estensione per il recapito alla condivisione file consente di recapitare un report come file di applicazione statico a una cartella condivisa. Nella maggior parte dei casi, è necessario utilizzare un valore del database per creare il nome file. In base all'impostazione della modalità di scrittura, se viene utilizzato un valore statico ogni nuovo recapito può sovrascrivere il recapito precedente.  
  
 **Percorso**  
 Specificare una cartella condivisa accessibile in una connessione di rete. Per verificare che la cartella sia accessibile, fare clic su **Esegui** nel menu Start e immettere il percorso della cartella nel \\ \\ formato:<\> \\ nomecomputer<\>nomecartellacondivisa.  
  
 **Formato rendering**  
 Specificare il formato di output del file. Il file può essere scritto nei formati di applicazione delle estensioni di rendering installate nel server di report.  
  
 **Modalità scrittura**  
 Specificare se il server di report deve sostituire un file con una versione più recente, incrementarlo o eliminare il recapito se viene trovato un file con lo stesso nome.  
  
 **Estensione di file**  
 Specificare True per aggiungere un'estensione di file corrispondente al formato di rendering selezionato.  
  
 **Nome utente**  
 Immettere l'account utente di dominio che dispone delle autorizzazioni per aggiungere file alla cartella condivisa nel formato \<dominio>\\<nome utente\>.  
  
 **Password**  
 Immettere la password per l'account.  
  
## <a name="set-parameters-page-5"></a>Impostazione dei parametri (pagina 5)  
 Se un report include parametri è necessario specificare i valori dei parametri da utilizzare con il report. I valori dei parametri possono essere recuperati dall'origine dati di sottoscrizione. Ad esempio, nel caso di un report con parametri sulle vendite regionali basato sul codice di regione, è possibile ottenere informazioni sulla regione per ogni dipendente se tali informazioni sono archiviate nel database dei dipendenti.  
  
|Opzione|Per|  
|-----------------|----------------|  
|**Specificare un valore statico**|Utilizzare un valore costante per il parametro se si desidera utilizzare lo stesso parametro per tutti i sottoscrittori. Se il parametro prevede più valori, è possibile selezionare un valore nell'elenco.|  
|**Usa valore predefinito**|Alcuni report contengono un valore predefinito per tutti i parametri o alcuni di essi. Se il parametro del report dispone di un valore predefinito, fare clic su questa casella di controllo per utilizzarlo.|  
|**Estrai il valore dal database**|Utilizzare un valore dal set di risultati. Le colonne del set di risultati possono essere selezionate come origine per il valore di dati da utilizzare con ogni istanza della sottoscrizione.|  
  
## <a name="specify-a-trigger-page-6"></a>Impostazione di un trigger (pagina 6)  
 Selezionare un evento per l'avvio dell'elaborazione della sottoscrizione.  
  
|Opzione|Per|  
|-----------------|----------------|  
|**Quando i dati del report vengono aggiornati nel server di report**|Se il report è configurato per l'esecuzione come snapshot dell'esecuzione del report, è possibile specificare che la sottoscrizione deve essere eseguita quando lo snapshot viene aggiornato.|  
|**In base a una pianificazione creata per questa sottoscrizione**|Eseguire la sottoscrizione nella data e all'ora specificate.|  
|**In base a una pianificazione condivisa**|Eseguire la sottoscrizione in base alle informazioni di pianificazione fornite tramite una pianificazione condivisa.|  
  
## <a name="schedule-a-subscription-page-7"></a>Pianificazione di una sottoscrizione (pagina 7)  
 Se si sceglie di pianificare la sottoscrizione, è necessario impostare la frequenza di recapito del report. Il primo set di opzioni consente di specificare la frequenza (oraria, giornaliera, settimanale e così via). Il secondo set di opzioni varia a seconda dell'opzione selezionata nel primo gruppo e consente di impostare ulteriori dettagli della pianificazione.  
  
 **Oraria**  
 Consente di impostare una pianificazione eseguita a intervalli di ore.  
  
 **Giornaliera**  
 Consente di impostare una pianificazione eseguita nei giorni selezionati a un'ora specifica. È possibile specificare i giorni nei modi seguenti: ogni * \<giorno>*, ogni giorno feriale e ogni * \<numero>* giorno. La selezione di un'opzione determina la disattivazione delle altre anche se può sembrare che siano selezionati altri giorni.  
  
 **Settimanale**  
 Consente di impostare una pianificazione eseguita settimanalmente a un'ora specifica. È possibile impostare un intervallo di una o più settimane intere (ad esempio, ogni due settimane) oppure i giorni della settimana.  
  
 **Ogni mese**  
 Consente di impostare una pianificazione eseguita su base mensile. Per una pianificazione mensile è possibile scegliere un giorno in base a uno schema (ad esempio l'ultima domenica di ogni mese) oppure date specifiche (ad esempio 1 e 15 per indicare il primo e il quindicesimo giorno di ogni mese). Per specificare più giorni e intervalli è possibile utilizzare virgole e trattini, ad esempio, 1, 5, 7-12, 21.  
  
 **Una volta**  
 Consente di definire una pianificazione eseguita una sola volta. Utilizzare le opzioni nella sezione **Date di inizio e fine** per specificare il giorno di esecuzione della pianificazione. La pianificazione scade subito dopo l'elaborazione.  
  
 **Date di inizio e fine**  
 Consente di specificare le date di inizio e fine, ovvero la data di attivazione e la data di scadenza della pianificazione. La scadenza delle pianificazioni non viene notificata. Dopo la data di scadenza, le pianificazioni non vengono più eseguite.  
  
## <a name="saving-the-subscription"></a>Salvataggio della sottoscrizione  
 Il pulsante **Fine** viene abilitato quando sono disponibili informazioni sufficienti per la sottoscrizione. Fare clic su **Fine** per completare l'impostazione della sottoscrizione.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
