---
title: Eseguire il backup e il ripristino di applicazioni di servizio SharePoint di Reporting Services | Microsoft Docs
description: Informazioni sulle procedure di backup e ripristino di applicazioni di servizio di SQL Server Reporting Services tramite Amministrazione centrale SharePoint o PowerShell.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e40a80f58bcc3eb2210ebb127248746e8a45a4f1
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91935534"
---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Eseguire il backup e il ripristino di applicazioni di servizio SharePoint di Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Questo argomento descrive le procedure di backup e ripristino di un'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tramite Amministrazione centrale SharePoint o PowerShell.

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

## <a name="before-you-begin"></a>Prima di iniziare

### <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni

> [!NOTE]
>  È possibile eseguire il backup e il ripristino parziale delle applicazioni di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tramite le funzionalità di backup e ripristino di SharePoint. **Sono necessari passaggi aggiuntivi** , illustrati in questo argomento. Il processo di backup attualmente **non** interessa le credenziali e le chiavi di crittografia per gli account di esecuzione automatica (UEA) o per l'autenticazione di Windows al database di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

### <a name="recommendations"></a>Consigli
  
-   Eseguire il backup delle chiavi di crittografia prima di avviare il backup di SharePoint. Se non si esegue il backup delle chiavi di crittografia, non sarà possibile accedere ai dati crittografati in seguito al ripristino dell'applicazione di servizio. Sarà necessario eliminare i dati crittografati.  
  
-   Verificare se nell'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene utilizzato un account di esecuzione automatica o l'autenticazione di Windows per l'accesso al database. In caso affermativo, verificare quali sono le credenziali appropriate, per poter configurare correttamente l'applicazione di servizio dopo il processo di ripristino.  
  
-   Accertarsi che il log di backup di SharePoint sia stato creato nella stessa cartella del file di backup. Il file è in genere denominato **spbackup.log**  
  
## <a name="back-up-the-service-application"></a>Backup dell'applicazione di servizio

 Completare i passaggi seguenti nell'ordine indicato:  
  
1.  Backup delle chiavi di crittografia  
  
2.  Backup dell'applicazione di servizio  
  
3.  Verificare se nell'applicazione di servizio viene utilizzato un account di esecuzione automatica o l'autenticazione di Windows per l'accesso al database. In caso affermativo, annotare le credenziali in modo da poterle utilizzare per configurare l'applicazione di servizio dopo il ripristino.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>Eseguire il backup delle chiavi di crittografia tramite Amministrazione centrale SharePoint

Per informazioni sul backup delle chiavi di crittografia di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere la sezione "Chiavi di crittografia" di [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>Eseguire il backup dell'applicazione di servizio tramite Amministrazione centrale SharePoint

Per eseguire il backup dell'applicazione di servizio, attenersi alla procedura seguente:  
  
1.  In Amministrazione centrale SharePoint selezionare **Esegui backup** nel gruppo **Backup e ripristino**.  
  
2.  Nel nodo **Servizi condivisi** espandere **Applicazioni di servizi condivisi** e selezionare l'applicazione di servizio. L'applicazione sarà di tipo **Applicazione di servizio SQL Server Reporting Services**.  
  
3.  Selezionare **Avanti**.  
  
4.  Digitare il percorso in **Percorso backup:** e selezionare **Avvia backup**.  
  
5.  Ripetere il processo precedente ma, anziché selezionare l'applicazione di servizio, espandere il nodo **Proxy servizi condivisi** e selezionare il proxy dell'applicazione di servizio. Il proxy sarà di tipo **Proxy dell'applicazione di servizio SQL Server Reporting Services**.  
  
 Per ulteriori informazioni, vedere gli argomenti seguenti nella documentazione di SharePoint:  
  
 [Eseguire il backup di un'applicazione di servizio (SharePoint Foundation 2010) nella documentazione di SharePoint](/previous-versions/office/sharepoint-foundation-2010/ee748601(v=office.14)).  
  
 [Eseguire il backup di un'applicazione di servizio (SharePoint Server 2010)](/SharePoint/administration/back-up-a-service-application)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Verificare l'account di esecuzione e l'autenticazione del database

 **Account di esecuzione:** per verificare se nell'applicazione di servizio viene usato un account di esecuzione:  
  
1.  In Amministrazione centrale SharePoint selezionare **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni**.  
  
2.  Selezionare il nome dell'applicazione di servizio e quindi selezionare **Gestisci** sulla barra multifunzione di SharePoint.  
  
3.  Selezionare **Account di esecuzione**.  
  
4.  Se è configurato un account di esecuzione, è necessario conoscere le credenziali per ripristinare il backup dell'applicazione di servizio. Non procedere con le operazioni di backup e ripristino fino a quando non si conoscono le credenziali corrette.  
  
 **Autenticazione del database:** per verificare se nell'applicazione di servizio viene usata l'autenticazione di Windows per l'autenticazione del database:  
  
1.  In Amministrazione centrale SharePoint selezionare **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni**.  
  
2.  Selezionare il nome dell'applicazione di servizio e quindi selezionare **Proprietà** sulla barra multifunzione di SharePoint.  
  
3.  Analizzare la sezione **Database di servizio di SQL Server Reporting Services (SSRS)** .  
  
4.  Se è configurata l'autenticazione di Windows, è necessario conoscere le credenziali per poter configurare l'applicazione di servizio dopo il ripristino. Non procedere con le operazioni di backup e ripristino fino a quando non si conoscono le credenziali corrette.  
  
## <a name="restore-the-service-application"></a>Ripristinare l'applicazione di servizio

 Completare i passaggi seguenti nell'ordine indicato:  
  
1.  Ripristinare l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Ripristinare le chiavi di crittografia.  
  
3.  Se nell'applicazione di servizio viene utilizzato un account di esecuzione o l'autenticazione di Windows per l'accesso al database, configurare le credenziali.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Ripristinare l'applicazione di servizio tramite Amministrazione centrale SharePoint
  
1.  In Amministrazione centrale SharePoint selezionare **Ripristina da backup** nel gruppo **Backup e ripristino**.  
  
2.  Digitare il percorso del file di backup nella casella **Percorso directory di backup** e selezionare **Aggiorna**.  
  
3.  Selezionare il backup dell'applicazione di servizio nell'elenco **Componente principale** e quindi fare clic su **Avanti**.  
  
4.  Selezionare l'applicazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e quindi selezionare **Avanti**.  
  
5.  Nella sezione **Nomi e password di accesso** digitare la password per il nome di accesso. La casella del nome di accesso viene popolata con l'account di accesso usato dall'applicazione di servizio prima del backup.  
  
6.  Selezionare **Avvia ripristino**.  
  
7.  Ripetere il processo precedente ma, anziché ripristinare l'applicazione di servizio, espandere il nodo **Servizi condivisi** , quindi il nodo **Applicazioni di servizi condivisi** .  
  
 Per ulteriori informazioni, vedere gli argomenti seguenti nella documentazione di SharePoint:  
  
 [Ripristinare un'applicazione di servizio (SharePoint Foundation 2010)](/previous-versions/office/sharepoint-foundation-2010/ee748615(v=office.14)).  
  
 [Ripristinare un'applicazione di servizio (SharePoint Server 2010)](/SharePoint/administration/restore-a-service-application).  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>Eseguire il ripristino delle chiavi di crittografia tramite Amministrazione centrale SharePoint

 Per informazioni sul ripristino delle chiavi di crittografia di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere la sezione "Chiavi di crittografia" di [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="configure-the-execution-account-and-database-authentication"></a>Configurare l'account di esecuzione e l'autenticazione del database

 **Account di esecuzione:** se nell'applicazione di servizio viene usato un account di esecuzione, completare la procedura seguente per configurarlo:  
  
1.  In Amministrazione centrale SharePoint selezionare **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni**.  
  
2.  Selezionare il nome dell'applicazione di servizio e quindi selezionare **Gestisci** sulla barra multifunzione di SharePoint.  
  
3.  Selezionare **Account di esecuzione**.  
  
4.  Digitare l'account e la password, quindi selezionare la casella **Specifica account di esecuzione** .  
  
5.  Selezionare **OK**.  
  
 **Autenticazione del database:** se nell'applicazione di servizio viene usata l'autenticazione di Windows per l'autenticazione del database, completare la procedura seguente:  
  
1.  In Amministrazione centrale SharePoint selezionare **Gestisci applicazioni di servizio** nel gruppo **Gestione applicazioni**.  
  
2.  Selezionare il nome dell'applicazione di servizio e quindi selezionare **Proprietà** sulla barra multifunzione di SharePoint.  
  
3.  Analizzare la sezione **Database di servizio di SQL Server Reporting Services (SSRS)** .  
  
4.  Selezionare **Autenticazione di Windows**.  
  
5.  Digitare l'account e la password. Selezionare **Usa come credenziali di Windows** , se appropriato.  
  
6.  Scegliere **OK**.

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)