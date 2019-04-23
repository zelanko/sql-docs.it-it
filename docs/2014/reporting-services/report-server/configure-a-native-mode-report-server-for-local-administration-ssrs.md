---
title: Configurare un server di report in modalità nativa per gli amministratori locali (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- UAC
- installing Reporting Services
- Windows Vista
- Localhost
- windows server 2008
- Vista
ms.assetid: 312c6bb8-b3f7-4142-a55f-c69ee15bbf52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 96926b2c7c305bf685bc91206072755081ed35a4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967927"
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>Configurare un server di report in modalità nativa per gli amministratori locali (SSRS)
  Per la distribuzione di un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in uno dei seguenti sistemi operativi sono necessarie ulteriori operazioni di configurazione se si desidera amministrare localmente un'istanza del server di report. Questo argomento spiega come configurare il server di report per l'amministrazione locale. Se non si è ancora installato o configurato il server di report, vedere [installare SQL Server 2014 dall'installazione guidata di &#40;installazione&#41; ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) e [gestire un Reporting Services in modalità Server di Report nativa](manage-a-reporting-services-native-mode-report-server.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] |  
  
-   [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]  
  
-   [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]  
  
-   [!INCLUDE[win8](../../includes/win8-md.md)]  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
 Poiché i sistemi operativi menzionati rimuovono le autorizzazioni, i membri del gruppo Administrators locale eseguono la maggior parte delle applicazioni come se utilizzassero l'account utente standard.  
  
 Benché questa prassi migliori la sicurezza complessiva del sistema, impedisce l'utilizzo delle assegnazioni di ruolo predefinite create da Reporting Services per gli amministratori locali.  
  
-   [Panoramica delle modifiche di configurazione](#bkmk_configuraiton_overview)  
  
-   [Per configurare l'amministrazione locale del server di report e Gestione report](#bkmk_configure_local_server)  
  
-   [Per configurare SQL Server Management Studio (SSMS) per l'amministrazione locale del server di report](#bkmk_configure_ssms)  
  
-   [Per configurare SQL Server Data Tools BI (SSDT) per la pubblicazione in un Server di Report locale](#bkmk_configure_ssdt)  
  
-   [Informazioni aggiuntive](#bkmk_addiitonal_informaiton)  
  
##  <a name="bkmk_configuraiton_overview"></a> Panoramica delle modifiche di configurazione  
 Le seguenti modifiche di configurazione consentono di configurare il server in modo tale da utilizzare autorizzazioni utente standard per le gestione del contenuto e le operazioni del server di report:  
  
-   Aggiungere gli URL di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ai siti attendibili. Per impostazione predefinita, nei sistemi operativi seguenti Internet Explorer viene eseguito in **modalità protetta**. Questa funzionalità impedisce alle richieste del browser di accedere a processi di alto livello in esecuzione nello stesso computer. È possibile disabilitare la modalità protetta per le applicazioni del server di report aggiungendo le applicazioni come Siti attendibili.  
  
-   Creare assegnazioni di ruolo che concedono all'amministratore del server di report l'autorizzazione necessaria per gestire il contenuto e le operazioni senza dover utilizzare la funzionalità **Esegui come amministratore** in Internet Explorer. Creando assegnazioni di ruolo per l'account utente di Windows, è possibile accedere a un server di report con le autorizzazioni Gestione contenuto e Amministratore sistema tramite assegnazioni di ruolo esplicite che sostituiscono le assegnazioni di ruolo predefinite create da Reporting Services.  
  
##  <a name="bkmk_configure_local_server"></a> Per configurare l'amministrazione locale del server di report e Gestione report  
 Se si sta esplorando un server di report locale e vengono visualizzati errori simili ai seguenti, completare i passaggi di configurazione riportati in questa sezione.  
  
-   L'utente `'Domain\[user name]`' non dispone delle autorizzazioni necessarie. Verificare che siano state concesse autorizzazioni sufficienti e che le restrizioni di Controllo account utente di Windows siano state gestite.  
  
###  <a name="bkmk_site_settings"></a> Impostazioni dei siti attendibili nel browser  
  
1.  Aprire una finestra del browser utilizzando autorizzazioni Esegui come amministratore. Dal menu **Start** scegliere **Tutti i programmi**, fare clic con il pulsante destro del mouse su **Internet Explorer**e scegliere **Esegui come amministratore**.  
  
2.  Fare clic su **Consenti** per continuare.  
  
3.  Nell'indirizzo URL immettere l'URL di Gestione report. Per istruzioni, vedere [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Fare clic su **Strumenti**.  
  
5.  Fare clic su **Opzioni Internet**.  
  
6.  Fare clic su **Sicurezza**.  
  
7.  Fare clic su **Siti attendibili**.  
  
8.  Fare clic su **Siti**.  
  
9. Aggiungere `http://<your-server-name>`.  
  
10. Se non si usa HTTPS per il sito predefinito, deselezionare la casella di controllo **Richiedi verifica server (https:) per tutti i siti compresi nell'area** .  
  
11. Scegliere **Aggiungi**.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_folder_settings"></a> Impostazioni cartella Gestione report)  
  
1.  Nella home page di Gestione report fare clic su **Impostazioni cartella**.  
  
2.  Nella pagina Impostazioni cartella fare clic su **Sicurezza**.  
  
3.  Fare clic su **Nuova assegnazione ruolo**.  
  
4.  Nel campo **Nome gruppo o utente** digitare l'account utente di Windows utilizzando il formato: `<domain>\<user>`.  
  
5.  Selezionare **Gestione contenuto**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_site_settings"></a> Impostazioni sito Gestione report  
  
1.  Aprire il browser con i privilegi di amministratore e accedere a Gestione report, `http://<server name>/reports`.  
  
2.  Fare clic su **Impostazioni sito** nell'angolo superiore della home page.  
  
    > [!TIP]  
    >  **Nota:** Se non viene visualizzato il **Impostazioni sito** opzione, chiudere e riaprire il browser e passare a Gestione report con privilegi amministrativi.  
  
3.  Fare clic su **Sicurezza**.  
  
4.  Fare clic su **Nuova assegnazione ruolo**.  
  
5.  Nel campo **Nome gruppo o utente** digitare l'account utente di Windows utilizzando il formato: `<domain>\<user>`.  
  
6.  Selezionare **Amministratore sistema**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Chiudere Gestione report.  
  
9. Riaprire Gestione report in Internet Explorer senza usare le autorizzazioni **Esegui come amministratore**.  
  
##  <a name="bkmk_configure_ssms"></a> Per configurare SQL Server Management Studio (SSMS) per l'amministrazione locale del server di report  
 Per impostazione predefinita, non è possibile accedere a tutte le proprietà dei server di report in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] a meno che non si esegua [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] con privilegi di amministratore.  
  
 **Per configurare proprietà e assegnazioni dei ruoli di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** , pertanto, non è necessario avviare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] con autorizzazioni elevate tutte le volte:  
  
-   Dal menu **Start** scegliere **Tutti i programmi**e **SQL Server 2014**, fare clic con il pulsante destro del mouse su **[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]** e quindi scegliere **Esegui come amministratore**.  
  
-   Connessione al server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] locale.  
  
-   Nel nodo **Sicurezza** fare clic su **Ruoli a livello di sistema**.  
  
-   Fare clic con il pulsante destro del mouse su **Amministratore sistema** e quindi scegliere **Proprietà**.  
  
-   Nella pagina **Proprietà ruolo a livello di sistema** , selezionare **Visualizzazione delle proprietà del server di report**. Selezionare le altre proprietà che si desidera associare ai membri del ruolo degli amministratori di sistema.  
  
-   Fare clic su **OK**.  
  
-   Chiudere [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   Per aggiungere un utente al ruolo di sistema "amministratore di sistema", vedere la sezione [Impostazioni sito Gestione report](#bkmk_configure_site_settings) più indietro in questo argomento.  
  
 Quando si apre [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e non si seleziona esplicitamente **Esegui come amministratore** si ha accesso alle proprietà del server di report.  
  
##  <a name="bkmk_configure_ssdt"></a> Per configurare SQL Server Data Tools BI (SSDT) per la pubblicazione in un Server di Report locale  
 Se è stato installato [!INCLUDE[SSDTDev11](../../includes/ssdtdev11-md.md)] in uno dei sistemi operativi indicati nella prima sezione di questo argomento e si vuole che SSDT interagisca con un server di report in modalità nativa locale, si verificheranno problemi di autorizzazione a meno che non si apra [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] con autorizzazioni elevate o si configurino ruoli di Reporting Services. Ad esempio, se non si dispone di autorizzazioni sufficienti, si verificheranno problemi simili ai seguenti:  
  
-   Quando si tenta di distribuire elementi dei report nel server di report del computer, viene visualizzato un messaggio di errore simile al seguente nella finestra **Elenco errori** :  
  
    -   Le autorizzazioni concesse all'utente 'Dominio\\<nome utente\>' non sono sufficienti per eseguire questa operazione.  
  
 **Per eseguire con autorizzazioni elevate tutte le volte che si apre SSDT:**  
  
1.  Dalla schermata start, digitare `sql server` e quindi fare doppio clic su **SQL Server Data Tools per Visual Studio**. Fare clic su **Esegui come amministratore**.  
  
     **Oppure**, in sistemi operativi precedenti:  
  
     Dal menu **Start** fare clic su **Tutti i programmi**, selezionare **SQL Server 2014**, fare clic con il pulsante destro del mouse su **SQL Server Data Tools**, quindi scegliere **Esegui come amministratore**.  
  
2.  Scegliere **Continua**.  
  
3.  Fare clic su **Esegui programma**.  
  
 Sarà ora possibile distribuire report o altri elementi in un server di report locale.  
  
 **Per configurare proprietà e assegnazioni dei ruoli di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , pertanto, non è necessario avviare SSDT con autorizzazioni elevate tutte le volte:**  
  
-   Vedere le sezioni [Impostazioni cartella Gestione report)](#bkmk_configure_folder_settings) e [Impostazioni sito Gestione report](#bkmk_configure_site_settings) più indietro in questo argomento.  
  
##  <a name="bkmk_addiitonal_informaiton"></a> Informazioni aggiuntive  
 Un passaggio di configurazione aggiuntivo e comune correlato all'amministrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consiste nell'aprire la porta 80 in Windows Firewall per consentire l'accesso al computer del server di report. Per istruzioni, vedere [Configure a Firewall for Report Server Access](configure-a-firewall-for-report-server-access.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire un server di report in modalità nativa di Reporting Services](manage-a-reporting-services-native-mode-report-server.md)  
  
  
