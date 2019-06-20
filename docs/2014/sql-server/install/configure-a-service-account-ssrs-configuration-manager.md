---
title: Configurare un Account del servizio (Gestione configurazione SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Server Web service, accounts
- service accounts [Reporting Services]
- Report Server Windows service, accounts
- Web service [Reporting Services], report server
ms.assetid: 25000ad5-3f80-4210-8331-d4754dc217e0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 84f6f2bdb4c5c512cb75dfea554b5ae28e3c3f02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096103"
---
# <a name="configure-a-service-account-ssrs-configuration-manager"></a>Configurare un account del servizio (Gestione configurazione SSRS)
  In un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] il servizio Web Report Server, Gestione report e l'applicazione di elaborazione in background vengono eseguiti all'interno di un singolo servizio. L'account utilizzato per l'esecuzione di tale servizio viene definito durante l'installazione, quando si specifica l'account nella pagina Identità servizio Web, ma è possibile utilizzare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se si desidera utilizzare un account diverso oppure aggiornare la password.  
  
 Se si dispone di un server di report configurato per usare la modalità integrata SharePoint e si modifica l'account di servizio usando il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] strumento di configurazione, è necessario anche aprire Amministrazione centrale SharePoint e utilizzare il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  **Concedi accesso al Database** pagina per applicare nuovamente le impostazioni di istanza e del server di report. Questo passaggio concederà al nuovo servizio account accesso al database di SharePoint, che è necessario per l'integrazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
 Utilizzare sempre lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per aggiornare l'account del servizio in modo da per poter aggiornare simultaneamente anche le impostazioni che dipendono dall'identità del servizio.  
  
> [!NOTE]  
>  Gli account di servizio Windows predefiniti (Servizio locale o Servizio di rete) non sono supportati come account del servizio del server di report su un computer con funzioni di controller di dominio.  
  
 Procedure  
  
### <a name="to-configure-the-report-server-service-account"></a>Per configurare l'account del servizio del server di report  
  
1.  Avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi al server di report.  
  
2.  Nella pagina Account servizio selezionare l'opzione che descrive il tipo di account che si desidera utilizzare. Per indicazioni su quale tipo di account da specificare, vedere [configurare l'Account del servizio ReportServer &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
3.  Se è stato selezionato un account utente di Windows, specificare il nuovo account e la password. Il nome dell'account non può contenere più di 20 caratteri.  
  
     Se il server di report viene distribuito in una rete che supporta l'autenticazione Kerberos, è necessario registrare il nome dell'entità servizio del server di report con l'account utente di dominio specificato. Per altre informazioni, vedere [Registrare un nome dell'entità servizio &#40;SPN&#41; per un server di report](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
4.  Fare clic su **Applica**.  
  
5.  Quando viene richiesto di eseguire il backup della chiave simmetrica, digitare un nome di file e un percorso per la copia di backup della chiave simmetrica, digitare una password per bloccare e sbloccare il file, quindi scegliere **OK**.  
  
6.  Se il server di report utilizza l'account del servizio per connettersi al database del server di report, le informazioni di connessione verranno aggiornate per l'utilizzo del nuovo account o della nuova password. L'aggiornamento delle informazioni di connessione richiede la connessione al database. Se viene visualizzata la finestra di dialogo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Database Connection** dialog box appears, enter credentials that have permission to connect to the database, and then click **OK**.  
  
7.  Quando viene richiesto di ripristinare la chiave simmetrica, digitare la password specificata al passaggio 5, quindi scegliere **OK**.  
  
8.  Controllare i messaggi di stato nel riquadro Risultati per verificare che tutte le attività siano state completate correttamente.  
  
## <a name="troubleshooting-service-identity-update-errors"></a>Risoluzione degli errori di aggiornamento dell'identità del servizio  
 La modifica dell'identità del servizio avvia una serie di eventi che includono il riavvio del servizio, l'aggiornamento della chiave di crittografia protetta da password, l'aggiornamento delle prenotazioni URL e, se si utilizza l'account del servizio per la connessione al database del server di report, l'aggiornamento delle informazioni di connessione al database del server di report. È possibile monitorare lo stato di tali eventi visualizzando le notifiche incluse nel riquadro Risultati nella parte inferiore della pagina. Se durante il processo si verificano errori, è possibile provare a risolverli utilizzando le tecniche seguenti:  
  
-   Se non è possibile ripristinare la chiave simmetrica, tentare di ripristinarla manualmente usando il comando **Ripristina** nella pagina Chiave di crittografia. Se il problema persiste, valutare l'opportunità di eliminare il contenuto crittografato. In questo caso, sarà necessario ricreare le informazioni di connessione all'origine dati e le sottoscrizioni, ma il resto del contenuto sarà ancora disponibile. Per altre informazioni, vedere [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
-   Se non è possibile avviare il servizio, riavviarlo manualmente utilizzando l'applicazione console Servizi in Strumenti di amministrazione.  
  
-   Quando si aggiorna l'account del servizio, possono verificarsi errori relativi alle prenotazioni URL. Ogni prenotazione URL include un descrittore di sicurezza che include a sua volta un elenco di controllo di accesso discrezionale che concede all'account del servizio l'autorizzazione necessaria per accettare richieste nell'URL. Quando si aggiorna l'account, è necessario ricreare l'URL per aggiornare l'elenco di controllo di accesso discrezionale con le nuove informazioni sull'account. Se non è possibile ricreare la prenotazione URL e si è certi della validità dell'account, provare a riavviare il computer. Se l'errore persiste, provare a utilizzare un account diverso.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Account del servizio &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/service-account-ssrs-native-mode.md)   
 [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
