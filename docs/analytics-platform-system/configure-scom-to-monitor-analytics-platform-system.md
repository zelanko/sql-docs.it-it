---
title: Configurare SCOM per monitorare il sistema di piattaforma Analitica | Microsoft Docs
description: Seguire questi passaggi per configurare il management pack di System Center Operations Manager (SCOM) per il sistema di piattaforma Analitica. I Management Pack sono necessari per monitorare il sistema di piattaforma Analitica da SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2dae92263d7be76490a51ea7027f79ab5fcd6118
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532575"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Configurare System Center Operations Manager (SCOM) per monitorare il sistema di piattaforma Analitica
Seguire questi passaggi per configurare il Management Pack di System Center Operations Manager (SCOM) per il sistema di piattaforma Analitica. I Management Pack sono necessari per monitorare il sistema di piattaforma Analitica da SCOM.  
  
## <a name="BeforeBegin"></a>Prima di iniziare  
**Prerequisiti**  
  
System Center Operations Manager 2007 R2 deve essere installato e in esecuzione.  
  
I management pack deve essere installato e configurato. Visualizzare [installa i Management Pack SCOM &#40;sistema di piattaforma Analitica&#41; ](install-the-scom-management-packs.md) e [importare il Management Pack SCOM per PDW &#40;il sistema di piattaforma Analitica&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Configurare profilo runas in System Center  
Per configurare System Center, è necessario eseguire la procedura seguente:  
  
-   Creare account RunAs per il **APS Watcher** utente di dominio e mapparlo al **Account Watcher piattaforma di strumenti analitici Microsoft.**  
  
-   Creare account RunAs per il **monitoring_user** utente APS e mapparlo al **Account azione di piattaforma di strumenti analitici Microsoft**.  
  
Di seguito sono istruzioni dettagliate su come eseguire le attività:  
  
1.  Creare il **APS Watcher** account RunAs con **Windows** per tipo di account il **Watcher APS** utente di dominio.  
  
    1.  Passare al **Administration** pulsante destro del mouse sul riquadro **configurazione runas** -> **account** e selezionare **crea Account runas...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  Il **Creazione guidata Account runas** della finestra verrà aperta. Nel **Introduction** pagina, fare clic su **successivo**.  
  
    3.  Nel **delle proprietà generali** pagina, selezionare **Windows** da **tipo Account runas** e specificare "APS Watcher" come il **nome visualizzato**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  Nel **credenziali** pagina ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  Nel **sicurezza della distribuzione** pagina, selezionare **meno sicuro** e fare clic sui **crea** per terminare.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Se si decide di usare la **più sicuro** opzione, è necessario specificare manualmente i computer in cui le credenziali verranno distribuite. A tale scopo, dopo aver creato l'account RunAs, fare doppio clic su di esso e selezionare **proprietà**.  
  
        2.  Passare al **distribuzione** scheda e **Add** computer desiderato.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Impostare il **Account Watcher piattaforma di strumenti analitici Microsoft** profilo da utilizzare **Watcher APS** account RunAs.  
  
    1.  Passare a **Administration** -> **configurazione runas** -> **profili**.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Fare clic con il pulsante destro sul **Account di Microsoft APS Watcher** dall'elenco e selezionare **proprietà**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  Il **guidata profilo runas** della finestra verrà aperta. Ignora la **Introduction** , facendo clic su **successivo**.  
  
    4.  Nel **delle proprietà generali** pagina, fare clic su **successivo**.  
  
    5.  Nel **account RunAs** pagina, fare clic su di **Aggiungi...**  e selezionare creato in precedenza **Watcher APS** account RunAs.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Fare clic su **salvare** per completare l'assegnazione del profilo.  
  
3.  Attendere fino al completamento dell'individuazione di Appliance APS.  
  
    1.  Passare al **Monitoring** riquadro e aprire il **Appliance di SQL Server** -> **sistema di piattaforma Analitica Microsoft**  ->   **Appliance** vista stato.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Attendere che il dispositivo viene visualizzato nell'elenco. Il nome dell'appliance deve essere uguale a quello specificato nel Registro di sistema. Al termine dell'individuazione dovrebbe essere tutte le Appliance elencati, ma non monitorato. Per abilitare il monitoraggio, seguire i passaggi successivi.  
  
    > [!NOTE]  
    > Mentre si è in attesa per l'individuazione iniziale appliance alla fine, è possono eseguire i passaggi successivi in parallelo.  
  
4.  Creare un altro nuovo account RunAs per eseguire query dei punti di accesso per il recupero dei dati di integrità.  
  
    1.  Iniziare a creare un nuovo account RunAs, come descritto nel passaggio 1.  
  
    2.  Nel **delle proprietà generali** pagina, selezionare **l'autenticazione di base** tipo di account.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  Nel **credenziali** pagina, fornire credenziali valide per accedere allo stato di integrità APS viste a gestione dinamica.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Configurare il **Account di azione di piattaforma di strumenti analitici Microsoft** profilo da utilizzare per l'account RunAs appena creato per l'istanza di punti di accesso.  
  
    1.  Passare al **Account di azione di piattaforma di strumenti analitici Microsoft** proprietà come descritto nel passaggio 2.  
  
    2.  Nel **account RunAs** pagina, fare clic su **Aggiungi...**  e 
    3.  Selezionare l'account RunAs appena creato.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>Passaggio successivo  
Ora che è stato configurato il Management Pack, si è pronti per avviare il monitoraggio dell'appliance. Per altre informazioni, vedere [monitorare l'Appliance tramite System Center Operations Manager &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
