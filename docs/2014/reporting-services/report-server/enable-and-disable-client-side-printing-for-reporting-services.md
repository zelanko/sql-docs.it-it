---
title: Abilitare e disabilitare la stampa sul lato client per Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea5016aa51a25bd296d2e77516b30b84a7a28cec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103925"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Abilitare e disabilitare la stampa sul lato client per Reporting Services
  Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] controllo ActiveX **RSClientPrint**consente la stampa sul lato client dei report visualizzati in un browser. Tramite il controllo viene visualizzata una finestra di dialogo di stampa personalizzata che supporta funzionalità comuni ad altre finestre di questo tipo. Tra le funzionalità sono incluse l'anteprima di stampa, le selezioni delle pagine per specificare pagine e intervalli particolari, i margini di pagina e l'orientamento. Sebbene la funzionalità di stampa sul alto client sia abilitata per impostazione predefinita, è possibile disabilitarla per evitare che venga utilizzata.  
  
> [!NOTE]  
>  Per il download dei controlli ActiveX, sono necessarie le autorizzazioni di amministratore.  
  
## <a name="downloading-the-activex-control"></a>Download del controllo ActiveX  
 Ogni utente che desidera utilizzare la caratteristica di stampa deve scaricare e installare il controllo ActiveX che consente di stampare sul client. La prima volta che un utente fa clic sull'icona della **stampante** sulla barra degli strumenti del report, il controllo Microsoft ActiveX viene scaricato nel computer. Dopo il download del controllo, viene visualizzata la finestra di dialogo **stampa** ogni volta che l'utente fa clic sull'icona della **stampante** .  
  
 A seconda delle impostazioni del browser, è possibile che venga richiesto di installare il controllo, che venga impedito di farlo oppure che il controllo venga installato in modo trasparente in background.  
  
 Per [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, le impostazioni che interessano il download e l'installazione dei controlli ActiveX vengono specificate tramite il nodo **controlli ActiveX e plug-** in nella pagina **impostazioni di sicurezza** per l'area del contenuto Web. Le impostazioni seguenti determinano se gli utenti possono scaricare ed eseguire il controllo di stampa, in base alle preferenze di sicurezza dell'area Web:  
  
-   Scarica controlli ActiveX con firma elettronica.  
  
-   Esegui script controlli ActiveX contrassegnati come sicuri.  
  
-   Esegui controlli e plug-in ActiveX.  
  
 Gli utenti che desiderano utilizzare **RSClientPrint** per eseguire la stampa sul lato client devono abilitare gli elementi seguenti:  
  
-   **Scaricare i controlli ActiveX firmati** e il **controllo ActiveX script contrassegnati come sicuri per gli script** per scopi di installazione.  
  
-   **Eseguire controlli ActiveX e plug-** in per le operazioni di stampa in corso.  
  
 Il controllo ActiveX **RSClientPrint** è firmato, ovvero contiene un certificato digitale valido da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="enabling-and-disabling-client-side-printing"></a>Abilitazione e disabilitazione della stampa sul lato client  
 Gli amministratori del server di report hanno la possibilità di disabilitare la funzionalità di stampa impostando la proprietà **** di sistema `false`del server di report EnableClientPrinting su. Questa impostazione disabilita la stampa sul lato client per tutti i report gestiti dal server. Per impostazione predefinita, **EnableClientPrinting** è impostato `true`su. È possibile disabilitare la stampa sul lato client nei modi seguenti:  
  
-   Per un **server di report in modalità nativa**:  
  
    1.  Avviare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] con privilegi amministrativi.  
  
    2.  Connettersi a un'istanza del server di report in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
    3.  Fare clic con il pulsante destro del mouse sul nodo del server di report, quindi scegliere **Proprietà**. Se l'opzione **Proprietà** è disabilitata, verificare che [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] sia stato avviato con i privilegi amministrativi.  
  
    4.  Selezionare **Abilita download per il controllo di stampa client ActiveX**.  
  
    5.  Fare clic su **OK**.  
  
-   Per un **server di report in modalità SharePoint**:  
  
    1.  In Amministrazione centrale SharePoint fare clic su **Gestione applicazioni**.  
  
    2.  Fare clic su **Gestisci applicazioni di servizio**.  
  
    3.  Fare clic sul nome dell'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , quindi su **Gestisci** nella barra multifunzione di SharePoint.  
  
    4.  Fare clic su **Impostazioni sistema**.  
  
    5.  Selezionare **Abilita stampa client**. L'opzione **Abilita stampa client** si trova nella parte inferiore della pagina.  
  
    6.  Fare clic su **OK**.  
  
-   Scrivere script o codice per impostare la proprietà di sistema del server di report **EnableClientPrinting** su`false.`  
  
 Nello script di esempio riportato di seguito viene illustrato un approccio per la disabilitazione della stampa sul alto client. Compilare e quindi eseguire il codice di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] seguente per impostare la proprietà **EnableClientPrinting** su **False**. Al termine dell'esecuzione del codice, riavviare IIS.  
  
### <a name="sample-script"></a>Script di esempio  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```  
  
  
