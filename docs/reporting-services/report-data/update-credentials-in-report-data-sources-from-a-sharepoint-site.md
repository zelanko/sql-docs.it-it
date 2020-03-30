---
title: Aggiornare le credenziali nelle origini dati dei report da un sito di SharePoint | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a9908e340dadeb1108e68ca10f466276c14df23
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "65575440"
---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>Aggiornare le credenziali nelle origini dati dei report da un sito di SharePoint
  In questo argomento viene descritto come aggiornare origini dati incorporate in report e origini dati condivise salvate in una raccolta documenti di SharePoint.  
  
 Molti dei report potrebbero includere origini dati o utilizzare origini dati condivise configurate per l'utilizzo dell'autenticazione di Windows. In alcuni casi, ad esempio per la creazione di avvisi dati in report salvati in una raccolta documenti di SharePoint, è necessario aggiornare le credenziali dell'origine dati in modo che vengano utilizzate credenziali archiviate o nessuna credenziale.  
  
 Per utilizzare credenziali archiviate nei report, è possibile decidere di creare e utilizzare un nuovo account di accesso di SQL server. Per altre informazioni, vedere [Creazione di un account di accesso](../../relational-databases/security/authentication-access/create-a-login.md).  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>Per aggiornare un'origine dati incorporata per utilizzare credenziali archiviate  
  
1.  Passare alla raccolta documenti di SharePoint in cui è stato salvato il report.  
  
2.  Fare clic sull'icona per espandere il menu a discesa nel report, quindi fare clic su **Gestisci origini dati**.  
  
     Verrà visualizzata la pagina Gestisci origini dati.  
  
3.  Nella colonna **Nome** fare clic sull'origine dati.  
  
4.  Per **Tipo di connessione** verificare che sia selezionata l'opzione **Origine dati personalizzata** .  
  
     Questa opzione indica che l'origine dati è incorporata nel report.  
  
5.  Lasciare invariate le opzioni **Tipo di origine dati** e **Stringa di connessione** , a meno che non si desideri connettere il report a un diverso tipo di origine dati, server o archivio dati.  
  
6.  Per **Credenziali**selezionare **Credenziali archiviate**. Questa opzione funziona solo se l'origine dati non accetta le credenziali o se il passaggio di queste ultime avviene in altro modo.  
  
     In determinate circostanze è anche possibile utilizzare l'opzione **Credenziali non necessarie** .  
  
     Con alcuni tipi di origini dati, l'account di esecuzione automatica deve essere configurato nel server di report. Per altre informazioni, vedere l'argomento per l'origine dati corrispondente in [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) e [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
7.  Digitare un nome utente e una password.  
  
    -   Se l'account è un account utente di dominio di Windows, specificarlo nel formato: \<dominio>\\<account\>, quindi selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**.  
  
    -   Se il nome utente e la password sono credenziali del database, non selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**. Se il server di database supporta la rappresentazione o la delega, è possibile selezionare **Imposta contesto di esecuzione sull'account seguente**.  
  
8.  Per verificare che l'origine dati possa connettersi usando le credenziali aggiornate, fare clic su **Test connessione**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>Per aggiornare un'origine dati condivisa per utilizzare credenziali archiviate  
  
1.  Passare alla raccolta documenti di SharePoint in cui è stata salvata l'origine dati condivisa.  
  
2.  Fare clic sull'icona per espandere il menu a discesa nell'origine dati condivisa, quindi fare clic su **Modifica definizione origine dati**.  
  
     Verrà visualizzata la pagina Origine dati.  
  
3.  Lasciare invariate le opzioni **Tipo di origine dati** e **Stringa di connessione** , a meno che non si desideri connettere l'origine dati condivisa a un diverso tipo di origine dati, server o archivio dati.  
  
4.  Per **Credenziali**selezionare **Credenziali archiviate**.  
  
     In determinate circostanze è anche possibile utilizzare l'opzione **Credenziali non necessarie** . Questa opzione funziona solo se l'origine dati non accetta le credenziali o se il passaggio di queste ultime avviene in altro modo.  
  
     Con alcuni tipi di origini dati, l'account di esecuzione automatica deve essere configurato nel server di report. Per altre informazioni, vedere l'argomento per l'origine dati corrispondente in [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) e [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
5.  Digitare un nome utente e una password.  
  
    -   Se l'account è un account utente di dominio Windows, specificarlo nel formato \<dominio>\\<account\> e quindi selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**.  
  
    -   Se il nome utente e la password sono credenziali del database, non selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**. Se il server di database supporta la rappresentazione o la delega, è possibile selezionare **Imposta contesto di esecuzione sull'account seguente**.  
  
6.  Per verificare che l'origine dati possa connettersi usando le credenziali aggiornate, fare clic su **Test connessione**.  
  
7.  Verificare che l'opzione Abilita questa origine dati sia selezionata.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Caricare documenti in una raccolta di SharePoint &#40;Reporting Services in modalità SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  
