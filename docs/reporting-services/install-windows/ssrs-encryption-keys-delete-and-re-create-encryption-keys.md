---
title: Eliminare e ricreare chiavi di crittografia (Gestione configurazione) | Microsoft Docs
description: Le attività di eliminazione e ricreazione di chiavi di crittografia non rientrano nella manutenzione di routine delle chiavi di crittografia.
ms.date: 12/04/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.custom: seo-lt-2019, seo-mmd-2019
ms.topic: conceptual
helpviewer_keywords:
- recreating encryption keys
- encryption keys [Reporting Services]
- deleting encryption keys
- symmetric keys [Reporting Services]
- removing encryption keys
- resetting encryption keys
ms.assetid: 201afe5f-acc9-4a37-b5ec-121dc7df2a61
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 60e0814a72d09ff8612ef6d14a6ef7abfd2e92f1
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934664"
---
# <a name="delete-and-recreate-encryption-keys-report-server-configuration-manager"></a>Eliminare e ricreare chiavi di crittografia (Gestione configurazione del server di report)
  Le attività di eliminazione e ricreazione di chiavi di crittografia non rientrano nella manutenzione di routine delle chiavi di crittografia. Tali attività vengono eseguite in risposta a una specifica minaccia al server di report oppure come ultima risorsa quando non è più possibile accedere a un database del server di report.  
  
-   Ricreare la chiave simmetrica quando si ritiene che quella esistente sia compromessa. È anche possibile ricreare la chiave regolarmente come procedura consigliata per la sicurezza.  
  
-   Eliminare le chiavi di crittografia esistenti e il contenuto crittografato inutilizzabile quando non è possibile ripristinare la chiave simmetrica.  
  
## <a name="recreating-encryption-keys"></a>Ricreazione di chiavi di crittografia  
 Se si ha la prova che la chiave simmetrica sia nota a utenti non autorizzati oppure se il server di report è stato attaccato, come misura di sicurezza è possibile ricreare la chiave simmetrica in modo da reimpostarla. Se si ricrea la chiave simmetrica, tutti i valori crittografati verranno crittografati nuovamente usando il nuovo valore. Se si eseguono più server in una distribuzione con scalabilità orizzontale, tutte le copie della chiave simmetrica verranno aggiornate in base al nuovo valore. Il server di report utilizza le chiavi pubbliche disponibili per aggiornare la chiave simmetrica per ogni server presente nella distribuzione.  
  
 La chiave simmetrica può essere ricreata solo quando il server di report è in uno stato attivo. La ricreazione delle chiavi di crittografia e la riesecuzione della crittografia del contenuto interferisce con le operazioni del server. Durante l'operazione di riesecuzione della crittografia il server deve essere offline e il server di report non deve ricevere richieste.  
  
 Per reimpostare la chiave simmetrica e i dati crittografati è possibile usare lo strumento di configurazione di Reporting Services o l'utilità **rskeymgmt** . Per altre informazioni sulla creazione della chiave simmetrica, vedere [Inizializzare un server di report &#40;Gestione configurazione del server di report&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
### <a name="how-to-recreate-encryption-keys-reporting-services-configuration-tool"></a>Come ricreare chiavi di crittografia (strumento di configurazione di Reporting Services)  
  
1.  Disabilitare il servizio Web ReportServer e l'accesso HTTP modificando la proprietà **IsWebServiceEnabled** nel file rsreportserver.config. Questo passaggio arresta temporaneamente l'invio delle richieste di autenticazione al server di report senza arrestare completamente il server. È necessario disporre di un servizio minimo per poter ricreare le chiavi.  
  
     Se vengono ricreate chiavi di crittografia per una distribuzione con scalabilità orizzontale del server di report, disabilitare questa proprietà in tutte le istanze presenti nella distribuzione.  
  
    1.  Aprire Esplora risorse e passare all' *unità*:\Programmi\Microsoft SQL Server\\*istanza_server_report*\Reporting Services. Sostituire *unità* con la lettera dell'unità locale e *istanza_server_report* con il nome della cartella che corrisponde all'istanza del server di report per cui si vuole disabilitare il servizio Web e l'accesso HTTP. Ad esempio, C:\Programmi\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services.  
  
    2.  Aprire il file rsreportserver.config.  
  
    3.  Per la proprietà **IsWebServiceEnabled** , specificare **False**e salvare le modifiche.  
  
2.  Avviare lo strumento di configurazione di Reporting Services e quindi connettersi all'istanza del server di report che si desidera configurare.  
  
3.  Nella pagina Chiave di crittografia fare clic su **Cambia**. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Riavviare il servizio Windows ReportServer. Se si ricreano chiavi di crittografia per una distribuzione con scalabilità orizzontale, riavviare il servizio su tutte le istanze.  
  
5.  Riabilitare il servizio Web e l'accesso HTTP modificando la proprietà **IsWebServiceEnabled** nel file rsreportserver.config. Se si utilizza una distribuzione con scalabilità orizzontale, eseguire questa procedura per tutte le istanze.  
  
### <a name="how-to-recreate-encryption-keys-rskeymgmt"></a>Come ricreare chiavi di crittografia (rskeymgmt)  
  
1.  Disabilitare il servizio Web ReportServer e l'accesso HTTP. Per arrestare le operazioni del servizio Web, seguire le istruzioni riportate nella procedura precedente.  
  
2.  Eseguire l'utilità **rskeymgmt.exe** nel computer locale che ospita il server di report. Per reimpostare la chiave simmetrica, usare l'argomento **-s** . Non sono necessari altri argomenti:  
  
    ```  
    rskeymgmt -s  
    ```  
  
3.  Riavviare il servizio Windows per Reporting Services.  
  
## <a name="deleting-unusable-encrypted-content"></a>Eliminazione di contenuto crittografato non utilizzabile  
 Se per qualsiasi motivo non è possibile ripristinare la chiave di crittografia, il server di report non è in grado di decrittografare e utilizzare dati crittografati con quella chiave. Per ripristinare lo stato attivo del server di report, è necessario eliminare i valori crittografati attualmente archiviati nel database del server di report e quindi specificare di nuovo manualmente i valori necessari.  
  
 Se si eliminano le chiavi di crittografia, verranno rimosse tutte le informazioni relative alla chiave simmetrica dal database del server di report e verrà eliminato tutto il contenuto crittografato. Tutti i dati non crittografati rimarranno invariati. Verrà eliminato solo il contenuto crittografato. Quando si eliminano le chiavi di crittografia, il server di report viene reinizializzato automaticamente mediante l'aggiunta di una nuova chiave simmetrica. Quando viene eliminato contenuto crittografato, si verifica quanto riportato di seguito:  
  
-   Vengono eliminate le stringhe di connessione nelle origini dei dati condivise. Per gli utenti che eseguono report viene visualizzato l'errore "La proprietà ConnectionString non è stata inizializzata".  
  
-   Le credenziali archiviate vengono eliminate. I report e le origini dei dati condivise vengono riconfigurati in modo da utilizzare le credenziali richieste.  
  
-   I report basati su modelli, e che richiedono origini dei dati condivise configurate con credenziali archiviate o prive di credenziali, non vengono eseguiti.  
  
-   Le sottoscrizioni vengono disattivate.  
  
 Il contenuto crittografato eliminato non potrà essere recuperato. Oltre a specificare di nuovo le stringhe di connessione e le credenziali archiviate, è necessario attivare le sottoscrizioni.  
  
 Per rimuovere i valori è possibile usare lo strumento di configurazione di Reporting Services o l'utilità **rskeymgmt** .  
  
### <a name="how-to-delete-encryption-keys-reporting-services-configuration-tool"></a>Come eliminare chiavi di crittografia (strumento di configurazione di Reporting Services)  
  
1.  Avviare lo strumento di configurazione di Reporting Services e quindi connettersi all'istanza del server di report che si desidera configurare.  
  
2.  Fare clic su **Chiave di crittografia**e quindi su **Elimina**. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Riavviare il servizio Windows ReportServer. Per una distribuzione con scalabilità orizzontale, eseguire questa procedura per tutte le istanze del server di report.  
  
### <a name="how-to-delete-encryption-keys-rskeymmgt"></a>Come eliminare chiavi di crittografia (rskeymgmt)  
  
1.  Eseguire l'utilità **rskeymgmt.exe** nel computer locale che ospita il server di report. È necessario usare l'argomento di applicazione **-d** . Nell'esempio seguente viene illustrato l'argomento che è necessario specificare:  
  
    ```  
    rskeymgmt -d  
    ```  
  
2.  Riavviare il servizio Windows ReportServer. Per una distribuzione con scalabilità orizzontale, eseguire questa procedura per tutte le istanze del server di report.  
  
### <a name="how-to-re-specify-encrypted-values"></a>Come specificare di nuovo i valori crittografati  
  
1.  Digitare di nuovo la stringa di connessione per ogni origine dei dati condivisa.  
  
2.  Digitare di nuovo il nome utente e la password per ogni report e origine dati condivisa che utilizza le credenziali archiviate, quindi salvare. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
3.  Aprire ogni sottoscrizione guidata dai dati e digitare di nuovo le credenziali per l'accesso al database di sottoscrizione.  
  
4.  Aprire ogni sottoscrizione che utilizza dati crittografati, incluse l'estensione per il recapito tramite condivisione file ed eventuali estensioni per il recapito di terze parti che utilizzano la crittografia, e quindi digitare di nuovo le credenziali. Le sottoscrizioni che utilizzano il recapito tramite posta elettronica di Report Server non utilizzano dati crittografati e quindi non sono interessate dalla modifica delle chiavi.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione del server di report&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [Archiviare i dati crittografati del server di report &#40;Gestione configurazione del server di report&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
