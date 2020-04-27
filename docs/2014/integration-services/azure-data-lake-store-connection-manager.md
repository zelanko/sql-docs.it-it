---
title: Gestione connessione di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSCM.F1
- SQL11.DTS.DESIGNER.AFPADLSCM.F1
ms.assetid: 7f1323f9-9dc3-4378-9c70-bbc65bfeabfd
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: c835f42fdbcc43309a0235f8ad862bee9c230e33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66462695"
---
# <a name="azure-data-lake-store-connection-manager"></a>Gestione connessioni di Azure Data Lake Store
  La **Gestione connessioni di Azure Data Lake Store** consente a un pacchetto SSIS di connettersi a un servizio di Azure Data Lake Store tramite due tipi di autenticazione: identità utente Azure AD e identità del servizio di Azure Active Directory.  

## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurare la Gestione connessioni di Azure Data Lake Store 
  
1.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **AzureDataLake**e fare clic su **Aggiungi**.   
  
2.  Nella finestra di dialogo dell'editor della Gestione connessioni di Azure Data Lake Store digitare l'URL host di Azure Data Lake Store nel campo **ADLS Host** (Host ADLS). Ad esempio: https:\//test.azuredatalakestore.net o test.azuredatalakestore.NET.
  
3.  Scegliere il tipo di autenticazione corrispondente per accedere ai dati di Azure Data Lake Store.

    1.  Se si seleziona l'opzione di autenticazione **Identità utente Azure AD** , eseguire le operazioni seguenti:

        1. Specificare i valori per i campi **Nome utente** e **Password** . 
    
        2. Fare clic su **Test connessione** per testare la connessione. Se l'utente e l'amministratore tenant non hanno mai consentito prima a SSIS di accedere ai dati di Azure Data Lake Store, è necessario fare clic sul pulsante **Accetta** per consentire a SSIS di accedere ai dati di Azure Data Lake Store nella finestra di pop up separata. Per altre informazioni su questa esperienza di consenso, vedere [Integrazione di applicazioni con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad).
    
        > [!NOTE] 
        > Per l'opzione di autenticazione Identità utente Azure AD, l'autenticazione a più fattori e account Microsoft NON è supportata.
    
    2.  Se si seleziona l'opzione di autenticazione **Identità del servizio di Azure AD** , eseguire le operazioni seguenti:
        1. Creare un'applicazione e un'entità servizio di AAD che possano accedere alle risorse di Azure Data Lake.
    
        2. Assegnare le autorizzazioni corrispondenti all'applicazione AAD per accedere alle risorse di Azure Data Lake. Per altre informazioni su questa opzione di autenticazione, vedere [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)(Usare il portale per creare applicazioni ed entità servizio di Active Directory che possano accedere alle risorse).
    
        3. Specificare i valori per **ID client**, **Chiave privata** e **Nome del tenant** .
    
        4. Fare clic su **Test connessione** per testare la connessione.  
  
4.  Fare clic su **OK** per chiudere la finestra di dialogo.  
  
    È possibile visualizzare le proprietà del componente Gestione connessione create nella finestra **Proprietà** .  
  
  
