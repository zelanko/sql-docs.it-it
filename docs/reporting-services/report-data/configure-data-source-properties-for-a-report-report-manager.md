---
title: Configurare le proprietà delle origini dati per un report impaginato - SSRS | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
ms.assetid: 27af5195-c845-40e0-9a9c-efe569424022
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5e134c81fd697d4aa6fc7e5b620c1a71ff462b73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573200"
---
# <a name="configure-data-source-properties-for-a-paginated-report"></a>Configurare le proprietà delle origini dati per un report impaginato
  Quando si esegue un report impaginato, il server di report recupera informazioni sulle proprietà per determinare come effettuare la connessione a un'origine dati. Il tipo di origine dati, la stringa di connessione e le informazioni sulle credenziali sono specificati nelle pagine delle proprietà dell'origine dati del report pubblicato. È possibile impostare le proprietà per modificare le informazioni sulla connessione all'origine dati rispetto ai valori originali specificati al momento della creazione del report.  
  
 In alternativa, se si dispone di un'origine dati condivisa predefinita che specifica già le informazioni sulla connessione da utilizzare, è possibile specificare tale origine. Per usare un'origine dati condivisa, fare clic su **Origine dati condivisa** nella pagina delle proprietà dell'origine dati del report.  
  
## <a name="to-configure-an-embedded-data-source"></a>Per configurare un'origine dati incorporata  
  
1.  Nel portale Web passare al report per il quale si vuole configurare un'origine dati specifica del report.  
  
3.  Selezionare i puntini di sospensione ( **...** ) nell'angolo superiore destro > **Gestisci**.  
  
4.  Fare clic sulla scheda **Origini dati** . Verrà visualizzata la pagina delle proprietà dell'origine dati del report.  
  
5.  Fare clic su **Origine dati personalizzata** per specificare le informazioni sulla connessione all'origine dati all'interno del report.  
  
6.  Nell'elenco **Tipo di connessione** specificare l'estensione per l'elaborazione dati usata per elaborare i dati dall'origine dati.  
  
7.  Per **Stringa di connessione**specificare la stringa utilizzata dal server di report per la connessione all'origine dei dati. È consigliabile evitare di specificare credenziali nella stringa di connessione.  
  
     L'esempio seguente illustra una stringa di connessione usata per connettersi al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] database:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  Per **Connetti tramite**specificare come verranno ottenute le credenziali quando il report è in esecuzione:  
  
    -   Se si vuole richiedere all'utente un nome di accesso e una password, fare clic su **Credenziali fornite dall'utente che esegue il report**.  
  
    -   Se si prevede di usare l'origine dati con report che supportano le sottoscrizioni o altre operazioni pianificate, ad esempio la generazione della cronologia del report automatica, fare clic su **Credenziali archiviate in modo sicuro nel server di report**.  
  
    -   Se si vuole che le credenziali dell'utente che accede al report vengano passate dal server di report al server che ospita l'origine dati esterna, fare clic su **Sicurezza integrata di Windows**. In questo caso, all'utente non viene richiesto di digitare un nome utente o una password.  
  
    -   Se l'origine dati non usa credenziali (ad esempio, se l'origine dati è un file XML a cui si accede dal file system), fare clic su **Credenziali non necessarie**. È necessario specificare questo tipo di credenziali solo se l'operazione risulta valida per l'origine dati specifica. Se si seleziona questa opzione per un'origine dati che richiede l'autenticazione, la connessione non verrà stabilita. Se si seleziona questa opzione, assicurarsi inoltre di configurare l'account di esecuzione automatica che consente al server di report di connettersi agli altri computer per recuperare dati o file quando le credenziali utente non sono disponibili.  
  
 Per altre informazioni sulla configurazione delle credenziali, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Per altre informazioni sull'account di esecuzione automatica, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Vedere anche  
[Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
[Gestire origini dati dei report](../../reporting-services/report-data/manage-report-data-sources.md)
  
