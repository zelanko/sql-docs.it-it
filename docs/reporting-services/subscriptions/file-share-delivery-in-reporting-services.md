---
title: Recapito tramite condivisione file in Reporting Services | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
ms.assetid: 9f338dd3-f68a-4355-b9d7-9b25dacf3b5e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 181f349f4dc878f0612cf6635143469c2cbe3f34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575994"
---
# <a name="file-share-delivery-in-reporting-services"></a>Recapito tramite condivisione file in Reporting Services
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include un'estensione per il recapito tramite condivisione file che consente di recapitare un report a una cartella. L'estensione per il recapito tramite condivisione file è disponibile per impostazione predefinita e non richiede alcuna operazione di configurazione. Per fare in modo che il recapito dei file abbia esito positivo, è necessario impostare autorizzazioni di accesso in scrittura sulla cartella condivisa. L'account che richiede le autorizzazioni di scrittura può avere credenziali configurate nella sottoscrizione o un **account di condivisione file** configurato per il server di report. Per altre informazioni sull'account di condivisione file, vedere [Impostazioni di sottoscrizione e un account di condivisione file &#40;Gestione configurazione&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md). Inoltre, gli utenti che richiedono l'accesso ai report devono disporre di autorizzazioni in lettura per la cartella condivisa.  
  
 Per distribuire un report a una condivisione file, è necessario definire una sottoscrizione standard oppure una sottoscrizione guidata dai dati. Per informazioni su come usare il recapito tramite condivisione file in una sottoscrizione guidata dai dati, vedere [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md). L'account che esegue sottoscrizioni con recapito tramite condivisione di file remote deve disporre dei diritti necessari per accedere in locale nel computer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
  
 **Contenuto dell'argomento:**  
  
-   [Report di caratteristiche recapitati alle cartelle condivise](#bkmk_Characteristics)  
  
-   [Cartelle di destinazione](#bkmk_target_folders)  
  
-   [Formati di file](#bkmk_file_formats)  
  
-   [Opzioni relative ai file](#bkmk_file_options)  
  
##  <a name="bkmk_Characteristics"></a> Report di caratteristiche recapitati alle cartelle condivise  
  
-   A differenza dei report che sono ospitati e gestiti in un server di report, i report che vengono recapitati a una cartella condivisa sono file statici.  
  
-   Le funzionalità interattive definite per il report **non funzionano** per i report archiviati come file nel file system. e sono rappresentate come elementi statici. Se ad esempio si recapita un report matrice, nel file risultante sarà riportata la visualizzazione di livello principale del report e non sarà possibile espandere righe e colonne per visualizzare i dati sottostanti.  
  
-   Se il report include grafici, viene utilizzato il formato di visualizzazione predefinito. Se il report è collegato a un altro report, il collegamento viene rappresentato come testo statico.  
  
-   Se si desidera mantenere le funzionalità interattive in un report recapitato, utilizzare il recapito tramite posta elettronica. Il messaggio di posta elettronica contiene un collegamento al report nel server di report e gli utenti possono usare le funzionalità interattive. Per altre informazioni, vedere [Recapito tramite posta elettronica in Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
##  <a name="bkmk_target_folders"></a> Cartelle di destinazione  
 Quando si definisce una sottoscrizione che utilizza il recapito tramite condivisione file, è necessario specificare una cartella esistente come cartella di destinazione. Il server di report non crea automaticamente cartelle nel file system. La cartella specificata deve essere accessibile su una connessione di rete.  
  
 Verificare che gli utenti che **visualizzeranno** i report presenti nella cartella condivisa abbiano l'autorizzazione di lettura.  
  
 Quando si specifica la cartella di destinazione in una sottoscrizione utilizzare il formato UNC (Uniform Naming Convention) in modo da includere il nome di rete del computer. Non includere barre rovesciate finali nel percorso della cartella. Nell'esempio seguente viene illustrato un percorso UNC:  
  
```  
\\<servername>\reportarchive\operations\2014  
```  
  
 Quando si crea la cartella, considerare i limiti della connessione richiesti. Per il server di report sono necessarie due connessioni, ma è necessario includere un numero sufficiente di connessioni per consentire ad altri utenti di visualizzare i report nella cartella condivisa.  
  
##  <a name="bkmk_file_formats"></a> Formati di file  
 Il rendering dei report può essere eseguito in vari formati di file, ad esempio HTML, DOCX ed Excel. Per salvare il report in un formato di file specifico, selezionare il formato di rendering desiderato al momento della creazione della sottoscrizione. Se, ad esempio, si sceglie **Excel** , il report viene salvato come file di [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] . Sebbene sia possibile selezionare qualsiasi formato di rendering supportato, alcuni formati risultano più appropriati quando si esegue il rendering in un file.  
  
 Se si utilizza il recapito tramite condivisione file, scegliere un formato che consenta di recapitare il report in un singolo file e di includere nel report tutte le immagini e il contenuto correlato. I formati adatti a questo scopo sono Archivio Web, PDF, TIFF ed Excel. Evitare il formato HTML4.0. Se nel report sono presenti immagini, queste non verranno incluse nel file se si utilizza il formato HTML 4.0.  
  
##  <a name="bkmk_file_options"></a> Opzioni relative ai file  
 Quando si crea una sottoscrizione di condivisione file, è possibile configurare la modalità di creazione del nome file e se il file sovrascrive le versioni precedenti del report. Un nome file completo è costituito da tre parti, ovvero il nome, l'estensione e un testo o un numero aggiunto al file per creare un nome file univoco  
  
 **Nome file** : il nome file predefinito è basato sul nome del report di origine, tuttavia è possibile specificare un nome personalizzato nella sottoscrizione. L'estensione è facoltativa. Se specificata, il server di report creerà un'estensione corrispondente al formato di rendering.  
  
 **Sovrascrittura:** è possibile specificare le opzioni di sovrascrittura per riusare lo stesso nome file per tutti i recapiti di report oppure per creare un nuovo file. Per sovrascrivere il file, è necessario utilizzare lo stesso nome file e la stessa estensione.  
  
 Un modo alternativo per creare file univoci per ogni recapito consiste nell'includere un timestamp nel nome file. A tale scopo, aggiungere la variabile **@timestamp** al nome file, ad esempio *CompanySales@timestamp* . In tal modo il nome file sarà univoco per definizione e non verrà mai sovrascritto.  
  
 L'immagine seguente riporta un esempio delle impostazioni per una sottoscrizione configurata per il recapito della condivisione file.  
  
 ![sottoscrizione di condivisione di file](../../reporting-services/subscriptions/media/ssrs-file-share-subscription.png "sottoscrizione di condivisione di file")  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire sottoscrizioni per server di report in modalità nativa](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Impostazioni di sottoscrizione e un account di condivisione file &#40;Gestione configurazione&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)  
  
  
