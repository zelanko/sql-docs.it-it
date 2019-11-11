---
title: Abilita errori remoti (Reporting Services) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- remote data source [Reporting Services]
- EnableRemoteError server property
ms.assetid: 5f05022b-d557-43e0-b50a-f5e2a1846b83
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3b26db3656ee548e08f9e5d4737033bb3393a969
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593877"
---
# <a name="enable-remote-errors-reporting-services"></a>Abilita errori remoti (Reporting Services)
  È possibile impostare le proprietà di un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modo che vengano restituite ulteriori informazioni sulle condizioni di errore che si verificano nei server remoti. Se in un messaggio di errore è incluso il testo "Per ulteriori informazioni su questo errore, passare al server di report nel server locale oppure abilitare gli errori remoti", sarà possibile impostare la proprietà **EnableRemoteErrors** per accedere a informazioni aggiuntive che consentono di risolvere il problema. Per altre informazioni, vedere [Proprietà di sistema del server di report](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md).  
  
 Contenuto dell'argomento:  
  
-   [Abilitare errori remoti per la modalità SharePoint](#bkmk_sharepoint)  
  
-   [Abilitare errori remoti tramite SQL Server Management Studio (modalità nativa)](#bkmk_mgtStudio)  
  
-   [Abilitare errori remoti tramite script (modalità nativa)](#bkmk_script)  
  
-   [Modifica della tabella ConfigurationInfo (modalità nativa)](#bkmk_ConfigurationInfo)  
  
##  <a name="bkmk_sharepoint"></a> Abilitare errori remoti per la modalità SharePoint  
 Sono disponibili due procedure diverse per l'abilitazione di errori remoti per la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La procedura è diversa per le due differenti architetture del server di report. Nell'architettura più recente basata sul servizio SharePoint introdotta nella versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] viene utilizzata un'impostazione che può essere configurata per ogni applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Nell'architettura precedente viene utilizzata una sola impostazione del livello di sito.  
  
#### <a name="enable-remote-errors-for-a-reporting-services-service-application"></a>Abilitare errori remoti per un'applicazione di servizio Reporting Services  
  
1.  Per un server di report in modalità SharePoint installato con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o una versione più recente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], abilitare l'impostazione dell'applicazione di servizio **Abilita errori remoti**. Questa impostazione può essere configurata per ogni applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni** .  
  
3.  Trovare l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e fare clic sul relativo nome.  
  
4.  Fare clic su **Impostazioni sistema**.  
  
5.  Fare clic su **Abilita errori remoti** nella sezione **Sicurezza** .  
  
6.  Fare clic su **OK**.  
  
#### <a name="enable-remote-errors-for-a-sharepoint-site"></a>Abilitare errori remoti per un sito SharePoint  
  
1.  Per un server di report in modalità SharePoint installato con una versione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] precedente a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], abilitare l'impostazione del sito **Abilita i messaggi di errore in modalità locale**.  
  
2.  In **Azioni sito** fare clic su **Impostazioni sito** per il sito che si desidera modificare.  
  
3.  Fare clic su **Impostazioni del sito per Reporting Services** nel gruppo **Reporting Services** .  
  
4.  Fare clic su **Abilita i messaggi di errore in modalità locale**.  
  
5.  Fare clic su **OK**.  
  
##  <a name="bkmk_mgtStudio"></a> Abilitare errori remoti tramite SQL Server Management Studio (modalità nativa)  
  
1.  Avviare Management Studio e connettersi a un'istanza del server di report. Per altre informazioni, vedere [Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
2.  Fare clic con il pulsante destro del mouse sul nodo del server di report, quindi scegliere **Proprietà**.  
  
3.  Fare clic su **Avanzate** per aprire la pagina delle proprietà. Per altre informazioni, vedere [Proprietà server &#40;pagina Avanzate&#41; - Reporting Services](../../reporting-services/tools/server-properties-advanced-page-reporting-services.md).  
  
4.  Nella sezione **sicurezza** , in **EnableRemoteErrors**, selezionare **true**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_script"></a> Abilitare errori remoti tramite script (modalità nativa)  
  
1.  Creare un file di testo e copiare lo script seguente nel file.  
  
    ```  
    Public Sub Main()  
      Dim P As New [Property]()  
      P.Name = "EnableRemoteErrors"  
      P.Value = True  
      Dim Properties(0) As [Property]  
      Properties(0) = P  
      Try  
        rs.SetSystemProperties(Properties)  
        Console.WriteLine("Remote errors enabled.")  
      Catch SE As SoapException  
        Console.WriteLine(SE.Detail.OuterXml)  
      End Try  
    End Sub  
    ```  
  
2.  Salvare il file con il nome EnableRemoteErrors.rss.  
  
3.  Fare clic sul pulsante **Start**, scegliere **Esegui**, digitare **cmd**e quindi fare clic su **OK** per aprire una finestra del prompt dei comandi.  
  
4.  Passare alla directory in cui è incluso il file con estensione rss appena creato.  
  
5.  Digitare la riga di comando seguente sostituendo *servername* con il nome effettivo del server in uso:  
  
    ```  
    rs -i EnableRemoteErrors.rss -s https://servername/ReportServer  
    ```  
  
6.  Per altre informazioni, vedere [Utilità RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md).  
  
##  <a name="bkmk_ConfigurationInfo"></a> Modifica della tabella ConfigurationInfo (modalità nativa)  
  
> [!NOTE]  
>  È possibile modificare la tabella **ConfigurationInfo** nel database del server di report per impostare **EnableRemoteErrors** su **True**. Se, tuttavia, il server di report viene utilizzato in modo attivo, per modificare le impostazioni è consigliabile utilizzare SQL Server Management Studio o uno script. Se si modifica l'impostazione nel database, è necessario riavviare il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] prima dell'applicazione delle modifiche.  
  
  
