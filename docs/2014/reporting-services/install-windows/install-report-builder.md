---
title: Installare la versione autonoma di Generatore Report (Generatore Report) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 830854a26d3f9b05465ee37aac6a9b7584750fe2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012712"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>Installare la versione autonoma di Generatore report (Generatore report)
  È possibile installare Generatore Report dal [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] feature pack di sul [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=168472) o in un percorso come una cartella pubblica per cui dispone il file reportbuilder3_x86.msi, ovvero il pacchetto di Windows Installer per Generatore Report, è stato scaricato.  
  
 È inoltre possibile eseguire un'installazione dalla riga di comando di Generatore report e immettere argomenti per la personalizzazione dell'installazione. Oltre i parametri intrinseci MSI standard, è possibile usare i parametri personalizzati di Generatore Report: RBINSTALLDIR e REPORTSERVERURL. RBINSTALLDIR specifica la cartella di installazione radice per Generatore report. REPORTSERVERURL specifica il server di report predefinito utilizzato da Generatore report per salvare i report.  
  
 Se si vuole eseguire un'installazione invisibile all'utente che non richiede interazioni con l'interfaccia utente, specificare l'opzione **/quiet** . In base alle caratteristiche di progettazione, il flag dell'opzione quiet elimina la visualizzazione degli errori di installazione. Quando si usa questa opzione è quindi consigliabile includere l'opzione **/l** che specifica la registrazione.  
  
> [!IMPORTANT]  
>  Le funzionalità di sicurezza di Windows Vista e Windows 7 richiedono autorizzazioni elevate per l'esecuzione delle operazioni dalla riga di comando. L'installazione non è invisibile all'utente. Per renderla invisibile è necessario eseguire la riga di comando come amministratore.  
  
### <a name="to-install-report-builder-from-the-download-site"></a>Per installare Generatore report dal sito di download  
  
1.  Passare a [Generatore Report di Microsoft SQL Server 2012](https://go.microsoft.com/fwlink/?LinkID=219138) e individuare la sezione Generatore Report della pagina Web.  
  
2.  Fare clic su **X86 pacchetto**.  
  
3.  Nel **del File da scaricare** finestra di dialogo, fare clic su **eseguire**.  
  
    > [!IMPORTANT]  
    >  Scaricare file solo da fonti attendibili.  
  
4.  Nella finestra di dialogo di Internet Explorer, fare clic su **eseguiti**.  
  
    > [!IMPORTANT]  
    >  Eseguire file solo da fonti attendibili.  
  
5.  Verrà avviata la procedura di installazione guidata di Generatore report per Microsoft SQL Server.  
  
6.  Nel **l'installazione guidata di** pagina, fare clic su **successivo**.  
  
7.  Nel **contratto di licenza** pagina, leggere il contratto e quindi selezionare la **accetto i termini del contratto di licenza** opzione. Scegliere **Avanti**.  
  
8.  Digitare il proprio nome e il nome della società. Scegliere **Avanti**.  
  
9. Nel **Selezione funzionalità** facoltativamente fare clic su **Sfoglia** o **spazio richiesto**. Scegliere **Avanti**.  
  
    -   Fare clic su **esplorare** per visualizzare il percorso predefinito di Generatore Report e aggiornarlo.  
  
        > [!NOTE]  
        >  La cartella di installazione predefinite per Generatore Report è \<unità > Program Files\Microsoft SQL Server.  
  
    -   Fare clic su **zio richiesto** per informazioni su quanto spazio su disco Generatore Report utilizza.  
  
        > [!NOTE]  
        >  Se la quantità di spazio libero su disco disponibile in un volume non è sufficiente, questo volume viene evidenziato.  
  
10. Nella pagina **Server di destinazione predefinito** immettere facoltativamente l'URL del server di report di destinazione se diverso da quello predefinito. Scegliere **Avanti**.  
  
    > [!NOTE]  
    >  Se si intende utilizzare Generatore report quando è connesso a un server di report, è consigliabile specificare l'URL del server. Tuttavia, è possibile anche eseguire questa operazione dal **opzioni** finestra di dialogo quando si lavora in Generatore Report.  
  
11. Fare clic su **installare** per completare l'installazione di Generatore Report.  
  
### <a name="to-install-report-builder-from-a-share"></a>Per installare Generatore report da una condivisione  
  
1.  Per informazioni sul percorso del file ReportBuilder3_x86.msi.msi che si esegue per installare Generatore report nel computer locale, rivolgersi all'amministratore.  
  
2.  Individuare il file ReportBuilder3_x86.msi.msi, ovvero il pacchetto di Windows Installer (MSI) per Generatore report, e fare clic su di esso.  
  
     Verrà avviata la procedura di installazione guidata di Generatore report per Microsoft SQL Server.  
  
3.  Nel **l'installazione guidata di** pagina, fare clic su **successivo**.  
  
4.  Nel **contratto di licenza** pagina, leggere il contratto e quindi selezionare la **accetto i termini del contratto di licenza** opzione. Scegliere **Avanti**.  
  
5.  Digitare il proprio nome e il nome della società. Scegliere **Avanti**.  
  
6.  Nel **Selezione funzionalità** facoltativamente fare clic su **Sfoglia** o **spazio richiesto**. Scegliere **Avanti**.  
  
    -   Fare clic su **esplorare** per visualizzare il percorso predefinito di Generatore Report e aggiornarlo.  
  
        > [!NOTE]  
        >  La cartella di installazione predefinite per Generatore Report è \<unità > Program Files\Microsoft SQL Server.  
  
    -   Fare clic su **zio richiesto** per informazioni su quanto spazio su disco Generatore Report utilizza.  
  
        > [!NOTE]  
        >  Se la quantità di spazio libero su disco disponibile in un volume non è sufficiente, questo volume viene evidenziato.  
  
7.  Nella pagina **Server di destinazione predefinito** immettere facoltativamente l'URL del server di report di destinazione se diverso da quello predefinito. Scegliere **Avanti**.  
  
    > [!NOTE]  
    >  Se si intende utilizzare Generatore report quando è connesso a un server di report, è consigliabile specificare l'URL del server. Tuttavia, è possibile anche eseguire questa operazione dal **opzioni** finestra di dialogo quando si lavora in Generatore Report.  
  
8.  Fare clic su **installare** per completare l'installazione di Generatore Report.  
  
### <a name="to-install-report-builder-from-the-command-line"></a>Per installare Generatore report dalla riga di comando  
  
1.  Passare a [Generatore Report di Microsoft SQL Server 2012](https://go.microsoft.com/fwlink/?LinkID=219138) e individuare la sezione Generatore Report.  
  
2.  Fare clic su **X86 pacchetto**.  
  
3.  Fare clic su Salva.  
  
4.  Facoltativamente, selezionare il percorso per il salvataggio, per verificare i **Salva con nome** opzione è **pacchetto di Windows Installer**e quindi fare clic su **Salva**.  
  
5.  Fare clic sul menu **Start** e scegliere **Esegui**.  
  
6.  Nella casella di testo Apri, digitare `cmd.`  
  
7.  Nella finestra del prompt dei comandi, spostarsi sulla cartella in cui è stato salvato il file ReportBuilder3_x86.msi.  
  
8.  Digitare un comando con il formato seguente:  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     Le due opzioni specifiche dell'installazione di Generatore Report sono: RBINSTALLDIR e REPORTSERVERURL. Non è necessario includere questi argomenti nella riga di comando. Di seguito è riportato il comando di base:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. Per eseguire il comando, premere Invio.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare, disinstallare e supporto di Generatore Report](../install-uninstall-and-report-builder-support.md)   
 [Disinstallare la versione autonoma di Generatore Report &#40;Generatore Report&#41;](install-report-builder.md)  
  
  
