---
title: Specificare le credenziali in Generatore Report | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 7412ce68-aece-41c0-8c37-76a0e54b6b53
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 32bd106320c8969813dbae107a7569af8560aba4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956067"
---
# <a name="specify-credentials-in-report-builder"></a>Specifica di credenziali in Generatore report
  Le credenziali consentono di autenticare l'utente che tenta di recuperare dati da un'origine dati. Il proprietario dell'origine dati determina il tipo di credenziali che è necessario usare. Ad esempio, un amministratore di database può specificare che l'utente deve fornire un nome utente e una password di Windows.  
  
 In una definizione di report ogni definizione di origine dati specifica un nome, una stringa di connessione, se usare la sicurezza integrata e il tipo di prompt da visualizzare se le credenziali sono richieste ma non sono state specificate. Le credenziali non vengono salvate nella definizione del report. Dopo la pubblicazione di un report nel server di report, le origini dati possono essere gestite indipendentemente dalla definizione del report. I proprietari delle origini dati possono specificare le credenziali per origini dati incorporate e condivise nel server di report.  
  
> [!NOTE]  
>  L'amministratore del server di report deve concedere a un utente le autorizzazioni appropriate per esplorare il server di report in modo da selezionare origini dati condivise o modelli o da aprire o salvare report. Per altre informazioni, vedere [di installazione, disinstallazione e supporto di Generatore Report](../../2014/reporting-services/install-uninstall-and-report-builder-support.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-when-credentials-are-used"></a>Informazioni sulle condizioni che comportano l'utilizzo di credenziali  
 In Generatore report le credenziali vengono spesso usate quando ci si connette a un server di report o per attività correlate a dati, ad esempio la creazione di un'origine dati incorporata, l'esecuzione di una query del set di dati o la visualizzazione in anteprima di un report. Le credenziali non vengono archiviate nel report. Esse vengono gestite separatamente nel server di report o nel client locale. Nell'elenco seguente vengono descritti i tipi di credenziali che potrebbe essere necessario fornire, dove sono archiviati e come vengono usati:  
  
-   Le credenziali del server di report immesse nella [Finestra di dialogo Accesso a Reporting Services &#40;Generatore report&#41;](report-builder/reporting-services-login-dialog-box-report-builder.md).  
  
     Quando si salva, si pubblica su o si passa a un server di report o a un sito di SharePoint, potrebbe essere necessario immettere le proprie credenziali. Le credenziali immesse verranno usate fino alla fine della sessione di Generatore report. Se si sceglie di salvare le credenziali, esse vengono archiviate in modo sicuro con le impostazioni utente nel computer. Nelle sessioni di Generatore report successive, le credenziali salvate vengono usate per connettersi allo stesso server di report o sito di SharePoint. L'amministratore del server di report o di SharePoint specifica quale tipo di credenziali usare.  
  
-   Le credenziali dell'origine dati immesse nella pagina [Finestra di dialogo Proprietà origine dati, Credenziali &#40;Generatore report&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md) per un'origine dati incorporata.  
  
     Queste credenziali vengono usate dal server di report per stabilire una connessione dati all'origine dati esterna. Per alcuni tipi di origini dati, le credenziali possono essere archiviate in modo sicuro nel server di report. Queste credenziali consentono ad altri utenti di eseguire il report senza fornire credenziali per la connessione dati sottostante.  
  
-   Le credenziali dell'origine dati immesse nella [Finestra di dialogo Immetti credenziali origine dei dati&#40;Generatore Report&#41;](report-data/enter-data-source-credentials-dialog-box-report-builder.md) quando si esegue una query del set di dati, si aggiornano i campi del set di dati o si visualizza in anteprima il report.  
  
     Queste credenziali vengono usate per stabilire una connessione dati da Generatore report e l'origine dati esterna o per visualizzare in anteprima un report configurato per la richiesta di credenziali. Le credenziali che si immettono in questa finestra di dialogo non sono archiviate nel server di report e non sono disponibili per l'utilizzo da parte di altri utenti. Generatore report memorizza nella cache le credenziali durante la sessione di modifica del report in modo che non sia necessario immetterle ogni volta che si esegue la query o si visualizza in anteprima il report.  
  
     Per le origini dati condivise, usare l'opzione **Salva password** per salvare in locale le credenziali con le impostazioni utente nel computer. Generatore report usa le credenziali salvate ogni volta che viene stabilita una connessione all'origine dati esterna corrispondente.  
  
 Per altre informazioni, vedere [Finestra di dialogo Proprietà origine dati, Generale &#40;Generatore report&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md) e [Anteprima di report in Generatore report](report-builder/previewing-reports-in-report-builder.md).  
  
## <a name="types-of-credentials"></a>Tipi di credenziali  
 Il tipo di credenziali supportato da un'origine dati è specificato dal relativo proprietario. Ad esempio, per accedere a un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , può essere necessario specificare un nome utente e una password di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per accedere a un'origine dati diversa, può essere necessario specificare un nome utente e una password di Windows. In alcuni casi, è possibile che l'origine dati non richieda credenziali.  
  
### <a name="options-for-specifying-credentials"></a>Opzioni per la specifica di credenziali  
 Per specificare credenziali per un'origine dati, sono disponibili le opzioni seguenti:  
  
-   Usare l'utente di Windows corrente (nota anche come sicurezza integrata).  
  
-   Utilizzare un nome utente e una password archiviati.  
  
-   Richiedere all'utente le credenziali.  
  
-   Non sono necessarie credenziali.  
  
### <a name="windows-integrated-security"></a>Sicurezza integrata di Windows  
 Quando si seleziona **Usa autenticazione di Windows (sicurezza integrata)**, il token di sicurezza dell'utente corrente viene passato all'origine dati. In questo caso, all'utente non viene richiesto di digitare un nome utente o una password. Questa opzione richiede in genere che le caratteristiche di delega siano abilitate. In caso contrario, è possibile usare questa opzione solo per accedere a un'origine dati disponibile nello stesso computer.  
  
### <a name="user-name-and-password-login"></a>Accesso tramite nome utente e password  
 Quando si seleziona **Usa il nome utente e la password seguenti**, è necessario specificare un nome utente e una password per accedere all'origine dati. Per un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , le credenziali possono essere relative a un account di accesso al database. Le credenziali vengono passate all'origine dati per l'autenticazione.  
  
### <a name="prompted-credentials"></a>Credenziali fornite dall'utente  
 Quando si specifica di richiedere le credenziali, ogni utente che accede al report deve immettere un nome utente e una password per recuperare i dati. Questa opzione è consigliata per i report contenenti dati riservati. Le credenziali fornite dall'utente possono essere relative a un account di Windows o a un account di accesso al database. Se il server di database non riconosce le credenziali fornite o se l'utente specificato non dispone dell'autorizzazione per il recupero dei dati, la connessione non riesce.  
  
### <a name="no-credentials"></a>Connessioni senza credenziali  
 Le credenziali non sono richieste per questa origine dati. Per eseguire questo report nel server di report, è necessario configurare l'account di esecuzione automatica. Per altre informazioni, vedere [configurare l'Account di esecuzione automatica &#40;Gestione configurazione SSRS&#41; ](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) nel [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nella documentazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [documentazione Online di](https://go.microsoft.com/fwlink/?linkid=121312).  
  
## <a name="see-also"></a>Vedere anche  
 [Installare, disinstallare e supporto di Generatore Report](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)   
 [Connessioni dati o origini dati incorporate e condivise &#40;Generatore report e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Finestra di dialogo, le impostazioni di opzioni di Generatore report &#40;Generatore Report&#41;](report-builder/set-default-options-for-report-builder.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Aggiungere e verificare una connessione dati o un'origine dati &#40;Report e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
  
