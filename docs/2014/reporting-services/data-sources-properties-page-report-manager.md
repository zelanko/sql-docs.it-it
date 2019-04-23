---
title: Proprietà origini dati (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f37edda0-19e6-489e-b544-8751fa6b6cfb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 00bc66f116a489858d6383d90a17e730792e6325
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59941637"
---
# <a name="data-sources-properties-page-report-manager"></a>Pagina delle proprietà Origini dati (Gestione report)
  La pagina delle proprietà Origini dati consente di definire la modalità di connessione del report corrente a un'origine dati esterna. In questa pagina è possibile sostituire le informazioni di connessione all'origine dati pubblicate originalmente con il report. Se per un report vengono utilizzate più origini dati, nella pagina delle proprietà è disponibile una sezione specifica per ogni origine dati. Le origini dati vengono elencate nell'ordine in cui sono definite nel report.  
  
 Per specificare l'origine dati da utilizzare nel report, è possibile utilizzare un'origine dati condivisa creata e gestita separatamente dai report che la utilizzano. Se non si desidera utilizzare un'origine dei dati condivisa, è possibile definire una connessione all'origine dati da utilizzare con il report.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-data-sources-properties-page"></a>Per aprire la pagina delle proprietà Origini dati  
  
1.  Aprire Gestione report e individuare il report per il quale si desidera selezionare un'origine dati.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà **Generale** per il report.  
  
4.  Selezionare la scheda **Origini dati** .  
  
## <a name="options"></a>Opzioni  
 **Un'origine dati condivisa**  
 Consente di specificare un'origine dati condivisa da utilizzare con il report. Per altre informazioni sulla creazione di una nuova origine dati, vedere [creare, eliminare o modificare un'origine dati condivisa &#40;gestione Report&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md).  
  
 **Sfoglia**  
 Fare clic su **Sfoglia** per aprire la pagina di selezione dell'origine dei dati nella quale è possibile selezionare un'origine dei dati condivisa. Per altre informazioni, vedere [pagina Selezione origine dati &#40;gestione Report&#41;](../../2014/reporting-services/data-source-selection-page-report-manager.md).  
  
 **Un'origine dati personalizzata**  
 Consente di impostare la modalità di connessione del report all'origine dei dati.  
  
 Per specificare una connessione a un'origine dati personalizzata, vengono utilizzate le opzioni seguenti:  
  
 **Tipo di origine dati**  
 Consente di specificare l'estensione per l'elaborazione dati utilizzata per elaborare i dati dall'origine dati. Per l'elenco delle estensioni dati incorporate, vedere [origini dati supportate da Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md). È possibile che siano disponibili ulteriori estensioni per l'elaborazione dati di terze parti.  
  
 **Stringa di connessione**  
 Specificare la stringa di connessione utilizzata dal server di report per la connessione all'origine dati. Il tipo di connessione determina la sintassi da utilizzare. Ad esempio, una stringa di connessione per l'estensione per l'elaborazione dei dati XML è rappresentata da un URL per un documento XML. In una stringa di connessione tipica vengono in genere specificati il server di database e un file di dati. Nell'esempio seguente viene illustrata una stringa di connessione utilizzata per la connessione al database MyData di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
 `data source=<a SQL Server instance>;initial catalog=MyData`  
  
 È possibile configurare una stringa di connessione come espressione in modo da poter specificare l'origine dati in fase di esecuzione. Le espressioni dell'origine dati sono definite nel report in Progettazione report. L'espressione dell'origine dati non può essere definita, visualizzata o modificata in Gestione report. È tuttavia possibile sostituire un'espressione delle origini dei dati scegliendo **Ignora predefinita** per digitare una stringa di connessione statica. Per tornare nuovamente all'espressione, fare clic su **Ripristina predefinita**. Nel server di report viene archiviata la stringa di connessione originale che può essere utilizzata nel caso sia necessario ripristinarla. Per utilizzare le espressioni dell'origine dati, è necessario utilizzare le informazioni di connessione all'origine dati pubblicate originariamente con il report. Le origini dati condivise non supportano l'utilizzo di espressioni nella stringa di connessione.  
  
 **Connetti tramite**  
 Consente di specificare le opzioni che determinano la modalità di recupero delle credenziali.  
  
> [!IMPORTANT]  
>  Se le credenziali vengono specificate nella stringa di connessione, le opzioni e i valori selezionati in questa sezione vengono ignorati. Si noti che le credenziali specificate nella stringa di connessione sono visibili in forma non crittografata per tutti gli utenti che accedono a questa pagina.  
  
 **Credenziali fornite dall'utente che esegue il report**  
 Tutti gli utenti devono digitare un nome utente e una password per accedere all'origine dati. È possibile specificare il testo per il messaggio di richiesta delle credenziali utente. La stringa di testo predefinita è "Immettere nome utente e password per accedere all'origine dati".  
  
 Selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati** se l'utente fornisce credenziali di autenticazione di Windows. Non selezionare questa casella di controllo se si utilizza l'autenticazione del database, ad esempio l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Credenziali archiviate in modo sicuro nel server di report**  
 Consente di archiviare nome utente e password in forma crittografata nel database del server di report. Selezionare questa opzione per eseguire un report in modo automatico, ad esempio nel caso di report avviati tramite pianificazioni o eventi anziché da un'azione dell'utente. Se si utilizza la sicurezza predefinita, il nome utente deve essere un account di dominio di Windows. Specificare l'account nel formato seguente: \<dominio >\\< nome utente\>. L'account specificato deve disporre di autorizzazioni di accesso locale nel computer che ospita l'origine dati utilizzata dal report.  
  
 Selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati** se vengono utilizzate credenziali di autenticazione di Windows. Non selezionare questa casella di controllo se si utilizza l'autenticazione del database, ad esempio l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Selezionare **Rappresenta l'utente autenticato dopo che è stata stabilita una connessione all'origine dei dati** per consentire la delega delle credenziali, ma solo se un'origine dati supporta la rappresentazione. Nei database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] questa opzione consente di impostare la funzione SETUSER.  
  
> [!TIP]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]supporta solo le credenziali dell'account di Windows. Pertanto, selezionare entrambe le opzioni "Usa come credenziali di Windows per la connessione all'origine dei dati" e "Rappresenta l'utente autenticato dopo che è stata stabilita una connessione all'origine dei dati" per un'origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Sicurezza integrata di Windows**  
 Consente di utilizzare le credenziali di Windows dell'utente corrente per accedere all'origine dati. Selezionare questa opzione se le credenziali utilizzate per l'accesso a un'origine dati corrispondono a quelle utilizzate per l'accesso al dominio di rete. È consigliabile utilizzare questa opzione quando per il dominio è abilitata l'autenticazione Kerberos oppure quando l'origine dei dati si trova nello stesso computer del server di report. Se l'autenticazione Kerberos non è abilitata, le credenziali di Windows possono essere passate a un altro computer. Se sono necessarie ulteriori connessioni al computer, i dati previsti non verranno visualizzati e verrà invece visualizzato un errore.  
  
 Un amministratore del server di report può disabilitare l'utilizzo della sicurezza integrata di Windows per l'accesso alle origini dati del report. Se questo valore è disattivato, la funzionalità non è disponibile.  
  
 Non utilizzare questa opzione se si prevede di pianificare o sottoscrivere questo report. L'elaborazione pianificata o automatica dei report richiede credenziali che è possibile ottenere senza l'input dell'utente o il contesto di sicurezza di un utente corrente. Questa funzionalità è offerta solo dalle credenziali archiviate. Per questo motivo, il server di report impedisce la pianificazione dell'elaborazione di report o di sottoscrizioni se il report è configurato per il tipo di credenziali della sicurezza integrata di Windows. Se si sceglie questa opzione per un report già sottoscritto o per il quale sono previste operazioni pianificate, le sottoscrizioni e le operazioni pianificate vengono arrestate.  
  
 **Non sono richieste credenziali**  
 Consente di specificare che non sono necessarie credenziali per l'accesso all'origine dei dati. Si noti che se un'origine dei dati richiede l'accesso da parte degli utenti, la selezione di questa opzione non avrà alcun effetto. È consigliabile selezionare questa opzione solo se la connessione all'origine dei dati non richiede credenziali utente.  
  
 Per utilizzare questa opzione, è necessario avere prima configurato l'account di esecuzione automatica per la distribuzione del server di report. L'account di esecuzione automatica viene utilizzato per la connessione alle origini dati esterne quando le altre origini di credenziali non sono disponibili. Se si specifica questa opzione e l'account non è configurato, la connessione all'origine dati del report ha esito negativo e il report non viene elaborato.  Per altre informazioni su questo account, vedere [configurare l'Account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **Applica**  
 Fare clic per salvare le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire origini dati dei report](report-data/manage-report-data-sources.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
