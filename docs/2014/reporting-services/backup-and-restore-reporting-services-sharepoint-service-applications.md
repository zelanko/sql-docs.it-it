---
title: Backup e ripristino Services applicazioni di servizio SharePoint di Reporting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: dfb4ed77-90e5-4273-b690-89a945508ed2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ee23e7f2382ca84ad609b3c150f77b4f9530725b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033832"
---
# <a name="backup-and-restore-reporting-services-sharepoint-service-applications"></a>Eseguire il backup e il ripristino di applicazioni di servizio SharePoint di Reporting Services
  In questo argomento vengono descritte le procedure di backup e ripristino di un'applicazione di servizio [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] tramite Amministrazione centrale SharePoint o PowerShell. Contenuto dell'argomento:  
  
-   [Limitazioni e restrizioni](#bkmk_Restrictions)  
  
-   [Backup dell'applicazione di servizio](#bkmk_backup)  
  
-   [Ripristino dell'applicazione di servizio](#bkmk_restore)  
  
##  <a name="bkmk_BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="bkmk_Restrictions"></a> Limitazioni e restrizioni  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utilizzando le funzionalità di backup e ripristino di SharePoint. **Sono necessari passaggi aggiuntivi** , illustrati in questo argomento. Attualmente, tramite il processo di backup **non** viene eseguito il backup di credenziali e chiavi di crittografia per gli account di esecuzione automatica (UEA) o l'autenticazione di Windows nel database di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
###  <a name="bkmk_recommendations"></a> Indicazioni  
  
-   Eseguire il backup delle chiavi di crittografia prima di avviare il backup di SharePoint. Se non si esegue il backup delle chiavi di crittografia, non sarà possibile accedere ai dati crittografati in seguito al ripristino dell'applicazione di servizio. Sarà necessario eliminare i dati crittografati.  
  
-   Verificare se nell'applicazione di servizio [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] viene utilizzato un account di esecuzione automatica o l'autenticazione di Windows per l'accesso al database. In caso affermativo, verificare quali sono le credenziali appropriate, per poter configurare correttamente l'applicazione di servizio dopo il processo di ripristino.  
  
-   Rivedere il log di backup di SharePoint creato nella stessa cartella del file di backup. Il file è in genere denominato **spbackup.log**  
  
##  <a name="bkmk_backup"></a> Backup dell'applicazione di servizio  
 Completare i passaggi seguenti nell'ordine indicato:  
  
1.  Eseguire il backup delle chiavi di crittografia  
  
2.  Backup dell'applicazione di servizio  
  
3.  Verificare se nell'applicazione di servizio viene utilizzato un account di esecuzione automatica o l'autenticazione di Windows per l'accesso al database. In caso affermativo, annotare le credenziali in modo da poterle utilizzare per configurare l'applicazione di servizio dopo il ripristino.  
  
### <a name="backup-the-encryption-keys-using-central-administration"></a>Eseguire il backup delle chiavi di crittografia tramite Amministrazione centrale  
 Per informazioni sul backup delle chiavi di crittografia di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vedere la sezione "Chiavi di crittografia" di [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
###  <a name="bkmk_centraladmin"></a> Eseguire il backup dell'applicazione di servizio tramite Amministrazione centrale SharePoint  
 Per eseguire il backup dell'applicazione di servizio, attenersi alla procedura seguente:  
  
1.  In Amministrazione centrale SharePoint fare clic su **Esegui backup** nel gruppo **Backup e ripristino** .  
  
2.  Nel nodo **Servizi condivisi** espandere **Applicazioni di servizi condivisi** e selezionare l'applicazione di servizio. L'applicazione sarà di tipo **Applicazione di servizio SQL Server Reporting Services**.  
  
3.  Scegliere **Avanti**.  
  
4.  Digitare il percorso in **Percorso backup** , quindi fare clic su **Avvia backup**.  
  
5.  Ripetere il processo precedente ma, anziché selezionare l'applicazione di servizio, espandere il nodo **Proxy servizi condivisi** e selezionare il proxy dell'applicazione di servizio. Il proxy sarà di tipo **Proxy dell'applicazione di servizio SQL Server Reporting Services**.  
  
 Per ulteriori informazioni, vedere gli argomenti seguenti nella documentazione di SharePoint:  
  
 [Eseguire il backup di un'applicazione di servizio (SharePoint Foundation 2010) nella documentazione di SharePoint](https://msdn.microsoft.com/library/ee748601.aspx).  
  
 [Eseguire il backup di un'applicazione di servizio (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Verificare l'account di esecuzione e l'autenticazione del database  
 **Account di esecuzione:** per verificare se nell'applicazione di servizio viene usato un account di esecuzione:  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni** .  
  
2.  Fare clic sul nome dell'applicazione di servizio, quindi su **Gestisci** sulla barra multifunzione di SharePoint.  
  
3.  Fare clic su **Account di esecuzione**.  
  
4.  Se è configurato un account di esecuzione, è necessario conoscere le credenziali per ripristinare il backup dell'applicazione di servizio. Non procedere con le operazioni di backup e ripristino fino a quando non si conoscono le credenziali corrette.  
  
 **Autenticazione del database:** per verificare se nell'applicazione di servizio viene usata l'autenticazione di Windows per l'autenticazione del database:  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni** .  
  
2.  Fare clic sul nome dell'applicazione di servizio, quindi su **Proprietà** sulla barra multifunzione di SharePoint.  
  
3.  Analizzare la sezione **Database di servizio di SQL Server Reporting Services (SSRS)** .  
  
4.  Se è configurata l'autenticazione di Windows, è necessario conoscere le credenziali per poter configurare l'applicazione di servizio dopo il ripristino. Non procedere con le operazioni di backup e ripristino fino a quando non si conoscono le credenziali corrette.  
  
##  <a name="bkmk_restore"></a> Ripristino dell'applicazione di servizio  
 Completare i passaggi seguenti nell'ordine indicato:  
  
1.  Ripristinare l'applicazione di servizio [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
2.  Ripristinare le chiavi di crittografia.  
  
3.  Se nell'applicazione di servizio viene utilizzato un account di esecuzione o l'autenticazione di Windows per l'accesso al database, configurare le credenziali.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Ripristinare l'applicazione di servizio tramite Amministrazione centrale SharePoint  
  
1.  In Amministrazione centrale SharePoint fare clic su **Ripristina da backup** nel gruppo **Backup e ripristino** .  
  
2.  Digitare il percorso del file di backup nella casella **Percorso directory di backup** , quindi fare clic su **Aggiorna**.  
  
3.  Selezionare il backup dell'applicazione di servizio nell'elenco **Componente principale** , quindi fare clic su **Avanti**.  
  
4.  Selezionare l'applicazione [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , quindi fare clic su **Avanti**.  
  
5.  Nella sezione **Nomi e password di accesso** digitare la password per il nome di accesso. La casella del nome di accesso viene popolata con l'account di accesso utilizzato dall'applicazione di servizio prima del backup.  
  
6.  Fare clic su **Avvia ripristino**.  
  
7.  Ripetere il processo precedente ma, anziché ripristinare l'applicazione di servizio, espandere il nodo **Servizi condivisi** , quindi il nodo **Applicazioni di servizi condivisi** .  
  
 Per ulteriori informazioni, vedere gli argomenti seguenti nella documentazione di SharePoint:  
  
 [Ripristinare un'applicazione di servizio (SharePoint Foundation 2010)](https://msdn.microsoft.com/library/ee748615.aspx).  
  
 [Ripristinare un'applicazione di servizio (SharePoint Server 2010)](ttp://technet.microsoft.com/library/ee428305.aspx).  
  
### <a name="restore-the-encryption-keys-using-central-administration"></a>Eseguire il ripristino delle chiavi di crittografia tramite Amministrazione centrale  
 Per informazioni sul ripristino delle chiavi di crittografia di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vedere la sezione "Chiavi di crittografia" di [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
### <a name="configure-the-execution-account-and-database-authentication"></a>Configurare l'account di esecuzione e l'autenticazione del database  
 **Account di esecuzione:** se nell'applicazione di servizio viene usato un account di esecuzione, completare la procedura seguente per configurarlo:  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni** .  
  
2.  Fare clic sul nome dell'applicazione di servizio, quindi su **Gestisci** sulla barra multifunzione di SharePoint.  
  
3.  Fare clic su **Account di esecuzione**.  
  
4.  Digitare l'account e la password, quindi selezionare la casella **Specifica account di esecuzione** .  
  
5.  Fare clic su **OK**.  
  
 **Autenticazione del database:** se nell'applicazione di servizio viene usata l'autenticazione di Windows per l'autenticazione del database, completare la procedura seguente:  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni** .  
  
2.  Fare clic sul nome dell'applicazione di servizio, quindi su **Proprietà** sulla barra multifunzione di SharePoint.  
  
3.  Analizzare la sezione **Database di servizio di SQL Server Reporting Services (SSRS)** .  
  
4.  Selezionare **Autenticazione di Windows**.  
  
5.  Digitare l'account e la password. Selezionare **Usa come credenziali di Windows** , se appropriato.  
  
6.  Scegliere **OK**  
  
  
