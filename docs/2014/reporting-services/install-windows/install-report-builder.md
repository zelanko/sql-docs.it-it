---
title: Installare la versione autonoma di Generatore report (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 60a96db6a7568c2af22242f10f96e7a2abf13937
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637839"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>Installare la versione autonoma di Generatore report (Generatore report)
  È possibile installare Generatore report dalla [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack nell' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53613) o in un percorso, ad esempio cartella pubblica in cui è stato scaricato il file ReportBuilder3_x86. msi, il pacchetto Windows Installer per Generatore report.  
  
 È inoltre possibile eseguire un'installazione dalla riga di comando di Generatore report e immettere argomenti per la personalizzazione dell'installazione. Oltre ai parametri intrinseci MSI standard, è possibile utilizzare i parametri personalizzati specifici di Generatore report: RBINSTALLDIR e REPORTSERVERURL. RBINSTALLDIR specifica la cartella di installazione radice per Generatore report. REPORTSERVERURL specifica il server di report predefinito utilizzato da Generatore report per salvare i report.  
  
 Se si vuole eseguire un'installazione invisibile all'utente che non richiede interazioni con l'interfaccia utente, specificare l'opzione **/quiet** . In base alle caratteristiche di progettazione, il flag dell'opzione quiet elimina la visualizzazione degli errori di installazione. Quando si usa questa opzione è quindi consigliabile includere l'opzione **/l** che specifica la registrazione.  
  
> [!IMPORTANT]  
>  Le funzionalità di sicurezza di Windows Vista e Windows 7 richiedono autorizzazioni elevate per l'esecuzione delle operazioni dalla riga di comando. L'installazione non è invisibile all'utente. Per renderla invisibile è necessario eseguire la riga di comando come amministratore.  
  
### <a name="to-install-report-builder-from-the-download-site"></a>Per installare Generatore report dal sito di download  
  
1.  Passare a [Microsoft SQL Server 2012 Generatore report](https://go.microsoft.com/fwlink/?LinkID=219138) e individuare la sezione Generatore report della pagina Web.  
  
2.  Fare clic su **pacchetto x86**.  
  
3.  Nella finestra di dialogo **download del file** fare clic su **Esegui**.  
  
    > [!IMPORTANT]  
    >  Scaricare file solo da fonti attendibili.  
  
4.  Nella finestra di dialogo Internet Explorer fare clic su **Esegui**.  
  
    > [!IMPORTANT]  
    >  Eseguire file solo da fonti attendibili.  
  
5.  Verrà avviata la procedura di installazione guidata di Generatore report per Microsoft SQL Server.  
  
6.  Nella pagina **iniziale dell'installazione guidata** fare clic su **Avanti**.  
  
7.  Nella pagina **contratto di licenza** leggere il contratto e quindi selezionare l'opzione **Accetto i termini del contratto di licenza** . Scegliere **Avanti**.  
  
8.  Digitare il proprio nome e il nome della società. Scegliere **Avanti**.  
  
9. Nella pagina **Selezione funzionalità** fare clic facoltativamente su **Sfoglia** o su **costo del disco**. Scegliere **Avanti**.  
  
    -   Fare clic su **Sfoglia** per visualizzare il percorso predefinito di Generatore report e aggiornarlo.  
  
        > [!NOTE]  
        >  La cartella di installazione predefinita per Generatore report è \<unità > Programmi\Microsoft SQL Server.  
  
    -   Fare clic su **costo disco** per conoscere la quantità di spazio su disco utilizzata da Generatore report.  
  
        > [!NOTE]  
        >  Se la quantità di spazio libero su disco disponibile in un volume non è sufficiente, questo volume viene evidenziato.  
  
10. Nella pagina **Server di destinazione predefinito** immettere facoltativamente l'URL del server di report di destinazione se diverso da quello predefinito. Scegliere **Avanti**.  
  
    > [!NOTE]  
    >  Se si intende utilizzare Generatore report quando è connesso a un server di report, è consigliabile specificare l'URL del server. Tuttavia, è possibile eseguire questa operazione anche dalla finestra di dialogo **Opzioni** quando si lavora in Generatore report.  
  
11. Fare clic su **Installa** per completare l'installazione di Generatore report.  
  
### <a name="to-install-report-builder-from-a-share"></a>Per installare Generatore report da una condivisione  
  
1.  Per informazioni sul percorso del file ReportBuilder3_x86.msi.msi che si esegue per installare Generatore report nel computer locale, rivolgersi all'amministratore.  
  
2.  Individuare il file ReportBuilder3_x86.msi.msi, ovvero il pacchetto di Windows Installer (MSI) per Generatore report, e fare clic su di esso.  
  
     Verrà avviata la procedura di installazione guidata di Generatore report per Microsoft SQL Server.  
  
3.  Nella pagina **iniziale dell'installazione guidata** fare clic su **Avanti**.  
  
4.  Nella pagina **contratto di licenza** leggere il contratto e quindi selezionare l'opzione **Accetto i termini del contratto di licenza** . Scegliere **Avanti**.  
  
5.  Digitare il proprio nome e il nome della società. Scegliere **Avanti**.  
  
6.  Nella pagina **Selezione funzionalità** fare clic facoltativamente su **Sfoglia** o su **costo del disco**. Scegliere **Avanti**.  
  
    -   Fare clic su **Sfoglia** per visualizzare il percorso predefinito di Generatore report e aggiornarlo.  
  
        > [!NOTE]  
        >  La cartella di installazione predefinita per Generatore report è \<unità > Programmi\Microsoft SQL Server.  
  
    -   Fare clic su **costo disco** per conoscere la quantità di spazio su disco utilizzata da Generatore report.  
  
        > [!NOTE]  
        >  Se la quantità di spazio libero su disco disponibile in un volume non è sufficiente, questo volume viene evidenziato.  
  
7.  Nella pagina **Server di destinazione predefinito** immettere facoltativamente l'URL del server di report di destinazione se diverso da quello predefinito. Scegliere **Avanti**.  
  
    > [!NOTE]  
    >  Se si intende utilizzare Generatore report quando è connesso a un server di report, è consigliabile specificare l'URL del server. Tuttavia, è possibile eseguire questa operazione anche dalla finestra di dialogo **Opzioni** quando si lavora in Generatore report.  
  
8.  Fare clic su **Installa** per completare l'installazione di Generatore report.  
  
### <a name="to-install-report-builder-from-the-command-line"></a>Per installare Generatore report dalla riga di comando  
  
1.  Passare a [Microsoft SQL Server 2012 Generatore report](https://go.microsoft.com/fwlink/?LinkID=219138) e individuare la sezione Generatore report.  
  
2.  Fare clic su **pacchetto x86**.  
  
3.  Fare clic su Salva.  
  
4.  Facoltativamente, passare al percorso in cui salvare, verificare che l'opzione **Salva con nome** sia **Windows Installer pacchetto**, quindi fare clic su **Salva**.  
  
5.  Fare clic sul menu **Start** e scegliere **Esegui**.  
  
6.  Nella casella di testo Apri digitare `cmd.`  
  
7.  Nella finestra del prompt dei comandi, spostarsi sulla cartella in cui è stato salvato il file ReportBuilder3_x86.msi.  
  
8.  Digitare un comando con il formato seguente:  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     Le due opzioni specifiche dell'installazione di Generatore report sono: RBINSTALLDIR e REPORTSERVERURL. Non è necessario includere questi argomenti nella riga di comando. Di seguito è riportato il comando di base:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. Per eseguire il comando, premere Invio.  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione, disinstallazione e Generatore report del supporto](../install-uninstall-and-report-builder-support.md)   
 [Disinstallare la versione autonoma di Generatore report &#40;Generatore report&#41;](install-report-builder.md)  
  
  
