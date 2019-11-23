---
title: Chiavi di crittografia (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.encryptionkeypanel.F1
ms.assetid: cc7e6f84-80e1-4b5e-9409-d0e074edd147
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 540cf25a150349c7b6399975d20d10bc202ed935
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952175"
---
# <a name="encryption-keys-ssrs-native-mode"></a>Chiavi di crittografia (modalità nativa SSRS)
  Utilizzare la pagina Chiave di crittografia per gestire la chiave simmetrica utilizzata per crittografare e decrittografare i dati in un server di report. La gestione delle chiavi di crittografia rappresenta una parte fondamentale della configurazione del server di report. La chiave simmetrica viene creata e applicata automaticamente quando si crea il database del server di report. Creare una copia di backup della chiave simmetrica in modo da poter eseguire le operazioni di manutenzione periodiche. Per le attività di manutenzione indicate di seguito, è necessario disporre di una copia valida della chiave simmetrica:  
  
-   Modifica dell'account del servizio del server di report.  
  
-   Migrazione di un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un computer diverso.  
  
-   Configurazione di una nuova istanza del server di report da condividere o utilizzo di un database del server di report esistente.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  La modifica periodica della chiave di crittografia di Reporting Services è una procedura consigliata ai fini della sicurezza. È consigliabile modificare la chiave immediatamente dopo un aggiornamento della versione principale di Reporting Services. Modificando la chiave di crittografia di Reporting Services dopo un aggiornamento si riduce il rischio di ulteriori interruzioni del servizio rispetto invece all'eseguire questa operazione all'esterno del ciclo di aggiornamento.  
  
 Il ripristino della chiave simmetrica è necessario se l'account utente del servizio del server di report è stato aggiornato utilizzando uno strumento diverso da Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oppure se si esegue la migrazione di un'installazione del server di report in un nuovo server.  
  
 Per proteggerla dall'accesso non autorizzato, la chiave simmetrica viene crittografata utilizzando la chiave privata del servizio del server di report. Solo il servizio del server di report è in grado di sbloccare e utilizzare la chiave simmetrica per archiviare i dati sensibili nel database del server di report. Se si modifica l'identità del servizio del server di report o si esegue la migrazione del server di report a un nuovo computer, non sarà più possibile sbloccare la chiave simmetrica utilizzando la chiave privata del servizio del server di report. Per ripristinare l'accesso alla chiave simmetrica, è necessario crittografarla di nuovo utilizzando la chiave privata della nuova identità del servizio del server di report. Il ripristino della chiave simmetrica è il processo tramite cui viene effettuata la ricrittografia.  
  
 Ripristinare solo la chiave simmetrica se è quella attualmente utilizzata per crittografare e decrittografare i dati nel database del server di report. Se si ripristina una chiave simmetrica non valida, non è più possibile accedere ai dati sensibili. In questo caso, eliminare e ricreare la chiave.  
  
> [!IMPORTANT]  
>  L'azione di eliminazione e ricreazione della chiave simmetrica non può essere invertita o annullata e può comportare conseguenze significative nell'installazione corrente. Se si elimina la chiave, verranno eliminati anche tutti i dati esistenti crittografati con questa chiave simmetrica. I dati eliminati possono includere stringhe di connessione a origini dei dati esterne per i report, stringhe di connessione archiviate e alcune informazioni relative alle sottoscrizioni.  
  
 Per aprire questa pagina, avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e selezionare il collegamento nel riquadro di navigazione. Per altre informazioni, vedere [Reporting Services Configuration Manager &#40;Native Mode&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Backup**  
 Consente di copiare la chiave simmetrica in un file specificato. La chiave simmetrica non viene mai archiviata in testo non crittografato. Per la protezione del file, è necessario digitare una password.  
  
 **Ripristina**  
 Consente di applicare una copia della chiave simmetrica salvata in precedenza al database del server di report. Per sbloccare il file, è necessario specificare la password.  
  
 La copia della chiave simmetrica eseguita in precedenza per l'istanza del server di report a cui si è attualmente connessi viene sovrascritta dalla versione ripristinata. Dopo avere ripristinato la chiave simmetrica, è necessario inizializzare tutti i server di report che utilizzano il database del server di report. Per ulteriori informazioni sull'inizializzazione di server di report, vedere [Initialize &#40;a report&#41;server SSRS Configuration Manager](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
 **Modificare**  
 Consente di ricreare la chiave simmetrica e di crittografare di nuovo tutti i valori crittografati nel database del server di report. Accertarsi di arrestare il servizio del server di report prima di ricreare la chiave simmetrica.  
  
 In una distribuzione con scalabilità orizzontale ogni copia della chiave simmetrica viene sostituita con versioni più recenti. Prima di modificare la chiave simmetrica, accertarsi di controllare l'elenco dei server uniti alla distribuzione con scalabilità orizzontale per verificare che l'accesso alla nuova chiave venga concesso solo alle istanze del server di report valide. L'elenco dei server che fanno parte di una distribuzione con scalabilità orizzontale è disponibile nella pagina **Distribuzione con scalabilità orizzontale** . Prima di ricreare la chiave, arrestare il servizio in tutti i server di report inclusi nella distribuzione.  
  
 Si noti che la rigenerazione della chiave simmetrica può essere un processo con esecuzione prolungata, se le origini dei dati e le sottoscrizioni sono numerose.  
  
 **Delete**  
 Consente di eliminare la chiave simmetrica e tutto il contenuto crittografato, incluse le stringhe di connessione e le credenziali archiviate. La chiave simmetrica deve essere eliminata solo se non è possibile ripristinarla.  
  
 Dopo aver eliminato la chiave simmetrica, è necessario immettere di nuovo le stringhe di connessione e le credenziali archiviate nei report, nonché le origini dei dati per cui questi valori non sono più validi. È inoltre necessario aggiornare tutte le sottoscrizioni che utilizzano estensioni per il recapito in cui sono archiviati dati crittografati, incluse l'estensione per il recapito di condivisione dei file e l'estensione per il recapito di terze parti che utilizzano valori crittografati.  
  
 Non esiste alcun modo per aggiornare automaticamente queste informazioni. Ogni report, sottoscrizione e origine dei dati condivisa che fa uso di credenziali archiviate e stringhe di connessione deve essere aggiornato uno alla volta.  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services Configuration Manager &#40;argomenti della Guida sensibile al contesto&#41;  modalità nativa SSRS](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
 [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminare e ricreare chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
