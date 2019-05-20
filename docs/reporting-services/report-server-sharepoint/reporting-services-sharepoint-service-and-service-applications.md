---
title: Servizio SharePoint di Reporting Services e applicazioni di servizio | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1dfe62ba964b05f069009b51ddf62f376c12c906
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580541"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Servizio SharePoint di Reporting Services e applicazioni di servizio

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  La modalità SharePoint di Reporting Services è basata sull'architettura del servizio SharePoint e prevede l'uso di un servizio SharePoint e di applicazioni di servizio uno-a-molti. Creando un'applicazione di servizio si rende disponibile il servizio e si genera il database dell'applicazione di servizio. È possibile creare più applicazioni di servizio Reporting Services, tuttavia un'unica applicazione di servizio è sufficiente per la maggior parte degli scenari di distribuzione.  

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
  
## <a name="creating-a-reporting-services-service-application"></a>Creazione di un'applicazione di servizio Reporting Services

 Per creare applicazioni di servizio Reporting Services, è possibile usare Amministrazione centrale SharePoint o script di PowerShell. Per altre informazioni sull'uso di Amministrazione centrale SharePoint, vedere la sezione "Creare un'applicazione di servizio Reporting Services" in [Installare la modalità SharePoint di Reporting Services per SharePoint 2010](https://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c). Per uno script di PowerShell di esempio per la creazione di applicazioni di servizio, vedere la sezione relativa a PowerShell più avanti in questo argomento.  
  
## <a name="modify-the-associations-of-the-service-application-with-a-proxy-group"></a>Modifica delle associazioni dell'applicazione di servizio con un gruppo di proxy

 Nella pagina Nuova per la creazione di un'applicazione di servizio è contenuta la sezione **Associazione applicazione Web**. Questa sezione consente di associare l'applicazione di servizio quando viene creata. Utilizzare i passaggi seguenti per modificare l'associazione e assegnare una configurazione personalizzata all'applicazione di servizio. Lo stesso processo generale può inoltre essere utilizzato per aggiungere il proxy al gruppo predefinito anziché modificare l'associazione dell'applicazione di servizio a un gruppo personalizzato.  
  
1.  In Gestione applicazioni di Amministrazione centrale SharePoint fare clic su **Configura associazioni applicazione di servizio**.  
  
2.  Nella pagina Associazioni applicazione di servizio modificare la visualizzazione in **Applicazioni di servizio**.  
  
3.  Trovare e fare clic sul nome della nuova applicazione di servizio Reporting Services. È possibile fare clic anche sull' **impostazione predefinita** del nome del gruppo proxy di applicazione per aggiungere il proxy per impostare il gruppo piuttosto che completare i passaggi seguenti.  
  
4.  Nella casella di selezione **Modifica il gruppo di connessioni seguente** scegliere **Personalizza**.  
  
5.  Selezionare la casella relativa al proxy e fare clic su **OK**.  
  
## <a name="edit-service-application-properties"></a>Modificare le proprietà dell'applicazione di servizio

 È possibile riaprire la pagina delle proprietà dell'applicazione di servizio per modificare le proprietà.  
  
1.  Nel gruppo Gestione applicazioni di Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Selezionare l'applicazione di servizio facendo clic sul tipo di colonna per selezionare l'intera riga. Se si fa clic sul nome dell'applicazione, viene aperta la pagina delle opzioni di gestione per il servizio anziché le proprietà dell'applicazione di servizio.  
  
3.  Nella barra multifunzione relativa alle applicazioni di servizio fare clic su **Proprietà**.  
  
## <a name="create-a-reporting-services-service-application-using-powershell"></a>Creare un'applicazione di servizio Reporting Services usando PowerShell

 È possibile utilizzare PowerShell per creare l'applicazione di servizio e il proxy. Nell'esempio sottostante si presuppone che si conosca quale pool di applicazioni si desidera configurare affinché venga utilizzato dall'applicazione di servizio.  
  
1.  Aggiungere l'oggetto del pool di applicazioni del nome del pool di applicazioni a una variabile che viene passata in Nuova azione.  
  
    ```  
    $appPoolName = get-spserviceapplicationpool "<application pool name>"  
    ```  
  
2.  Creare l'applicazione di servizio con un nome e il nome del pool di applicazioni forniti.  
  
    ```  
    New-SPRSServiceApplication -Name 'MyServiceApplication' -ApplicationPool $appPoolName -DatabaseName 'MyServiceApplicationDatabase' -DatabaseServer '<Server Name>'  
    ```  
  
3.  Ottenere il nuovo oggetto dell'applicazione di servizio e inoltrare tramite pipe l'oggetto nella pipe del nuovo cmdlet del proxy.  
  
    ```  
    Get-SPRSServiceApplication -name MyServiceApplication | New-SPRSServiceApplicationProxy "MyServiceApplicationProxy"  
    ```  
  
## <a name="related-tasks"></a>Attività correlate
  
|Attività|Collegamento|  
|----------|----------|  
|Gestire le impostazioni dell'applicazione di servizio.|[Gestire un'applicazione di servizio SharePoint di Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|  
|Eseguire il backup e il ripristino dell'applicazione di servizio e dei componenti correlati, quali chiavi di crittografia e proxy.|[Eseguire il backup e il ripristino di applicazioni di servizio SharePoint di Reporting Services](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
