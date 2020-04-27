---
title: Pagina delle proprietà generale, origini dati condivise (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1b344449-6f7c-47d2-a737-972d88c0faf8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1de9a0091fa072fccea4825d31deb50463f6cd8c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109081"
---
# <a name="general-properties-page-shared-data-sources-report-manager"></a>Pagina delle proprietà Generale, Origini dati condivise (Gestione report)
  La pagina delle proprietà Generale consente di visualizzare o modificare le proprietà di un elemento origine dati condivisa. Quando si fa clic su **Applica**, tutte le modifiche apportate alle proprietà vengono applicate a tutti i report che fanno riferimento all'origine dei dati condivisa.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-general-properties-page-for-a-shared-data-source"></a>Per aprire la pagina delle proprietà Generale per un'origine dati condivisa  
  
1.  Aprire Gestione report, quindi individuare l'origine dati condivisa per la quale si desidera visualizzare le proprietà.  
  
2.  Passare con il puntatore del mouse sull'origine dati, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per l'origine dati condivisa.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di specificare il nome dell'origine dati condivisa, utilizzato per identificare l'elemento nello spazio dei nomi del server di report.  
  
 **Descrizione**  
 Consente di specificare informazioni sull'origine dei dati condivisa. Questa descrizione viene visualizzata nella pagina Contenuto.  
  
 **Nascondi in visualizzazione Elenco**  
 Selezionare questa opzione per fare in modo che l'origine dati condivisa non venga visualizzata per gli utenti che utilizzano la modalità di visualizzazione Elenco in Gestione report. La modalità di visualizzazione Elenco è il formato di visualizzazione predefinito utilizzato per l'esplorazione della gerarchia di cartelle del server di report. Nella visualizzazione Elenco i nomi e le descrizioni degli elementi vengono disposti dall'alto in basso nella pagina. Il formato alternativo è costituito dalla visualizzazione Dettagli, in cui non sono incluse le descrizioni ma sono disponibili altre informazioni sugli elementi. Gli elementi possono essere nascosti nella visualizzazione Elenco ma non nella visualizzazione Dettagli. Se si desidera limitare l'accesso a un elemento, è necessario creare un'assegnazione di ruolo.  
  
 **Abilita questa origine dei dati**  
 Selezionare questa opzione per abilitare o disabilitare l'origine dei dati condivisa. È possibile disabilitare l'origine dei dati condivisa per evitare che vengano elaborati tutti i report, i modelli di report e le sottoscrizioni guidate dai dati che fanno riferimento a tale origine dei dati.  
  
 **Tipo di origine dati**  
 Consente di selezionare l'estensione per l'elaborazione dati utilizzata per elaborare i dati dall'origine dei dati. Il server di report include estensioni per l' [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]elaborazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]dati per,, Oracle, XML [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], SAP,, ODBC e OLE DB. È possibile che siano disponibili ulteriori estensioni per l'elaborazione dati di terze parti.  
  
 Si noti che se si utilizza [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] Edition with Advanced Services, è possibile scegliere solo origini dati di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Stringa di connessione**  
 Specificare la stringa di connessione utilizzata dal server di report per la connessione all'origine dati. Il tipo di connessione determina la sintassi da utilizzare. Ad esempio, una stringa di connessione per l'estensione per l'elaborazione dei dati XML è rappresentata da un URL per un documento XML. In una stringa di connessione tipica vengono in genere specificati il server di database e un file di dati. Nell'esempio seguente viene illustrata una stringa di connessione utilizzata per la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] connessione al database:  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 **Connetti tramite**  
 Consente di specificare le opzioni che determinano la modalità di recupero delle credenziali.  
  
> [!IMPORTANT]  
>  Se le credenziali vengono specificate nella stringa di connessione, le opzioni e i valori selezionati in questa sezione vengono ignorati. Si noti che le credenziali specificate nella stringa di connessione sono visibili in forma non crittografata per tutti gli utenti che accedono a questa pagina.  
  
 **Le credenziali fornite dall'utente che esegue il report**  
 Tutti gli utenti devono digitare un nome utente e una password per accedere all'origine dati. È possibile specificare il testo per il messaggio di richiesta delle credenziali utente. La stringa di testo predefinita è "Immettere nome utente e password per accedere all'origine dati".  
  
 Selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati** se l'utente fornisce credenziali di autenticazione di Windows. Non selezionare questa casella di controllo se si utilizza il sistema di autenticazione del database, ad esempio l'autenticazione di SQL Server.  
  
 **Credenziali archiviate in modo protetto nel server di report**  
 Consente di archiviare nome utente e password in forma crittografata nel database del server di report. Selezionare questa opzione per eseguire un report in modo automatico, ad esempio nel caso di report avviati tramite pianificazioni o eventi anziché da un'azione dell'utente. Se si utilizza la sicurezza predefinita, il nome utente deve essere un account di dominio di Windows. Specificare l'account nel formato: \<dominio>\\<nome utente\>. L'account specificato deve disporre di autorizzazioni di accesso locale nel computer che ospita l'origine dati utilizzata dal report.  
  
 Selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati** se vengono utilizzate credenziali di autenticazione di Windows. Non selezionare questa casella di controllo se si utilizza l'autenticazione del database, ad esempio l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Se si utilizza l'autenticazione del database, selezionare **Rappresenta l'utente autenticato dopo che è stata stabilita una connessione all'origine dei dati (Connetti tramite)** per consentire la delega delle credenziali del database, ma solo se un server di database supporta la rappresentazione. Nei database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] questa opzione consente di impostare la funzione SETUSER.  
  
 **Sicurezza integrata di Windows**  
 Consente di utilizzare le credenziali di Windows dell'utente corrente per accedere all'origine dati. Selezionare questa opzione se le credenziali utilizzate per l'accesso a un'origine dati corrispondono a quelle utilizzate per l'accesso al dominio di rete. È consigliabile utilizzare questa opzione quando per il dominio è attivato il protocollo Kerberos oppure quando l'origine dati è disponibile nello stesso computer del server di report. Se l'autenticazione Kerberos non è abilitata, le credenziali di Windows possono essere passate a un altro computer. Se sono necessarie ulteriori connessioni al computer, i dati previsti non verranno visualizzati e verrà invece visualizzato un errore.  
  
 Un amministratore del server di report può disabilitare l'utilizzo della sicurezza integrata di Windows per l'accesso alle origini dati del report. Se questo valore è disattivato, la funzionalità non è disponibile.  
  
 Non utilizzare questa opzione se si prevede di pianificare o sottoscrivere questo report. L'elaborazione pianificata o automatica dei report richiede credenziali che è possibile ottenere senza l'input dell'utente o il contesto di sicurezza di un utente corrente. Questa funzionalità è offerta solo dalle credenziali archiviate. Per questo motivo, il server di report impedisce la pianificazione dell'elaborazione di report o di sottoscrizioni se il report è configurato per il tipo di credenziali della sicurezza integrata di Windows. Se si sceglie questa opzione per un report già sottoscritto o per il quale sono previste operazioni pianificate, le sottoscrizioni e le operazioni pianificate vengono arrestate.  
  
 **Le credenziali non sono necessarie**  
 Consente di specificare che non sono necessarie credenziali per l'accesso all'origine dei dati. Si noti che se un'origine dei dati richiede l'accesso da parte degli utenti, la selezione di questa opzione non avrà alcun effetto. È consigliabile selezionare questa opzione solo se la connessione all'origine dei dati non richiede credenziali utente.  
  
 Per utilizzare questa opzione, è necessario avere prima configurato l'account di esecuzione automatica per la distribuzione del server di report. L'account di esecuzione automatica viene utilizzato per la connessione alle origini dati esterne quando le altre origini di credenziali non sono disponibili. Se si specifica questa opzione e l'account non è configurato, la connessione all'origine dati del report ha esito negativo e il report non viene elaborato. Per ulteriori informazioni su questo account, vedere [configurare l'account di esecuzione automatica &#40;SSRS Configuration Manager&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **Applica**  
 Fare clic per salvare le modifiche.  
  
 **Elimina**  
 Fare clic per eliminare l'origine dati condivisa. Quando si elimina un'origine dati condivisa, vengono disattivati tutti i report, le sottoscrizioni guidate dai dati e i modelli che la utilizzano. Per riattivare un report, una sottoscrizione o un modello, è necessario aprirlo e aggiornare le proprietà dell'origine dati per l'utilizzo di un'altra origine dati condivisa. Per i report e le sottoscrizioni le informazioni sulla connessione all'origine dati possono essere specificate come valori della proprietà Origine dati.  
  
 **Spostamento**  
 Fare clic per spostare l'origine dati condivisa in una posizione diversa nello spazio dei nomi della cartella del server di report.  
  
 **Genera modello**  
 Fare clic per creare un nuovo modello basato sull'origine dati condivisa.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Pagina nuova origine dati &#40;Gestione report&#41;](../../2014/reporting-services/new-data-source-page-report-manager.md)   
 [Guida sensibile al contesto Gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
