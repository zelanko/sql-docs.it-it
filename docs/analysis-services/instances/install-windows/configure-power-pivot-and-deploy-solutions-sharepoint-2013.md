---
title: Configurare PowerPivot e distribuire soluzioni (SharePoint 2013) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 079988eb037ebeffbbbe6cae053e241518e41c81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63054591"
---
# <a name="configure-power-pivot-and-deploy-solutions-sharepoint-2013"></a>Configurare Power Pivot e distribuire soluzioni (SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Questo argomento descrive la distribuzione e la configurazione di miglioramenti di livello intermedio alle funzionalità di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] , tra cui la raccolta [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , la pianificazione dell'aggiornamento dei dati, il dashboard di gestione e i provider di dati. Eseguire lo strumento di **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013** per eseguire queste operazioni:  
  
-   Distribuire i file di soluzione SharePoint.  
  
-   Creare un'applicazione del servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
-   Configurare un'applicazione Excel Services per l'utilizzo di un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint. Per informazioni sui servizi back-end e sull'installazione di un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in modalità SharePoint, vedere [Installazione di Analysis Services in modalità Power Pivot](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 Per informazioni sull'installazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per lo strumento di configurazione di SharePoint 2013, vedere [Installare o disinstallare il componente aggiuntivo Power Pivot per SharePoint &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
##  <a name="bkmk_run_configuration_tool"></a> Eseguire la configurazione di Power Pivot per SharePoint 2013  
 **Nota:** Il [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] installazione guidata vengono installati due strumenti di configurazione diversi per [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]. Ognuno supporta una versione diversa di SharePoint.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013|SharePoint 2013|  
|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Strumento di configurazione|SharePoint 2010 con SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Nota:** Per completare questa procedura, è necessario essere un amministratore della farm. Se viene visualizzato un messaggio di errore simile al seguente,  
  
-   "L'utente non è un amministratore della farm. Risolvere gli errori di convalida e riprovare".  
  
 Effettuare l'accesso con l'account tramite cui è stato installato SharePoint oppure configurare l'account di configurazione come amministratore principale del sito Amministrazione centrale SharePoint.  
  
1.  Scegliere **Tutti i programmi** dal menu **Start**e quindi fare clic su [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi su **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013**. Lo strumento è elencato solo quando [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint è installato nel server locale.  
  
2.  Fare clic su **Configura o ripristina [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint**, quindi scegliere **OK**.  
  
3.  Lo strumento esegue una convalida per verificare lo stato corrente di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e identificare i passaggi necessari per completare la configurazione. Espandere completamente la finestra. Nella parte inferiore della finestra dovrebbe essere disponibile una barra contenente i comandi **Convalida**, **Esegui**ed **Esci** .  
  
4.  Nella scheda **Parametri** :  
  
    1.  **Nome utente Account predefinito**: Immettere un account utente di dominio per l'account predefinito. L'account verrà usato per eseguire il provisioning dei servizi, incluso il pool di applicazioni del servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Non specificare un account predefinito quale Servizio di rete o Sistema locale. Le configurazioni tramite cui vengono specificati account predefiniti vengono bloccate dallo strumento.  
  
    2.  **Server di database**: È possibile usare il motore di Database di SQL Server supportato per la farm di SharePoint.  
  
    3.  **Passphrase**: Immettere una passphrase. Se si crea una nuova farm di SharePoint, la passphrase viene utilizzata ogni volta che si aggiunge un server o un'applicazione alla farm di SharePoint. Se la farm esiste già, immettere la passphrase che consente di aggiungere un'applicazione server alla farm.  
  
    4.  **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Server per Excel Services**: Digitare il nome di un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] server in modalità SharePoint. In una distribuzione a server singolo è uguale al server di database. `[ServerName]\powerpivot`  
  
    5.  Fare clic su **Creare raccolta siti** nella finestra a sinistra. Annotarsi l' **URL sito** in modo che sia possibile utilizzarlo come riferimento nei passaggi successivi. Se il server SharePoint non è ancora configurato, tramite la Configurazione guidata l'applicazione Web e gli URL della raccolta siti vengono impostati in modo predefinito sulla radice di `http://[ServerName]`. Per modificare le impostazioni predefinite, rivedere le pagine seguenti nella finestra a sinistra: **Creare applicazione Web predefinita** e **distribuire la soluzione applicazione Web**  
  
5.  Facoltativamente, rivedere i valori di input rimanenti usati per completare ogni azione. Fare clic su ogni azione nella finestra a sinistra per visualizzare e verificare i dettagli dell'azione. Per altre informazioni su ciascuno di essi, vedere la sezione "valori di Input usati per configurare il server in [configurare o ripristinare Power Pivot per SharePoint 2010 (strumento di configurazione Power Pivot)](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046) in questo argomento.  
  
6.  Facoltativamente, rimuovere eventuali azioni che non si desidera elaborare in questo momento. Ad esempio, se si desidera configurare il servizio di archiviazione sicura in un secondo momento, fare clic su **Configurare il servizio di archiviazione sicura**, quindi deselezionare la casella di controllo **Includere l'azione nell'elenco attività**.  
  
7.  Fare clic su **Convalida** per verificare se sono disponibili informazioni sufficienti per lo strumento al fine di elaborare le azioni nell'elenco. Se si verificano errori di convalida, fare clic sugli avvisi nel riquadro a sinistra per visualizzare i dettagli dell'errore di convalida. Correggere gli eventuali errori di convalida, quindi fare di nuovo clic su **Convalida** .  
  
8.  Fare clic su **Esegui** per elaborare tutte le azioni nell'elenco attività. Si noti che dopo aver convalidato le azioni, il comando **Esegui** diventa disponibile. Se **Esegui** non è abilitato, fare clic su **Convalida** .  
  
 Per altre informazioni, vedere [Configurare o ripristinare Power Pivot per SharePoint 2010 (strumento di configurazione Power Pivot)](http://msdn.microsoft.com/d61f49c5-efaa-4455-98f2-8c293fa50046)  
  
##  <a name="bkmk_verify_powerpivot"></a> Verificare la configurazione di Power Pivot  
 **Servizi:**  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci servizi nel server**.  
  
2.  Verificare che **SQL Server Analysis Services** e **Servizio di sistema [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] di SQL Server** siano avviati.  
  
 **Funzionalità della farm:**  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci funzionalità farm**.  
  
2.  Verificare che la **Funzionalità di integrazione[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]** sia **Attiva**.  
  
 **Funzionalità della raccolta siti:**  
  
1.  Selezionare l'URL del sito creato tramite lo strumento di configurazione.  
  
     Fare clic su **le impostazioni**![impostazioni di SharePoint](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "impostazioni di SharePoint"), quindi fare clic su **Impostazioni sito**.  
  
     Fare clic su **Funzionalità raccolta siti**.  
  
2.  Verificare che l' **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per le raccolte siti** sia **attiva**.  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] :**  
  
1.  In **Gestione applicazioni**di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Verificare che lo stato dell'applicazione di servizio sia **Avviato**. Il nome predefinito è **Applicazione del servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] predefinita**.  
  
     Fare clic sul nome dell'applicazione di servizio per aprire il dashboard di gestione [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] da cui è possibile aprire l'applicazione del servizio. Al primo utilizzo, il dashboard potrebbe impiegare diversi minuti per il caricamento.  
  
 Per altre informazioni, vedere [Verify a Power Pivot for SharePoint Installation](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_troubleshoot_issues"></a> Risolvere eventuali problemi  
 Per ricevere assistenza durante la risoluzione dei problemi, è consigliabile verificare che la registrazione diagnostica sia abilitata.  
  
1.  In Amministrazione centrale SharePoint fare clic su **Monitoraggio** , quindi selezionare **Configura raccolta dati di utilizzo e integrità**.  
  
2.  Verificare che l'opzione **Abilita raccolta dati di utilizzo** sia selezionata.  
  
3.  Verificare che gli eventi seguenti siano selezionati:  
  
    -   Definizione dei campi di utilizzo per la telemetria del settore formativo  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] - Connessioni  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] - Utilizzo dati di caricamento  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Utilizzo query  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Utilizzo dati di scaricamento  
  
4.  Verificare che l'opzione **Abilita raccolta dati integrità** sia selezionata.  
  
5.  Fare clic su **OK**.  
  
 Per altre informazioni sull'aggiornamento dei dati di risoluzione dei problemi, vedere [risoluzione dei problemi di aggiornamento dati Power Pivot](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 Per altre informazioni sullo strumento di configurazione, vedere [Strumenti di configurazione di Power Pivot](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  
