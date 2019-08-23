---
title: Gestione connessione dell'archiviazione di Azure | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f171499471f8f94ad970446d31cf796f4ab55fb7
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028776"
---
# <a name="azure-storage-connection-manager"></a>Gestione connessione dell'archiviazione di Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  **Gestione connessione dell'archiviazione di Azure** consente a un pacchetto SSIS di connettersi a un account di archiviazione di Azure.
   
 **Gestione connessione dell'archiviazione di Azure** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **Sottoscrizione di Azure**, quindi fare clic su **Aggiungi**.  
  
Sono disponibili le proprietà seguenti.

- **Service:** specifica il servizio di archiviazione a cui connettersi.
- **Account name:** specifica il nome dell'account di archiviazione.
- **Authentication:** specifica il metodo di autenticazione da usare. Sono supportati i metodi di autenticazione **AccessKey** e **ServicePrincipal**.
    - **AccessKey:** per questo metodo di autenticazione, specificare la **chiave dell'account**.
    - **ServicePrincipal:** per questo metodo di autenticazione, specificare l'**ID applicazione**, la **chiave applicazione** e l'**ID tenant** per l'entità servizio.
      Per il funzionamento di **Test connessione**, all'entità servizio deve essere assegnato almeno il ruolo **Lettore dei dati dei BLOB di archiviazione** per l'account di archiviazione.
      Per informazioni dettagliate, vedere [questa](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) pagina.
- **Environment:** specifica l'ambiente cloud che ospita l'account di archiviazione.

## <a name="managed-identities-for-azure-resources-authentication"></a>Identità gestite per l'autenticazione delle risorse di Azure
Quando si eseguono pacchetti SSIS nel [runtime di integrazione Azure-SSIS in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), è possibile usare l'[identità gestita](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associata alla data factory per l'autenticazione dell'archiviazione di Azure. La factory specificata può accedere e copiare i dati dall'account di archiviazione o nell'account di archiviazione usando questa identità.

Per informazioni generali sull'autenticazione per l'archiviazione di Azure, vedere [Autenticare l'accesso all'archiviazione di Azure tramite Azure Active Directory](https://docs.microsoft.com/azure/storage/common/storage-auth-aad). Per usare l'autenticazione identità gestita per l'account di archiviazione, seguire questa procedura per configurare l'account di archiviazione:

1. **[Trovare l'identità gestita della data factory dal portale di Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)** . Visualizzare le **Proprietà** della data factory. Copiare l'**ID applicazione dell'identità gestita** (NON l'**ID oggetto identità gestita**).

1. **Concedere all'identità gestita l'autorizzazione appropriata nell'account di archiviazione**. Per informazioni dettagliate sui ruoli, vedere [Gestire i diritti di accesso ai dati di archiviazione di Azure con il controllo degli accessi in base al ruolo](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal).

    - **Come origine**, in Controllo degli accessi in base al ruolo, concedere almeno il ruolo **Lettore dei dati dei BLOB di archiviazione**.
    - **Come destinazione**, in Controllo degli accessi in base al ruolo, concedere almeno il ruolo **Collaboratore ai dati dei BLOB di archiviazione**.

**Configurare quindi l'autenticazione identità gestita** per la gestione connessione dell'autenticazione di Azure. Sono disponibili due opzioni.

1. Configurare in fase di progettazione. In Progettazione SSIS fare doppio clic sulla gestione connessione dell'archiviazione di Azure per aprire l'**editor gestione connessione dell'archiviazione di Azure** e selezionare **Use managed identity to authenticate on Azure** (Usa identità gestita per l'autenticazione in Azure).
    > [!NOTE]
    >  Attualmente questa opzione NON ha effetto (ovvero l'autenticazione identità gestita non funziona) quando il pacchetto SSIS viene eseguito in Progettazione SSIS o [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.
    
1. Configurare in fase di esecuzione. Quando il pacchetto viene eseguito tramite [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) o l'[attività Esegui pacchetto SSIS di Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), individuare la gestione connessione dell'archiviazione di Azure e aggiornarne la proprietà **ConnectUsingManagedIdentity** impostandola su **True**.
    > [!NOTE]
    >  Nel runtime di integrazione Azure-SSIS tutti gli altri metodi di autenticazione, ad esempio chiave di accesso ed entità servizio, preconfigurati nella gestione connessione dell'archiviazione di Azure verranno **ignorati** quando viene usata l'autenticazione identità gestita per le operazioni sull'archiviazione.

> [!NOTE]
>  Per configurare l'autenticazione identità gestita nei pacchetti esistenti, il metodo consigliato consiste nel ricompilare almeno una volta il progetto SSIS con l'[ultima versione di Progettazione SSIS](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) e ridistribuire il progetto SSIS nel runtime di integrazione Azure-SSIS in modo che la nuova proprietà di gestione connessione **ConnectUsingManagedIdentity** venga aggiunta automaticamente in tutte le gestioni connessione dell'archiviazione di Azure nel progetto SSIS. In alternativa, è possibile usare direttamente l'override della proprietà con il percorso della proprietà **\Package.Connections[{nome della gestione connessione}].Properties[ConnectUsingManagedIdentity]** in fase di esecuzione.

## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)
