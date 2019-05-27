---
title: Configurare un server di report per l'amministrazione remota | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- WMI provider [Reporting Services], remote configuration
- configuration management [WMI]
- report servers [Reporting Services], configuring
- remote server administration [Reporting Services]
ms.assetid: 8c7f145f-3ac2-4203-8cd6-2a4694395d09
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e83f539e1ffad77a337fc3e0142379da2ff0f703
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104100"
---
# <a name="configure-a-report-server-for-remote-administration"></a>Configurare un server di report per l'amministrazione remota
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]è possibile configurare istanze del server di report in modalità locale o remota. Per configurare un'istanza remota del server di report, è possibile usare lo strumento di configurazione di Reporting Services oppure scrivere codice personalizzato che usi il provider WMI (Windows Management Instrumentation) per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Lo strumento Gestione configurazione Reporting Services offre un'interfaccia grafica al provider WMI, per consentire di configurare un server di report senza dover scrivere codice. Quando si avvia lo strumento, è possibile specificare un server remoto a cui connettersi.  
  
 Prima che sia possibile utilizzare lo strumento per configurare un server di report remoto, è necessario seguire le indicazioni contenute in questo argomento per abilitare le porte in Windows Firewall, consentire le connessioni remote e abilitare le richieste WMI remote.  
  
 Una configurazione appropriata consente di evitare l'errore seguente:  
  
 `The machine could not be found.`  
  
 `"The RPC server is unavailable. (Exception from HRESULT: 0x800706BA)".`  
  
## <a name="prerequisites"></a>Prerequisiti  
 A tale scopo, è necessario accedere al sistema localmente ed essere membri del gruppo Administrators locale. Non è possibile modificare le impostazioni di Windows Firewall di un computer remoto tramite una connessione remota.  
  
 Se si desidera abilitare l'amministrazione remota per un utente non amministratore, è necessario concedere all'account le autorizzazioni per l'attivazione remota DCOM (Distributed Component Object Model). In questo argomento vengono fornite le istruzioni per la configurazione del server per l'accesso da parte di utenti non amministratori.  
  
 In alcune organizzazioni sono presenti criteri di gruppo che impediscono l'amministrazione remota del server per alcuni sistemi operativi o utenti. Prima di iniziare a modificare le impostazioni del firewall, rivolgersi all'amministratore di rete per verificare se vi sono limitazioni all'amministrazione remota.  
  
 Per ulteriori informazioni, vedere [Connecting Through Windows Firewall](https://go.microsoft.com/fwlink/?LinkId=63615) nella documentazione di Platform SDK nel sito Web MSDN.  
  
## <a name="tasks"></a>Attività  
 Tra le attività che consentono di configurare un server di report remoto sono incluse le seguenti:  
  
-   Abilitare le porte in Windows Firewall per consentire le richieste sulle porte utilizzate dal server di report e dall'istanza del Motore di database di SQL Server.  
  
-   Consentire le connessioni remote all'istanza del Motore di database che ospita il database del server di report. Una connessione remota è necessaria per la configurazione della connessione al database del server di report e per la gestione delle chiavi di crittografia.  
  
-   Consentire il passaggio delle richieste WMI remote attraverso [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Firewall.  
  
-   Se si configura un server di report remoto per l'amministrazione da parte di un utente non amministratore, è necessario impostare autorizzazioni DCOM per consentire l'accesso WMI remoto a un account utente di Windows standard. Poiché WMI utilizza DCOM per il trasporto delle chiamate remote, è necessario impostare le autorizzazioni DCOM per consentire agli utenti che non hanno eseguito l'accesso come amministratore locale di configurare il server.  
  
-   Se si configura un server di report remoto per l'amministrazione da parte di un utente non amministratore, è inoltre necessario impostare autorizzazioni WMI nello spazio dei nomi WMI del server di report. Per impostazione predefinita, tutti i membri del gruppo Administrators locale dispongono di accesso allo spazio dei nomi WMI del server di report. Per concedere l'accesso a utenti non amministratori, è necessario impostare le autorizzazioni.  
  
 Le indicazioni per l'esecuzione di queste attività sono disponibili in questo argomento.  
  
### <a name="to-open-ports-in-windows-firewall"></a>Per aprire porte in Windows Firewall  
  
1.  [Configurare un Firewall di Windows per l'accesso al motore di Database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
2.  [Configure a Firewall for Report Server Access](configure-a-firewall-for-report-server-access.md).  
  
### <a name="to-configure-remote-connections-to-the-report-server-database"></a>Per configurare connessioni remote al database del server di report  
  
1.  Fare clic sul pulsante **Start**, scegliere **Programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**, quindi **Gestione configurazione SQL Server**.  
  
2.  Nel riquadro a sinistra espandere **Configurazione di rete SQL Server**, quindi fare clic su **Protocolli** per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Nel riquadro dei dettagli abilitare i protocolli TCP/IP e Named Pipes, quindi riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-enable-remote-administration-in-windows-firewall"></a>Per abilitare l'amministrazione remota in Windows Firewall  
  
1.  Accedere come amministratore locale al computer per il quale si desidera abilitare l'amministrazione remota.  
  
2.  Se il server di report è in esecuzione in Windows Vista, fare clic con il pulsante destro del mouse su **Prompt dei comandi** , quindi scegliere **Esegui come amministratore**. Per gli altri sistemi operativi, aprire una finestra del prompt dei comandi.  
  
3.  Eseguire il comando seguente:  
  
    ```  
    netsh.exe firewall set service type=REMOTEADMIN mode=ENABLE scope=ALL  
    ```  
  
     È possibile specificare opzioni diverse per Scope. Per ulteriori informazioni, vedere la documentazione di Windows Firewall.  
  
4.  Verificare che l'amministrazione remota sia abilitata. Per visualizzare lo stato, è possibile eseguire il comando seguente:  
  
    ```  
    netsh.exe firewall show state  
    ```  
  
5.  Riavviare il computer.  
  
### <a name="to-set-dcom-permissions-to-enable-remote-wmi-access-for-non-administrators"></a>Per impostare autorizzazioni DCOM per consentire l'accesso WMI remoto a utenti non amministratori  
  
1.  Nel menu Start, scegliere **Strumenti di amministrazione**e quindi **Servizi componenti**.  
  
     Per Windows Vista, nel menu Start, scegliere **tutti i programmi**, fare clic su **eseguito**, quindi immettere `mmc comexp.msc`.  
  
2.  Aprire la cartella Component Services.  
  
3.  Aprire la cartella Computer.  
  
4.  Selezionare Risorse del computer.  
  
5.  Scegliere **Proprietà** dal menu **Azione**.  
  
6.  Fare clic su **Sicurezza COM**.  
  
7.  In **Autorizzazioni di esecuzione e attivazione**fare clic su **Modifica limiti**.  
  
8.  Se il proprio nome non è visualizzato in **Autorizzazioni di avvio**fare clic su **Aggiungi**.  
  
9. Digitare il nome del proprio account utente e quindi fare clic su **OK**.  
  
10. In **Autorizzazioni per \<Utente o Gruppo>** nella colonna **Consenti** selezionare **Avvio remoto** e **Attivazione remota** e quindi fare clic su **OK**.  
  
### <a name="to-set-permissions-on-the-report-server-wmi-namespace-for-non-administrators"></a>Per impostare autorizzazioni nello spazio dei nomi WMI del server di report per utenti non amministratori  
  
1.  Nel menu Start, scegliere **Strumenti di amministrazione**e quindi **Gestione computer**.  
  
2.  Aprire la cartella Servizi e applicazioni.  
  
3.  Fare clic con il pulsante destro del mouse su **Controllo WMI**e scegliere **Proprietà**.  
  
4.  Fare clic su **Sicurezza**.  
  
5.  Aprire la cartella Root.  
  
6.  Aprire la cartella Microsoft.  
  
7.  Aprire la cartella SQLServer.  
  
8.  Aprire la cartella ReportServer.  
  
9. Aprire la cartella dell'istanza. Se è stata installata l'istanza predefinita, il nome della cartella è MSSQLSERVER.  
  
10. Aprire la cartella v10.  
  
11. Selezionare la cartella Admin e quindi fare clic su **Sicurezza**.  
  
12. Fare clic su **Aggiungi**e quindi digitare l'account utente che si desidera utilizzare per gestire il server.  
  
13. Nella colonna **Consenti** selezionare **Abilita account**, **Abilita remoto**e **Sicurezza da lettura**, quindi scegliere **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
