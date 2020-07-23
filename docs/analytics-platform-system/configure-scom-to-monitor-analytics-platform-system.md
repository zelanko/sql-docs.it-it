---
title: Configurare System Center Operations Manager per il monitoraggio di APS
description: Attenersi alla seguente procedura per configurare i Management Pack System Center Operations Manager (SCOM) per il sistema di piattaforma di analisi. I Management Pack sono necessari per monitorare il sistema di piattaforma di analisi da SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 0786cbc8230ecf29dd377a35fefc6969072512b3
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942213"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Configurare System Center Operations Manager (SCOM) per monitorare il sistema della piattaforma di analisi
Attenersi alla seguente procedura per configurare i Management Pack System Center Operations Manager (SCOM) per il sistema di piattaforma di analisi. I Management Pack sono necessari per monitorare il sistema di piattaforma di analisi da SCOM.  
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>Prima di iniziare  
**Prerequisiti**  
  
System Center Operations Manager 2007 R2 deve essere installato e in esecuzione.  
  
I Management Pack devono essere installati e configurati. Vedere [Install the SCOM management packs &#40;Analytics Platform system&#41;](install-the-scom-management-packs.md) e [importare il Management Pack di SCOM per PDW &#40;analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="configure-run-as-profile-in-system-center"></a><a name="ConfigureRunAsProfile"></a>Configurare il profilo RunAs in System Center  
Per configurare System Center, è necessario eseguire le operazioni seguenti:  
  
-   Creare un account RunAs per l'utente di dominio **APS Watcher** ed eseguirne il mapping all' **account Microsoft APS Watcher.**  
  
-   Creare un account RunAs per l'utente di **monitoring_user** APS ed eseguirne il mapping all' **account azione Microsoft APS**.  
  
Di seguito sono riportate istruzioni dettagliate su come eseguire le attività:  
  
1.  Creare l'account RunAs del controllo **APS** con il tipo di account di **Windows** per l'utente di dominio **APS Watcher** .  
  
    1.  Passare al riquadro **Amministrazione** , fare clic con il pulsante destro del mouse su account di **Configurazione RunAs**  ->  **Accounts** e selezionare **Crea account RunAs.**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  Verrà visualizzata la finestra di dialogo Creazione **guidata account RunAs** . Nella pagina **Introduzione** fare clic su **Avanti**.  
  
    3.  Nella pagina delle **proprietà generale** selezionare **Windows** dal **tipo di account RunAs** e specificare "APS Watcher" come **nome visualizzato**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  Nella pagina **credenziali** , ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  Nella pagina **sicurezza distribuzione** selezionare **meno sicuro** e fare clic sul pulsante **Crea** per terminare.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Se si decide di utilizzare l'opzione **più sicura** , è necessario specificare manualmente i computer a cui verranno distribuite le credenziali. A tale scopo, dopo aver creato l'account RunAs, fare clic con il pulsante destro del mouse su di esso e scegliere **Proprietà**.  
  
        2.  Passare alla scheda **distribuzione** e **aggiungere** i computer desiderati.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Impostare il profilo dell' **account Microsoft APS Watcher** per l'uso dell'account RunAs del controllo **APS** .  
  
    1.  Passare ad **Amministrazione**  ->  **Esegui come profili di configurazione**  ->  **Profiles**.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Fare clic con il pulsante destro del mouse sull' **account Microsoft APS Watcher** dall'elenco e scegliere **Proprietà**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  Verrà visualizzata la finestra **di dialogo Creazione guidata profilo RunAs** . Fare clic su **Avanti**per ignorare la pagina **introduttiva** .  
  
    4.  Nella pagina **Proprietà generali** , scegliere **Avanti**.  
  
    5.  Nella pagina **account RunAs** fare clic sul pulsante **Aggiungi...** e selezionare l'account RunAs del controllo **APS** creato in precedenza.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Fare clic su **Salva** per completare l'assegnazione del profilo.  
  
3.  Attendere il completamento dell'individuazione degli appliance APS.  
  
    1.  Passare al riquadro **monitoraggio** e aprire il **SQL Server Appliance**  ->  **piattaforma di strumenti analitici Microsoft**  ->  visualizzazione stato**Appliance** .  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Attendere che l'appliance venga visualizzata nell'elenco. Il nome dell'appliance deve essere uguale a uno specificato nel registro di sistema. Al termine dell'individuazione, verranno visualizzati tutti i dispositivi elencati ma non monitorati. Per abilitare il monitoraggio, attenersi alla procedura successiva.  
  
    > [!NOTE]  
    > I passaggi successivi possono essere completati in parallelo mentre si è in attesa del completamento dell'individuazione dell'appliance iniziale.  
  
4.  Creare un altro nuovo account RunAs per eseguire query su APS per il recupero dei dati di integrità.  
  
    1.  Iniziare a creare un nuovo account RunAs come descritto nel passaggio 1.  
  
    2.  Nella pagina delle **proprietà generale** selezionare tipo di account **autenticazione di base** .  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  Nella pagina **credenziali** specificare credenziali valide per accedere allo stato di integrità di APS DMV.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Configurare il profilo dell' **account azione APS Microsoft** per usare l'account RunAs appena creato per l'istanza di APS.  
  
    1.  Passare alle proprietà dell' **account azione di Microsoft APS** come descritto nel passaggio 2.  
  
    2.  Nella pagina **account RunAs** fare clic su **Aggiungi...** e 
    3.  Selezionare l'account RunAs appena creato.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>passaggio successivo  
Ora che sono stati configurati i Management Pack, si è pronti per avviare il monitoraggio dell'appliance. Per altre informazioni, vedere [monitorare l'appliance usando System Center Operations Manager&#41;di sistema della piattaforma &#40;Analytics ](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
