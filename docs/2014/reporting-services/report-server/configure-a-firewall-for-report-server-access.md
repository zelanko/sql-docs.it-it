---
title: Configurare un firewall per l'accesso al server di report | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [Reporting Services]
- configuring servers [Reporting Services]
ms.assetid: 04dae07a-a3a4-424c-9bcb-a8000e20dc93
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0f7016d47d060fa5f6708f907da848d7329482d4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024712"
---
# <a name="configure-a-firewall-for-report-server-access"></a>Configurare un firewall per l'accesso al server di report
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Alle applicazioni del server di report e ai report pubblicati si accede tramite URL che specificano un indirizzo IP, una porta e una directory virtuale. Se Windows Firewall è abilitato, la porta configurata per l'utilizzo da parte del server di report è probabilmente chiusa. Il fatto che una porta possa essere chiusa viene indicato dalla visualizzazione di una pagina Web vuota in seguito alla richiesta di un report o dalla visualizzazione di una pagina vuota quando si tenta di aprire Gestione report da un computer client remoto.  
  
 Per aprire una porta, è necessario utilizzare l'utilità Windows Firewall nel computer server di report. Poiché le porte non verranno aperte automaticamente da Reporting Services, è necessario eseguire questa operazione manualmente.  
  
 Per impostazione predefinita, il server di report è in attesa delle richieste HTTP sulla porta 80. Di conseguenza, le indicazioni seguenti includono passaggi in cui viene specificata tale porta. Se gli URL del server di report sono stati configurati per l'utilizzo di una porta diversa, è necessario specificare questo numero di porta quando si utilizzano le indicazioni fornite di seguito.  
  
 Se si accede ai database relazionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in computer esterni o se il database del server di report si trova in un'istanza esterna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario aprire le porte 1433 e 1434 nel computer esterno. Per altre informazioni, vedere [Configurare Windows Firewall per l'accesso al motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni sulle impostazioni predefinite di Windows Firewall e per una descrizione delle porte TCP che interessano [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="prerequisites"></a>Prerequisiti  
 In queste indicazioni si presuppone che sia già stato configurato l'account del servizio, sia già stato creato il database del server di report e che siano già stati configurati gli URL per il servizio Web ReportServer e per Gestione report. Per altre informazioni, vedere [Gestire un server di report in modalità nativa di Reporting Services](manage-a-reporting-services-native-mode-report-server.md).  
  
 È inoltre necessario avere verificato la possibilità di accedere al server di report tramite una connessione del browser all'istanza locale del server di report. Questo passaggio consente di stabilire che si dispone di un'installazione funzionante. Prima di procedere all'apertura delle porte, è necessario verificare la corretta configurazione dell'installazione. Per completare questo passaggio in Windows Server, è inoltre necessario avere aggiunto il server di report all'area dei siti attendibili. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="opening-ports-in-windows-firewall"></a>Apertura di porte in Windows Firewall  
 A seconda della versione di Windows Firewall in uso, è necessario seguire indicazioni distinte.  
  
#### <a name="to-open-port-80-on-windows-7-windows-server-2008-r2-windows-server-2012-and-2012-r2"></a>Per aprire la porta 80 in Windows 7, Windows Server 2008 R2 o Windows Server 2012 e 2012 R2  
  
1.  Fare clic sul menu **Start** , scegliere **Pannello di controllo**, **Sistema e sicurezza**e quindi **Windows Firewall**. Il Pannello di controllo non è configurato per la visualizzazione per 'Categorie': è sufficiente selezionare **Windows Firewall**.  
  
2.  Fare clic su **Impostazioni avanzate**.  
  
3.  Fare clic su **Regole connessioni in entrata**.  
  
4.  Fare clic su **Nuova regola** nella finestra **Azioni****.**  
  
5.  Fare clic su **Tipo di regola** in **Porta**.  
  
6.  Scegliere **Avanti**.  
  
7.  Nella pagina **Protocollo e porte** selezionare **TCP**.  
  
8.  Selezionare **Porte locali specifiche** e digitare il valore **80**.  
  
9. Scegliere **Avanti**.  
  
10. Nella pagina **Azione** fare clic su **Consenti la connessione**.  
  
11. Scegliere **Avanti**.  
  
12. Nella pagina **Profilo** fare clic sulle opzioni appropriate per l'ambiente.  
  
13. Scegliere **Avanti**.  
  
14. Nella pagina **Nome** immettere un nome di**ReportServer (TCP sulla porta 80)**  
  
15. Scegliere **Fine**.  
  
16. Riavviare il computer.  
  
#### <a name="to-open-port-80-on-windows-vista-or-windows-server-2008"></a>Per aprire la porta 80 in Windows Vista o Windows Server 2008  
  
1.  Dal **avviare** menu, fare clic su **Pannello di controllo**, fare clic su **sicurezza**e quindi fare clic su **Windows Firewall**.  
  
2.  Fare clic su **consentire a un programma attraverso Windows Firewall**.  
  
3.  Scegliere **Continua**.  
  
4.  Nella scheda eccezioni, fare clic su **Aggiungi porta**.  
  
5.  In nome digitare **ReportServer (TCP sulla porta 80)**.  
  
6.  Nel numero di porta, digitare **80**.  
  
7.  Verificare che **TCP** sia selezionata.  
  
8.  Fare clic su **Cambia ambito**.  
  
9. Fare clic su **solo la rete (subnet) locale**, quindi fare clic su **OK**.  
  
10. Scegliere **OK** per chiudere la finestra di dialogo.  
  
11. Riavviare il computer.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Dopo avere aperto la porta e prima di verificare che gli utenti remoti possano accedere al server di report sulla porta aperta, è necessario concedere accesso utente al server di report tramite assegnazioni di ruolo in Home e a livello di sito. Pur aprendo correttamente una porta, è possibile che le connessioni del server di report non vengano effettuate se gli utenti non dispongono di autorizzazioni sufficienti. Per altre informazioni, vedere [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](../security/grant-user-access-to-a-report-server.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È inoltre possibile verificare che la porta sia aperta correttamente avviando Gestione report in un computer diverso. Per altre informazioni, vedere [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Creare un database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Gestire un server di report in modalità nativa di Reporting Services](manage-a-reporting-services-native-mode-report-server.md)  
  
  
