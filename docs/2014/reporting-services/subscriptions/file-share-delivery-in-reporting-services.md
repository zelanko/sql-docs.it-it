---
title: Recapito tramite condivisione file in Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
ms.assetid: 9f338dd3-f68a-4355-b9d7-9b25dacf3b5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d3d042530f69d34fde377ffc7c6e0a9200b9cc48
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100912"
---
# <a name="file-share-delivery-in-reporting-services"></a>Recapito tramite condivisione file in Reporting Services
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include un'estensione per il recapito tramite condivisione file che consente di recapitare un report a una cartella. L'estensione per il recapito tramite condivisione file è disponibile per impostazione predefinita e non richiede alcuna operazione di configurazione. Per fare in modo che il recapito dei file abbia esito positivo, è necessario impostare autorizzazioni di accesso in scrittura sulla cartella condivisa. Inoltre, gli utenti che richiedono l'accesso ai report devono disporre di autorizzazioni in lettura per la cartella condivisa.  
  
 Per distribuire un report a una condivisione file, è necessario definire una sottoscrizione standard oppure una sottoscrizione guidata dai dati. È possibile eseguire la sottoscrizione e richiedere il recapito di un solo report alla volta. Per informazioni su come usare il recapito tramite condivisione file in una sottoscrizione guidata dai dati, vedere [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md). L'account che esegue sottoscrizioni con recapito tramite condivisione di file remote deve disporre dei diritti necessari per accedere in locale nel computer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modalità SharePoint|  
  
 In questo argomento  
  
-   [Caratteristiche di un report recapitato a una cartella condivisa](#bkmk_Characteristics)  
  
-   [Cartelle di destinazione](#bkmk_target_folders)  
  
-   [Formati di file](#bkmk_file_formats)  
  
-   [Opzioni relative ai file](#bkmk_file_options)  
  
##  <a name="characteristics-of-a-report-that-is-delivered-to-a-shared-folder"></a><a name="bkmk_Characteristics"></a>Caratteristiche di un report recapitato a una cartella condivisa  
 A differenza dei report che sono ospitati e gestiti in un server di report, i report che vengono recapitati a una cartella condivisa sono file statici. Le funzionalità interattive definite per il report non possono essere utilizzate per report archiviati come file nel file system e sono rappresentate come elementi statici. Se ad esempio si recapita un report matrice, nel file risultante sarà riportata la visualizzazione di livello principale del report e non sarà possibile espandere righe e colonne per visualizzare i dati sottostanti. Se il report include grafici, viene utilizzato il formato di visualizzazione predefinito. Se il report è collegato a un altro report, il collegamento viene rappresentato come testo statico. Se si desidera mantenere le funzionalità interattive in un report recapitato, utilizzare il recapito tramite posta elettronica. Per altre informazioni, vedere [Recapito tramite posta elettronica in Reporting Services](e-mail-delivery-in-reporting-services.md).  
  
##  <a name="target-folders"></a><a name="bkmk_target_folders"></a>Cartelle di destinazione  
 Quando si definisce una sottoscrizione che utilizza il recapito tramite condivisione file, è necessario specificare una cartella esistente come cartella di destinazione. Il server di report non crea automaticamente cartelle nel file system. La cartella specificata deve essere accessibile su una connessione di rete.  
  
 Verificare che gli utenti che visualizzeranno i report presenti nella cartella condivisa abbiano l'autorizzazione di lettura.  
  
 Quando si specifica la cartella di destinazione in una sottoscrizione utilizzare il formato UNC (Uniform Naming Convention) in modo da includere il nome di rete del computer. Non includere barre rovesciate finali nel percorso della cartella. Nell'esempio seguente viene illustrato un percorso UNC:  
  
```  
\\<servername>\reportarchive\operations\2003  
```  
  
 Quando si crea la cartella, considerare i limiti della connessione richiesti. Per il server di report sono necessarie due connessioni, ma è necessario includere un numero sufficiente di connessioni per consentire ad altri utenti di visualizzare i report nella cartella condivisa.  
  
##  <a name="file-formats"></a><a name="bkmk_file_formats"></a> Formati di file  
 Il rendering dei report può essere eseguito in vari formati di file, ad esempio HTML o Excel. Per salvare il report in un formato di file specifico, selezionare il formato di rendering desiderato al momento della creazione della sottoscrizione. Se, ad esempio, si sceglie **Excel** , il report viene salvato come file di [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] . Sebbene sia possibile selezionare qualsiasi formato di rendering supportato, alcuni formati risultano più appropriati quando si esegue il rendering in un file.  
  
 Se si utilizza il recapito tramite condivisione file, scegliere un formato che consenta di recapitare il report in un singolo file e di includere nel report tutte le immagini e il contenuto correlato. I formati adatti a questo scopo sono Archivio Web, PDF, TIFF ed Excel. Evitare il formato HTML 4.0. Se nel report sono presenti immagini, queste non verranno incluse nel file se si utilizza il formato HTML 4.0.  
  
##  <a name="file-options"></a><a name="bkmk_file_options"></a> Opzioni relative ai file  
 Quando si crea una sottoscrizione, è possibile scegliere le opzioni che determinano la modalità di creazione del nome file e se il file verrà sostituito di volta in volta dalle versioni più recenti. Un nome di file completo è costituito da tre parti, ovvero il nome, l'estensione e un testo o un numero aggiunto al file per creare un nome di file univoco. Le opzioni di sovrascrittura determinano se il testo o il numero viene aggiunto al nome del file.  
  
 Il nome file è basato sul nome del report, tuttavia è possibile specificare un nome personalizzato nella sottoscrizione. L'estensione è facoltativa. Se specificata, il server di report creerà un'estensione corrispondente al formato di rendering.  
  
 È possibile specificare le opzioni di sovrascrittura per riutilizzare lo stesso nome file per tutti i recapiti di report oppure per creare un nuovo file. Per sovrascrivere il file, è necessario utilizzare lo stesso nome file e la stessa estensione.  
  
 Un modo alternativo per creare file univoci per ogni recapito consiste nell'includere un timestamp nel nome file. A tale scopo, aggiungere la variabile `@timestamp` al nome file, ad esempio *CompanySales@timestamp*. In tal modo il nome file sarà univoco per definizione e non verrà mai sovrascritto.  
  
## <a name="see-also"></a>Vedi anche  
 [Creare, modificare ed eliminare sottoscrizioni standard &#40;Reporting Services in modalità nativa&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
