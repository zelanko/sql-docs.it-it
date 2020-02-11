---
title: Finestra di dialogo Proprietà origine dati, generale (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10018"
ms.assetid: b956f43a-8426-4679-acc1-00f405d5ff5b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7bedf016dce02928bbd47dbfce60943ec667a824
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109465"
---
# <a name="data-source-properties-dialog-box-general-report-builder"></a>Finestra di dialogo Proprietà origine dati, Generale (Generatore report)
  Selezionare **Generale** nella finestra di dialogo **Proprietà origine dati** per selezionare un'origine dati condivisa in un server di report o modificare le informazioni di connessione per un'origine dati incorporata nel report.  
  
 Il tipo di credenziali utilizzate per la connessione a un'origine dati è specificato nelle proprietà dell'origine dati. Quando si apre un report dal server di report, è possibile che le credenziali di run-time, specificate nelle proprietà dell'origine dati, non funzionino per le attività della fase di progettazione, quali la creazione di query e la visualizzazione in anteprima di report. L'origine dati, ad esempio, potrebbe utilizzare credenziali di Windows diverse da quelle in uso o un nome utente e una password non noti.  
  
 In Generatore report viene aperta la finestra di dialogo **Immetti credenziali origine dei dati** quando non è possibile connettersi all'origine dati tramite le credenziali fornite nelle proprietà dell'origine dati. Questa situazione si verifica quando:  
  
-   L'origine dati è configurata per richiedere le credenziali.  
  
-   L'origine dati è configurata per utilizzare le credenziali archiviate.  Per ridurre al minimo le potenziali minacce per la sicurezza, Generatore report è progettato in modo da non recuperare le credenziali archiviate nel server.  
  
 È possibile utilizzare la finestra di dialogo **Immetti credenziali origine dei dati** per modificare le credenziali utilizzate da Generatore report in fase di progettazione per la connessione all'origine dati come utente di Windows corrente o per fornire un nome utente e una password. Se si forniscono un nome utente e una password, è possibile indicare se questi dati vengono utilizzati come credenziali di Windows.  
  
> [!NOTE]  
>  Benché gli strumenti di progettazione query consentano di specificare un altro tipo di credenziali come credenziali della fase di progettazione, l'anteprima dei report consente di immettere il nome utente e la password solo per le opzioni di credenziali esistenti specificate nell'origine dati.  
  
 Quando si fa clic su **Test connessione**, viene testata la connessione all'origine dati utilizzando le credenziali specificate nella pagina delle credenziali delle proprietà per l'origine dati. È possibile testare connessioni a origini dati incorporate e condivise.  
  
 Se le credenziali specificate sono incomplete, ad esempio se è necessaria una password, in Generatore report vengono nuovamente richieste le credenziali della fase di progettazione quando è necessario connettersi all'origine dati. Le credenziali della fase di progettazione vengono archiviate e non vengono più richieste.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare il nome dell'origine dati. Tale nome deve essere univoco all'interno del report. Per impostazione predefinita, all'origine dei dati viene assegnato un nome generico, ad esempio DataSource1 o DataSource2.  
  
 **Usa una connessione condivisa**  
 Selezionare questa opzione per individuare un'origine dei dati condivisa pubblicata in un server di report.  
  
 Dopo aver selezionato un'origine dati in un server di report, in Generatore report viene mantenuta una connessione a tale server di report specifico.  
  
 **Usa una connessione incorporata nel report.**  
 Selezionare questa opzione per creare un'origine dei dati da utilizzare solo per il report specifico.  
  
 **Tipo**  
 Selezionare un'estensione per l'elaborazione dei dati. Nell'elenco vengono visualizzate tutte le estensioni registrate.  
  
 **Stringa di connessione**  
 Immettere una stringa di connessione per l'origine dati. Fare clic su **Compila** per compilare la stringa di connessione utilizzando la finestra di dialogo **Proprietà connessione** . Fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione.  
  
 **Usa transazione singola durante l'elaborazione delle query**  
 Selezionare questa opzione per indicare che i set di dati che utilizzano l'origine dei dati vengono eseguiti in un'unica transazione sul database. Per includere transazioni per sottoreport che utilizzano la stessa origine dati, selezionare il sottoreport quindi impostare **MergeTransactions** su **True**nel riquadro Proprietà.  
  
 **Test connessione**  
 Fare clic su questa opzione per verificare che la connessione all'origine dati funzioni correttamente tramite le credenziali specificate. Se non è possibile stabilire la connessione, è necessario verificare le credenziali e la disponibilità del server. È possibile testare connessioni a origini dati incorporate e condivise.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore report e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Finestra di dialogo Proprietà origine dati, credenziali &#40;Generatore report&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md)   
 [Guida Generatore report per finestre di dialogo, riquadri e procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
