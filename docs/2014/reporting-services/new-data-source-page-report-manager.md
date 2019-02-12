---
title: Nuova origine dati (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 35563d4c-a3d5-4f95-bf46-605da9dfcbb8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: aa144386222c489e9b682942873794669f5b31d6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56029102"
---
# <a name="new-data-source-page-report-manager"></a>Pagina Nuova origine dati (Gestione report)
  Utilizzare la pagina Nuova origine dati per creare un'origine dei dati condivisa. Un'origine dei dati condivisa definisce una connessione a un'origine dei dati esterna. Le origini dati condivise consentono di creare e gestire le impostazioni per la connessione all'origine dati separatamente rispetto ai report, ai modelli e alle sottoscrizioni guidate dai dati che utilizzano tale origine dati.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-new-data-source-page"></a>Per aprire la pagina Nuova origine dati  
  
1.  Aprire Gestione report e navigare fino alla cartella in cui si desidera creare un'origine dati.  
  
2.  Sulla barra degli strumenti, fare clic su **Nuova origine dati**. Per creare un'origine dati condivisa, è necessario disporre delle autorizzazioni Gestione contenuto.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Digitare un nome per l'origine dati condivisa, utilizzato per identificare l'elemento nella gerarchia di cartelle del server di report.  
  
 **Descrizione**  
 Consente di immettere informazioni sull'origine dati condivisa. Questa descrizione viene visualizzata nella pagina Contenuto.  
  
 **Nascondi in visualizzazione elenco**  
 Selezionare questa opzione per fare in modo che l'origine dati condivisa non venga visualizzata per gli utenti che utilizzano la modalità di visualizzazione Elenco in Gestione report. La modalità di visualizzazione Elenco è il formato di visualizzazione predefinito utilizzato per l'esplorazione della gerarchia di cartelle del server di report. Nella visualizzazione Elenco i nomi e le descrizioni degli elementi vengono disposti dall'alto in basso nella pagina. Il formato alternativo è costituito dalla visualizzazione Dettagli, in cui non sono incluse le descrizioni ma sono disponibili altre informazioni sugli elementi. Gli elementi possono essere nascosti nella visualizzazione Elenco ma non nella visualizzazione Dettagli. Se si desidera limitare l'accesso a un elemento, è necessario creare un'assegnazione di ruolo  
  
 **Abilita questa origine dati**  
 Selezionare questa opzione per abilitare o disabilitare l'origine dei dati condivisa. È possibile disabilitare l'origine dati condivisa per impedire l'elaborazione di tutti i report e i modelli che fanno riferimento a tale elemento.  
  
 **Tipo di origine dati**  
 Consente di specificare l'estensione per l'elaborazione dati utilizzata per elaborare i dati dall'origine dati. Il server di report include le estensioni per l'elaborazione dati per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], SAP, XML, ODBC e OLE DB. È possibile che siano disponibili ulteriori estensioni per l'elaborazione dati di terze parti.  
  
 Per altre informazioni sul supporto delle origini dati remote e non SQL, vedere [funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (HYPERLINK "<https://go.microsoft.com/fwlink/?linkid=232473>" <https://go.microsoft.com/fwlink/?linkid=232473>) e [origini dati supportate da Reporting Servizi di &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 **Stringa di connessione**  
 Specificare la stringa di connessione utilizzata dal server di report per la connessione all'origine dati. Il tipo di connessione determina la sintassi da utilizzare. Ad esempio, una stringa di connessione per l'estensione per l'elaborazione dei dati XML è rappresentata da un URL per un documento XML. In una stringa di connessione tipica vengono in genere specificati il server di database e un file di dati.  
  
 Nell'esempio seguente viene illustrata una stringa di connessione utilizzata per la connessione al database [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] :  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 Per altre informazioni ed esempi sui vari modi per specificare una stringa di connessione, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 **Connetti tramite**  
 Consente di specificare le opzioni che determinano come vengono ottenute le credenziali.  
  
> [!IMPORTANT]  
>  Se le credenziali vengono specificate nella stringa di connessione, le opzioni e i valori selezionati in questa sezione vengono ignorati. Si noti che le credenziali specificate nella stringa di connessione sono visibili in forma non crittografata per tutti gli utenti che accedono a questa pagina.  
  
 **Credenziali fornite dall'utente che esegue il report (Connetti tramite)**  
 Tutti gli utenti devono digitare un nome utente e una password per accedere all'origine dei dati. È possibile specificare il testo per il messaggio di richiesta delle credenziali utente. La stringa di testo predefinita è "Immettere nome utente e password per accedere all'origine dati".  
  
 Selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati** se l'utente fornisce credenziali di autenticazione di Windows. Non selezionare questa casella di controllo se si utilizza l'autenticazione del database, ad esempio l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Credenziali archiviate in modo sicuro nel server di report (Connetti tramite)**  
 Consente di archiviare nome utente e password in forma crittografata nel database del server di report. Selezionare questa opzione per l'esecuzione di report in modo automatico, ad esempio report avviati tramite pianificazioni o eventi anziché da un'azione dell'utente. Se si utilizza la sicurezza predefinita, il nome utente deve essere un account di dominio di Windows. Specificare l'account nel formato seguente: \<dominio >\\< nome utente\>. L'account specificato deve disporre di autorizzazioni di accesso locale nel computer che ospita l'origine dati utilizzata dal report.  
  
 Selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati** se vengono utilizzate credenziali di autenticazione di Windows. Non selezionare questa casella di controllo se si utilizza l'autenticazione del database, ad esempio l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Se si utilizza l'autenticazione del database, selezionare **Rappresenta l'utente autenticato dopo che è stata stabilita una connessione all'origine dati** per consentire la delega delle credenziali del database, ma solo se un server di database supporta la rappresentazione. Nei database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] questa opzione consente di impostare la funzione SETUSER.  
  
 **Sicurezza integrata di Windows (Connetti tramite)**  
 Consente di utilizzare le credenziali di Windows dell'utente corrente per accedere all'origine dati. Selezionare questa opzione se le credenziali utilizzate per l'accesso a un'origine dei dati sono le stesse utilizzate per l'accesso al dominio di rete. È consigliabile utilizzare questa opzione quando per il dominio è abilitata l'autenticazione Kerberos oppure quando l'origine dei dati si trova nello stesso computer del server di report. Se l'autenticazione Kerberos non è abilitata, le credenziali di Windows possono essere passate a un solo altro computer. Se sono necessarie ulteriori connessioni al computer, i dati previsti non verranno visualizzati e verrà invece visualizzato un errore.  
  
 Un amministratore del server di report può disabilitare l'utilizzo della sicurezza integrata di Windows per l'accesso alle origini dati del report. Se questo valore è disattivato, la funzionalità non è disponibile.  
  
 Non utilizzare questa opzione se si prevede di pianificare o sottoscrivere questo report. L'elaborazione pianificata o automatica dei report richiede credenziali che è possibile ottenere senza l'input dell'utente o il contesto di sicurezza di un utente corrente. Questa funzionalità è offerta solo dalle credenziali archiviate. Per questo motivo, il server di report impedisce la pianificazione dell'elaborazione di report o di sottoscrizioni se il report è configurato per il tipo di credenziali della sicurezza integrata di Windows. Se si sceglie questa opzione per un report già sottoscritto o per il quale sono previste operazioni pianificate, le sottoscrizioni e le operazioni pianificate vengono arrestate.  
  
 **Non sono necessarie le credenziali (Connetti tramite)**  
 Consente di specificare che non sono necessarie credenziali per l'accesso all'origine dei dati. Si noti che se un'origine dei dati richiede l'accesso da parte degli utenti, la selezione di questa opzione non avrà alcun effetto. È consigliabile selezionare questa opzione solo se la connessione all'origine dei dati non richiede credenziali utente.  
  
 Per utilizzare questa opzione, è necessario avere prima configurato l'account di esecuzione automatica per la distribuzione del server di report. L'account di esecuzione automatica viene utilizzato per la connessione alle origini dati esterne quando le altre origini di credenziali non sono disponibili. Se si specifica questa opzione e l'account non è configurato, la connessione all'origine dati del report ha esito negativo e il report non viene elaborato. Per altre informazioni su questo account, vedere [configurare l'Account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **OK**  
 Fare clic per salvare le modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, eliminare o modificare un'origine dei dati condivisa &#40;Gestione report&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Pagina Contenuto &#40;Gestione report&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Guida F1 di gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
