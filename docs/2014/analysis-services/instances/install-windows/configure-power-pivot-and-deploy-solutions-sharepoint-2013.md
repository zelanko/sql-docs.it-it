---
title: Configurare PowerPivot e distribuire soluzioni (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96b7798dcacc69b1de233b330b053b2d9a2bd776
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370083"
---
# <a name="configure-powerpivot-and-deploy-solutions-sharepoint-2013"></a>Configurare PowerPivot e distribuire soluzioni (SharePoint 2013)
  In questo argomento vengono descritte la distribuzione e la configurazione di miglioramenti di livello intermedio alle funzionalità di PowerPivot in [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] , tra cui la raccolta PowerPivot, la pianificazione dell'aggiornamento dati, il dashboard di gestione e i provider di dati. Eseguire lo strumento di **configurazione di PowerPivot per SharePoint 2013** per completare le operazioni seguenti:  
  
-   Distribuire i file di soluzione SharePoint.  
  
-   Creare un'applicazione del servizio PowerPivot.  
  
-   Configurare un'applicazione Excel Services per l'utilizzo di un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Per informazioni sui servizi back-end e l'installazione di un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] server in modalità SharePoint, vedere [PowerPivot per SharePoint 2013 Installation](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 Per informazioni sull'installazione di PowerPivot per SharePoint 2013, vedere [installare o disinstallare PowerPivot per SharePoint Add-in &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Esecuzione di PowerPivot per SharePoint 2013](#bkmk_run_configuration_tool)  
  
 [Verificare la configurazione di PowerPivot](#bkmk_verify_powerpivot)  
  
 [Risolvere eventuali problemi](#bkmk_troubleshoot_issues)  
  
##  <a name="bkmk_run_configuration_tool"></a> Esecuzione di PowerPivot per SharePoint 2013  
 **Nota:** Il [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] installazione guidata vengono installati due strumenti di configurazione diversi per [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]. Ognuno supporta una versione diversa di SharePoint.  
  
|nome|Descrizione|  
|----------|-----------------|  
|configurazione di PowerPivot per SharePoint 2013|SharePoint 2013|  
|Strumento di configurazione PowerPivot|SharePoint 2010 con SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Nota:** Per completare questa procedura, è necessario essere un amministratore della farm. Se viene visualizzato un messaggio di errore simile al seguente,  
  
-   "L'utente non è un amministratore della farm. Risolvere gli errori di convalida e riprovare".  
  
 Effettuare l'accesso con l'account tramite cui è stato installato SharePoint oppure configurare l'account di configurazione come amministratore principale del sito Amministrazione centrale SharePoint.  
  
1.  Nel menu **Start** fare clic su **Tutti i programmi**, quindi scegliere [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e, successivamente, selezionare **Configurazione di PowerPivot per SharePoint 2013**. Lo strumento viene elencato solo quando PowerPivot per SharePoint è installato nel server locale.  
  
2.  Fare clic su **Configura o ripristina PowerPivot per SharePoint** , quindi scegliere **OK**.  
  
3.  Tramite lo strumento viene eseguita una convalida per verificare lo stato corrente di PowerPivot e i passaggi necessari per completare la configurazione. Espandere completamente la finestra. Nella parte inferiore della finestra dovrebbe essere disponibile una barra contenente i comandi **Convalida**, **Esegui**ed **Esci** .  
  
4.  Nella scheda **Parametri** :  
  
    1.  **Nome utente Account predefinito**: Immettere un account utente di dominio per l'account predefinito. L'account verrà utilizzato per eseguire il provisioning dei servizi, incluso il pool di applicazioni del servizio PowerPivot. Non specificare un account predefinito quale Servizio di rete o Sistema locale. Le configurazioni tramite cui vengono specificati account predefiniti vengono bloccate dallo strumento.  
  
    2.  **Server di database**: È possibile usare il motore di Database di SQL Server supportato per la farm di SharePoint.  
  
    3.  **Passphrase**: Immettere una passphrase. Se si crea una nuova farm di SharePoint, la passphrase viene utilizzata ogni volta che si aggiunge un server o un'applicazione alla farm di SharePoint. Se la farm esiste già, immettere la passphrase che consente di aggiungere un'applicazione server alla farm.  
  
    4.  **Server PowerPivot per Excel Services**: Digitare il nome di un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] server in modalità SharePoint. In una distribuzione a server singolo è uguale al server di database. `[ServerName]\powerpivot`  
  
    5.  Fare clic su **Creare raccolta siti** nella finestra a sinistra. Annotarsi l' **URL sito** in modo che sia possibile utilizzarlo come riferimento nei passaggi successivi. Se il server SharePoint non è ancora configurato, tramite la Configurazione guidata l'applicazione Web e gli URL della raccolta siti vengono impostati in modo predefinito sulla radice di `http://[ServerName]`. Per modificare le impostazioni predefinite, rivedere le pagine seguenti nella finestra a sinistra: **Creare applicazione Web predefinita** e **distribuire la soluzione applicazione Web**  
  
5.  Facoltativamente, rivedere i valori di input rimanenti usati per completare ogni azione. Fare clic su ogni azione nella finestra a sinistra per visualizzare e verificare i dettagli dell'azione. Per altre informazioni su ciascuno di essi, vedere la sezione "valori di Input usati per configurare il server in [Configura o Ripristina PowerPivot per SharePoint 2010 &#40;PowerPivot Configuration Tool&#41; ](../../../analysis-services/configure-repair-powerpivot-sharepoint-2010.md) India la presente argomento.  
  
6.  Facoltativamente, rimuovere eventuali azioni che non si desidera elaborare in questo momento. Ad esempio, se si desidera configurare il servizio di archiviazione sicura in un secondo momento, fare clic su **Configurare il servizio di archiviazione sicura**, quindi deselezionare la casella di controllo **Includere l'azione nell'elenco attività**.  
  
7.  Fare clic su **Convalida** per verificare se sono disponibili informazioni sufficienti per lo strumento al fine di elaborare le azioni nell'elenco. Se si verificano errori di convalida, fare clic sugli avvisi nel riquadro a sinistra per visualizzare i dettagli dell'errore di convalida. Correggere gli eventuali errori di convalida, quindi fare di nuovo clic su **Convalida** .  
  
8.  Fare clic su **Esegui** per elaborare tutte le azioni nell'elenco attività. Si noti che dopo aver convalidato le azioni, il comando **Esegui** diventa disponibile. Se **Esegui** non è abilitato, fare clic su **Convalida** .  
  
 Per altre informazioni, vedere [Configura o Ripristina PowerPivot per SharePoint 2010 &#40;strumento di configurazione PowerPivot&#41;](../../../analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
##  <a name="bkmk_verify_powerpivot"></a> Verificare la configurazione di PowerPivot  
 **Servizi:**  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci servizi nel server**.  
  
2.  Verificare che **SQL Server Analysis Services** e **Servizio di sistema PowerPivot di SQL Server** siano avviati.  
  
 **Funzionalità della farm:**  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci funzionalità farm**.  
  
2.  Verificare che **Funzionalità integrazione PowerPivot** sia **Attiva**.  
  
 **Funzionalità della raccolta siti:**  
  
1.  Selezionare l'URL del sito creato tramite lo strumento di configurazione.  
  
     Fare clic su **le impostazioni**![impostazioni di SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "impostazioni di SharePoint"), quindi fare clic su **Impostazioni sito**.  
  
     Fare clic su **Funzionalità raccolta siti**.  
  
2.  Verificare che **Integrazione delle funzionalità di PowerPivot per le raccolte siti** sia **Attiva**.  
  
 **Applicazione di servizio PowerPivot:**  
  
1.  In **Gestione applicazioni**di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Verificare che lo stato dell'applicazione di servizio sia **Avviato**. Il nome predefinito è **Applicazione di servizio PowerPivot predefinita**.  
  
     Fare clic sul nome dell'applicazione di servizio per aprire il dashboard di gestione PowerPivot da cui è possibile visualizzare l'applicazione di servizio. Al primo utilizzo, il dashboard potrebbe impiegare diversi minuti per il caricamento.  
  
 Per altre informazioni, vedere [Verify a PowerPivot for SharePoint Installation](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_troubleshoot_issues"></a> Risolvere eventuali problemi  
 Per ricevere assistenza durante la risoluzione dei problemi, è consigliabile verificare che la registrazione diagnostica sia abilitata.  
  
1.  In Amministrazione centrale SharePoint fare clic su **Monitoraggio** , quindi selezionare **Configura raccolta dati di utilizzo e integrità**.  
  
2.  Verificare che l'opzione **Abilita raccolta dati di utilizzo** sia selezionata.  
  
3.  Verificare che gli eventi seguenti siano selezionati:  
  
    -   Definizione dei campi di utilizzo per la telemetria del settore formativo  
  
    -   Connessioni di PowerPivot  
  
    -   Utilizzo dati di caricamento di PowerPivot  
  
    -   Utilizzo query PowerPivot  
  
    -   Utilizzo dati di scaricamento di PowerPivot  
  
4.  Verificare che l'opzione **Abilita raccolta dati integrità** sia selezionata.  
  
5.  Fare clic su **OK**.  
  
 Per altre informazioni sull'aggiornamento dei dati di risoluzione dei problemi, vedere [risoluzione dei problemi di aggiornamento dati PowerPivot](https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 Per ulteriori informazioni sullo strumento di configurazione, vedere [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  
