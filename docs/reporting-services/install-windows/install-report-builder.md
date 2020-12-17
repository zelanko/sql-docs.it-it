---
title: Installare Generatore report | Microsoft Docs
description: Generatore report è un'app autonoma, installata nel computer in uso dall'utente o da un amministratore.
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ca0071416491700254047b43056d32fc64ed1d9d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97425130"
---
# <a name="install-report-builder"></a>Installare Generatore report

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] è un'app autonoma, installata nel computer in uso dall'utente o da un amministratore. È possibile installarla dall'Area download Microsoft, da un server di report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] o da un sito di SharePoint integrato con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  

> [!NOTE]
> Se invece si cercano informazioni di installazione per Power BI Report Builder, passare alla pagina [Microsoft Power BI Report Builder](https://www.microsoft.com/download/details.aspx?id=58158) nell'Area download. 

 In genere un amministratore installa e configura [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], concede l'autorizzazione per scaricare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] dal portale Web e gestisce cartelle e autorizzazioni per report, parti del report e set di dati condivisi salvati nel server di report. Per altre informazioni sull'amministrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Server di report di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
## <a name="install-ssrbnoversion-from--a--web-portal-or-sharepoint-library"></a>Installare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] da un portale Web o da una raccolta di SharePoint 

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
  
 È possibile avviare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] da un portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o da un sito di SharePoint integrato con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per informazioni, vedere [Avviare Generatore report](../../reporting-services/report-builder/start-report-builder.md).  

::: moniker range="=sql-server-2016"
  
### <a name="sharepoint-site-integrated-with-ssrsnoversion"></a>Sito di SharePoint integrato con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 In un sito di SharePoint integrato con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], se nel menu **Nuovo documento** non sono elencate le opzioni **Report di Generatore report**, **Modello di Generatore report** e **Origine dati report**, i relativi tipi di contenuto devono essere aggiunti alla raccolta di SharePoint. Per altre informazioni, vedere [Aggiungere i tipi di contenuto di Reporting Services a una raccolta di SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  

::: moniker-end
 
## <a name="install-ssrbnoversion-with-microsoft-endpoint-configuration-manager"></a>Installare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] con Microsoft Endpoint Configuration Manager 
  
 Un amministratore può usare anche un software come Microsoft Endpoint Configuration Manager per installare automaticamente il programma nel computer. Per informazioni sull'uso del software specifico per l'installazione di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], fare riferimento alla relativa documentazione. Per altre informazioni, vedere la [documentazione di Microsoft Endpoint Configuration Manager](/configmgr/).  
  
> [!IMPORTANT]  
>  Le funzionalità di sicurezza di Windows Vista e Windows 7 richiedono autorizzazioni elevate per l'esecuzione delle operazioni dalla riga di comando. L'installazione non è invisibile all'utente. Per renderla invisibile è necessario eseguire la riga di comando come amministratore.  
  
## <a name="system-requirements"></a>Requisiti di sistema
  
 Vedere la sezione **Requisiti di sistema** della [pagina di download di Generatore report](https://go.microsoft.com/fwlink/?LinkID=734968) nell'Area download Microsoft.
  
##  <a name="to-install-ssrbnoversion-from-the-download-site"></a><a name="download"></a> Per installare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] dal sito di download  
  
1.  Nella [pagina Generatore report dell'Area download Microsoft](https://go.microsoft.com/fwlink/?LinkID=734968) fare clic su **Download**.  
  
2.  Dopo aver completato il download di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], fare clic su **Esegui**.  
  
     Verrà avviata la Configurazione guidata di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] per SQL Server.  
  
3.  Accettare i termini del contratto di licenza e fare clic su **Avanti**.  
  
4.  Nella pagina **Server di destinazione predefinito** immettere facoltativamente l'URL del server di report di destinazione se diverso da quello predefinito. Fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  Se si intende usare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] quando è connesso a un server di report, è consigliabile specificare l'URL del server. È tuttavia possibile eseguire questa operazione dalla finestra di dialogo **Opzioni** in [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  
  
5.  Fare clic su **Installa** per completare l'installazione di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  
  
## <a name="to-install-ssrbnoversion-from-a-share"></a>Per installare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] da una condivisione  
  
1.  Per informazioni sul percorso del file ReportBuilder.msi che si esegue per installare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] nel computer locale, rivolgersi all'amministratore.  
  
2.  Individuare il file ReportBuilder.msi, ovvero il pacchetto di Windows Installer (MSI) per [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], e selezionarlo.  
  
     Verrà avviata la Configurazione guidata di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] per SQL Server.  
  
3.  Completare i passaggi restanti di [Per installare Generatore report dal sito di download](#download).  
  
## <a name="to-install-ssrbnoversion-from-the-command-line"></a>Per installare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] dalla riga di comando 

 È anche possibile eseguire un'installazione dalla riga di comando di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] e immettere argomenti per la personalizzazione dell'installazione. Oltre ai parametri intrinseci MSI standard, è possibile usare i parametri personalizzati specifici di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]: RBINSTALLDIR e RBSERVERURL. RBINSTALLDIR specifica la cartella di installazione radice per [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. REPORTSERVERURL specifica il server di report predefinito usato da [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] per salvare i report.  
  
 Se si vuole eseguire un'installazione invisibile all'utente che non richiede interazioni con l'interfaccia utente, specificare l'opzione **/quiet** . In base alle caratteristiche di progettazione, il flag dell'opzione quiet elimina la visualizzazione degli errori di installazione. Quando si usa questa opzione è quindi consigliabile includere l'opzione **/l** che specifica la registrazione.   
  
1.  Nella [pagina Generatore report dell'Area download Microsoft](https://go.microsoft.com/fwlink/?LinkID=734968)fare clic su **Download**.  
  
2.  Dopo aver completato il download di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], fare clic su **Salva**.  
  
3.  Fare clic sul menu **Start** e scegliere **Esegui**.  
  
4.  Nella casella **Apri** digitare **cmd.**  
  
5.  Nella finestra del prompt dei comandi spostarsi sulla cartella in cui è stato salvato il file ReportBuilder.msi.  
  
6.  Digitare un comando con il formato seguente:  
  
     `msiexec/i ReportBuilder.msi OPTION=OptionValue [OPTION=OptionValue]`  
  
     Le due opzioni specifiche dell'installazione di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] sono RBINSTALLDIR e RBSERVERURL. Non è necessario includere questi argomenti nella riga di comando. Di seguito è riportato il comando di base:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  Per eseguire il comando, premere INVIO.  
  
## <a name="set-ssrbnoversion-defaults"></a>Impostare i valori predefiniti di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]  
  
-   Al termine dell'installazione di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], è possibile configurare alcune opzioni predefinite. Fare clic su **File** > **Opzioni**.  
  
     È estremamente utile impostare il portale Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o il sito di SharePoint predefinito. Per altre informazioni, vedere [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md).  
  
-   Fare clic su **Generatore report** .  
  
     Se il server di report non è visibile nell'elenco dei server esistenti, chiudere la finestra di dialogo **Apri report**, quindi fare clic su **Connetti** nella parte inferiore di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] per connettersi al server.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Generatore report](../../reporting-services/report-builder/start-report-builder.md)   
 [Disinstallare Generatore report](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
