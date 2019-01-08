---
title: Gestione connessione di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: douglasl
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.openlocfilehash: 5db5df2a209cf9f291c37f960cdd9b2947966061
ms.sourcegitcommit: 85fd3e1751de97a16399575397ab72ebd977c8e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/17/2018
ms.locfileid: "53531106"
---
# <a name="azure-data-lake-store-connection-manager"></a>Gestione connessioni di Azure Data Lake Store
Un pacchetto di SQL Server Integration Services (SSIS) è in grado di usare Gestione connessione di Azure Data Lake Store per connettersi a un account di Azure Data Lake Storage Gen1 con uno dei due tipi di autenticazione seguenti:
-   Identità utente Azure AD
-   Identità del servizio di Azure AD 

Gestione connessione di Azure Data Lake Store è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

> [!NOTE]
> Per assicurarsi che la Gestione connessioni di Azure Data Lake Store e che i componenti che la usano, cioè l'origine e la destinazione di Data Lake Storage Gen1, possano connettersi ai servizi, scaricare la versione del Feature Pack di Azure più recente da [qui](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurare la Gestione connessioni di Azure Data Lake Store

1.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **AzureDataLake**e quindi **Aggiungi**. Viene visualizzata la finestra di dialogo dell'**editor di Gestione connessione di Azure Data Lake Store**.
  
2.  Nella finestra di dialogo dell'**editor di Gestione connessione di Azure Data Lake Store** specificare l'URL host di Data Lake Storage Gen1 nel campo **ADLS Host** (Host ADLS). Ad esempio, `https://test.azuredatalakestore.net` o `test.azuredatalakestore.net`.
  
3.  Nel campo **Autenticazione** scegliere il tipo di autenticazione appropriato per accedere ai dati in Data Lake Storage Gen1.

    1.  Se si seleziona l'opzione di autenticazione **Identità utente Azure AD**, eseguire le operazioni seguenti:
        1. Specificare i valori per i campi **Nome utente** e **Password**. 
    
        2. Fare clic su **Test connessione** per testare la connessione. Se l'utente o l'amministratore tenant non ha precedentemente autorizzato il consenso a SSIS per accedere ai dati di Data Lake Storage Gen1, selezionare **Accetto** quando richiesto. Per altre informazioni su questa esperienza di consenso, vedere [Integrazione di applicazioni con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        > [!NOTE] 
        > Quando si seleziona l'autenticazione dell'**identità del servizio di Azure AD** l'autenticazione a più fattori e l'autenticazione dell'account Microsoft non sono supportate.
    
    2. Se si seleziona l'autenticazione dell'**identità del servizio di Azure AD**, eseguire le operazioni seguenti:
        1. Creare un'applicazione Azure Active Directory (AAD) e l'entità servizio per accedere ai dati di Data Lake Storage Gen1.
    
        2. Assegnare le autorizzazioni appropriate per consentire all'applicazione AAD di accedere alle risorse di Data Lake Storage Gen1. Per altre informazioni su questa opzione di autenticazione, vedere [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)(Usare il portale per creare applicazioni ed entità servizio di Active Directory che possano accedere alle risorse).
    
        3. Specificare i valori per **ID client**, **Chiave privata** e **Nome del tenant**.
    
        4. Fare clic su **Test connessione** per testare la connessione.  
  
6.  Selezionare **OK** per chiudere la finestra di dialogo dell'**editor di Gestione connessione di Azure Data Lake Store**.  

## <a name="view-the-properties-of-the-connection-manager"></a>Visualizzare le proprietà della gestione connessione
È possibile visualizzare le proprietà del componente Gestione connessione create nella finestra **Proprietà** .  
  
  
