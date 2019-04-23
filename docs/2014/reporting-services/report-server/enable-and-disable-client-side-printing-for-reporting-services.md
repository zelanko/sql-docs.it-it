---
title: Abilitare e disabilitare la stampa sul lato client per Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 838c48ec4c15d1e89a571e5cb84cf1add613a045
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59936587"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Abilitare e disabilitare la stampa sul lato client per Reporting Services
  Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] controllo ActiveX **RSClientPrint**, consente la stampa sul lato client per i report visualizzati in un browser. Tramite il controllo viene visualizzata una finestra di dialogo di stampa personalizzata che supporta funzionalità comuni ad altre finestre di questo tipo. Tra le funzionalità sono incluse l'anteprima di stampa, le selezioni delle pagine per specificare pagine e intervalli particolari, i margini di pagina e l'orientamento. Sebbene la funzionalità di stampa sul alto client sia abilitata per impostazione predefinita, è possibile disabilitarla per evitare che venga utilizzata.  
  
> [!NOTE]  
>  Per il download dei controlli ActiveX, sono necessarie le autorizzazioni di amministratore.  
  
## <a name="downloading-the-activex-control"></a>Download del controllo ActiveX  
 Ogni utente che desidera utilizzare la caratteristica di stampa deve scaricare e installare il controllo ActiveX che consente di stampare sul client. La prima volta che un utente fa clic il **stampante** icona sulla barra degli strumenti report, il controllo viene scaricato nel computer Microsoft ActiveX. Dopo il download del controllo, il **Print** consente di visualizzare la finestra di dialogo ogni volta che l'utente fa clic il **stampante** icona.  
  
 A seconda delle impostazioni del browser, è possibile che venga richiesto di installare il controllo, che venga impedito di farlo oppure che il controllo venga installato in modo trasparente in background.  
  
 Per [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, le impostazioni che influiscono sull'installazione e download del controllo ActiveX sono specificate tramite il **ActiveX controlli e plug-in** nodo la **le impostazioni di sicurezza** pagina l'area di contenuto Web. Le impostazioni seguenti determinano se gli utenti possono scaricare ed eseguire il controllo di stampa, in base alle preferenze di sicurezza dell'area Web:  
  
-   Scarica controlli ActiveX con firma elettronica.  
  
-   Esegui script controlli ActiveX contrassegnati come sicuri.  
  
-   Esegui controlli e plug-in ActiveX.  
  
 Gli utenti che desiderano utilizzare **RSClientPrint** per eseguire la stampa sul lato client, è necessario abilitare le opzioni seguenti:  
  
-   **Scarica controlli ActiveX con firma** e **Esegui Script controlli ActiveX contrassegnati come sicuri per lo scripting** per scopi di installazione.  
  
-   **Eseguire i controlli ActiveX e plug-in** per operazioni di stampa in corso.  
  
 Il **RSClientPrint** controllo ActiveX è firmato, ovvero contiene un certificato digitale valido [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="enabling-and-disabling-client-side-printing"></a>Abilitazione e disabilitazione della stampa sul lato client  
 Gli amministratori di server di report hanno la possibilità di disabilitare la caratteristica di stampa impostando la proprietà di sistema di server di report **EnableClientPrinting** a `false`. Questa impostazione disabilita la stampa sul lato client per tutti i report gestiti dal server. Per impostazione predefinita **EnableClientPrinting** è impostata su `true`. È possibile disabilitare la stampa sul lato client nei modi seguenti:  
  
-   Per un **server di report in modalità nativa**:  
  
    1.  Avviare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] con privilegi amministrativi.  
  
    2.  Connettersi a un'istanza del server di report in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
    3.  Fare clic con il pulsante destro del mouse sul nodo del server di report, quindi scegliere **Proprietà**. Se l'opzione **Proprietà** è disabilitata, verificare che [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] sia stato avviato con i privilegi amministrativi.  
  
    4.  Selezionare **Consenti download per il controllo di stampa client ActiveX**.  
  
    5.  Fare clic su **OK**.  
  
-   Per un **server di report in modalità SharePoint**:  
  
    1.  In Amministrazione centrale SharePoint fare clic su **Gestione applicazioni**.  
  
    2.  Fare clic su **Gestisci applicazioni di servizio**.  
  
    3.  Fare clic sul nome dell'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , quindi su **Gestisci** nella barra multifunzione di SharePoint.  
  
    4.  Fare clic su **Impostazioni sistema**.  
  
    5.  Selezionare **Abilita stampa client**. L'opzione **Abilita stampa client** si trova nella parte inferiore della pagina.  
  
    6.  Fare clic su **OK**.  
  
-   Scrivere script o codice per impostare la proprietà di sistema di server di report **EnableClientPrinting** a `false.`  
  
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
  
  
