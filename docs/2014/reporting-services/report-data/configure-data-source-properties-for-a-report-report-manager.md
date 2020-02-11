---
title: Configurare le proprietà delle origini dati per un report (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
ms.assetid: 27af5195-c845-40e0-9a9c-efe569424022
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7823ce29facb7f1c85a51a12b31ee2076a0d023b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107419"
---
# <a name="configure-data-source-properties-for-a-report--report-manager"></a>Configurare le proprietà delle origini dati per un report (Gestione report)
  Quando si esegue un report, il server di report recupera informazioni sulla proprietà per determinare come connettersi a un'origine dati. Il tipo di origine dati, la stringa di connessione e le informazioni sulle credenziali sono specificati nelle pagine delle proprietà dell'origine dati del report pubblicato. È possibile impostare le proprietà per modificare le informazioni sulla connessione all'origine dati rispetto ai valori originali specificati al momento della creazione del report.  
  
 In alternativa, se si dispone di un'origine dati condivisa predefinita che specifica già le informazioni sulla connessione da utilizzare, è possibile specificare tale origine. Per usare un'origine dati condivisa, fare clic su **Origine dati condivisa** nella pagina delle proprietà dell'origine dati del report.  
  
### <a name="to-configure-an-embedded-data-source"></a>Per configurare un'origine dati incorporata  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  In Gestione report passare alla pagina **Contenuto** . quindi passare al report per il quale si desidera configurare un'origine dei dati specifica del report e aprirlo.  
  
3.  Fare clic sulla scheda **Proprietà** . Verrà visualizzata la pagina delle proprietà **generale** .  
  
4.  Fare clic sulla scheda **origini dati** . Verrà visualizzata la pagina delle proprietà dell'origine dati del report.  
  
5.  Fare clic su **Origine dati personalizzata** per specificare le informazioni sulla connessione all'origine dati all'interno del report.  
  
6.  Nell'elenco **Tipo di connessione** specificare l'estensione per l'elaborazione dati usata per elaborare i dati dall'origine dati.  
  
7.  Per **stringa di connessione**specificare la stringa di connessione utilizzata dal server di report per la connessione all'origine dati. È consigliabile evitare di specificare credenziali nella stringa di connessione.  
  
     Nell'esempio seguente viene illustrata una stringa di connessione per la connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] al database locale:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  Per **Connetti tramite**specificare come verranno ottenute le credenziali quando il report è in esecuzione:  
  
    -   Se si vuole richiedere all'utente un nome di accesso e una password, fare clic su **Credenziali fornite dall'utente che esegue il report**.  
  
    -   Se si prevede di usare l'origine dati con report che supportano le sottoscrizioni o altre operazioni pianificate, ad esempio la generazione della cronologia del report automatica, fare clic su **Credenziali archiviate in modo sicuro nel server di report**.  
  
    -   Se si vuole che le credenziali dell'utente che accede al report vengano passate dal server di report al server che ospita l'origine dati esterna, fare clic su **Sicurezza integrata di Windows**. In questo caso, all'utente non viene richiesto di digitare un nome utente o una password.  
  
    -   Se l'origine dati non usa credenziali (ad esempio, se l'origine dati è un file XML a cui si accede dal file system), fare clic su **Credenziali non necessarie**. È necessario specificare questo tipo di credenziali solo se l'operazione risulta valida per l'origine dati specifica. Se si seleziona questa opzione per un'origine dati che richiede l'autenticazione, la connessione non verrà stabilita. Se si seleziona questa opzione, assicurarsi inoltre di configurare l'account di esecuzione automatica che consente al server di report di connettersi agli altri computer per recuperare dati o file quando le credenziali utente non sono disponibili.  
  
 Per altre informazioni sulla configurazione delle credenziali, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](specify-credential-and-connection-information-for-report-data-sources.md). Per altre informazioni sull'account di esecuzione automatica, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina contenuti &#40;Gestione report&#41;](../contents-page-report-manager.md)   
 [Pagina nuova origine dati &#40;Gestione report&#41;](../new-data-source-page-report-manager.md)   
 [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Gestire origini dati dei report](manage-report-data-sources.md)   
 [Creare, eliminare o modificare un'origine dati condivisa &#40;Gestione report&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Pagina delle proprietà origini dati &#40;Gestione report&#41;](../data-sources-properties-page-report-manager.md)  
  
  
