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
ms.openlocfilehash: 9fe7c7cf04767e0536be8d04d99387a091962375
ms.sourcegitcommit: 5905c29b5531cef407b119ebf5a120316ad7b713
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66429005"
---
# <a name="azure-data-lake-store-connection-manager"></a>Gestione connessioni di Azure Data Lake Store
  Il **gestione connessione di Azure Data Lake Store** consente a un pacchetto SSIS per connettersi a un servizio di Azure Data Lake Store tramite due tipi di autenticazione: Identità utente Azure AD e l'identità del servizio di Azure AD.  

## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurare la Gestione connessioni di Azure Data Lake Store 
  
1.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare **AzureDataLake**e fare clic su **Aggiungi**.   
  
2.  Nella finestra di dialogo dell'editor della Gestione connessioni di Azure Data Lake Store digitare l'URL host di Azure Data Lake Store nel campo **ADLS Host** (Host ADLS). Ad esempio: https:\//test.azuredatalakestore.net o test.azuredatalakestore.net.
  
3.  Scegliere il tipo di autenticazione corrispondente per accedere ai dati di Azure Data Lake Store.

    1.  Se si seleziona l'opzione di autenticazione **Identità utente Azure AD** , eseguire le operazioni seguenti:

        1. Specificare i valori per i campi **Nome utente** e **Password** . 
    
        2. Fare clic su **Test connessione** per testare la connessione. Se l'utente e l'amministratore tenant non hanno mai consentito prima a SSIS di accedere ai dati di Azure Data Lake Store, è necessario fare clic sul pulsante **Accetta** per consentire a SSIS di accedere ai dati di Azure Data Lake Store nella finestra di pop up separata. Per altre informazioni su questa esperienza di consenso, vedere [Integrazione di applicazioni con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        > [!NOTE] 
        > Per l'opzione di autenticazione Identità utente Azure AD, l'autenticazione a più fattori e account Microsoft NON è supportata.
    
    2.  Se si seleziona l'opzione di autenticazione **Identità del servizio di Azure AD** , eseguire le operazioni seguenti:
        1. Creare un'applicazione e un'entità servizio di AAD che possano accedere alle risorse di Azure Data Lake.
    
        2. Assegnare le autorizzazioni corrispondenti all'applicazione AAD per accedere alle risorse di Azure Data Lake. Per altre informazioni su questa opzione di autenticazione, vedere [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) (Usare il portale per creare applicazioni ed entità servizio di Active Directory che possano accedere alle risorse).
    
        3. Specificare i valori per **ID client**, **Chiave privata** e **Nome del tenant** .
    
        4. Fare clic su **Test connessione** per testare la connessione.  
  
4.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
    È possibile visualizzare le proprietà del componente Gestione connessione create nella finestra **Proprietà** .  
  
  
