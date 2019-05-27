---
title: Pagina Carica File (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7bb3166f-9374-4449-b66a-ffb77298507d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1100baa3cd72a04d208b2076d91ca4efed7d38e6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098870"
---
# <a name="upload-file-page-report-manager"></a>Pagina Carica file (Gestione report)
  La pagina Carica file consente di pubblicare un file dal file system nel database del server di report. I file caricati vengono rappresentati come elementi nella gerarchia di cartelle del server di report.  
  
-   I file con estensione rdl caricati vengono pubblicati come report in un server di report.  
  
-   I file caricati con estensione smdl vengono pubblicati come modelli di report se includono informazioni sulla vista origine dati. Se tali file non contengono alcun riferimento alla vista origine dati, si verificherà un errore durante il caricamento. È possibile che le informazioni sulla vista origine dati non siano presenti nei file con estensione smdl caricati da un progetto modello di report di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . Nei progetti modello di report le informazioni relative alla vista origine dati vengono archiviate in un file separato anziché direttamente nel file con estensione smdl.  
  
     I file modello che contengono informazioni sulla vista origine dati, e che pertanto è possibile caricare, sono i file che sono stati pubblicati in precedenza in un server di report, quindi salvati in un file nel file system. Se si apre la pagina delle proprietà Generale di un modello e si fa clic su **Modifica** per aprire il modello, è possibile salvarlo in un file e quindi caricare il file come nuovo modello nel server di report. Nel file con estensione smdl caricato successivamente saranno disponibili tutte le informazioni necessarie per la pubblicazione del modello.  
  
-   Tutti gli altri tipi di file caricati vengono archiviati come risorse, inclusi i file con estensione rds che contengono informazioni di connessione all'origine dati del report. Il caricamento di un file rds non comporta la creazione di un'origine dei dati condivisa nel server di report.  
  
 Quando si carica un elemento, questo viene inserito nella cartella corrente. Dopo il caricamento, l'elemento può essere spostato in percorsi diversi.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-upload-file-page"></a>Per aprire la pagina Carica file  
  
1.  Aprire Gestione report e navigare fino alla cartella in cui si desidera caricare un file.  
  
2.  Nella barra degli strumenti fare clic su **Carica file**.  
  
## <a name="options"></a>Opzioni  
 **File da caricare**  
 Consente di visualizzare il percorso completo del file copiato dal file system.  
  
 **Sfoglia**  
 Fare clic per selezionare un file nel file system.  
  
 **Name**  
 Consente di digitare il nome del file nel modo in cui si desidera venga visualizzato nello spazio dei nomi del server di report. Il nome deve includere almeno un carattere alfanumerico. È inoltre possibile utilizzare spazi e alcuni simboli. Non utilizzare i caratteri ; ? : \@ & = +, $ * \< > | "oppure / per specificare il nome di un elemento.  
  
 **Sovrascrivi se esistente**  
 Selezionare questa casella di controllo se si desidera sostituire un elemento esistente con una versione più recente. Per sovrascrivere la versione esistente è necessario che i nomi del nuovo elemento e dell'elemento esistente siano identici.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Pagina Contenuto &#40;Gestione report&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Guida F1 di gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Caricare file in una cartella](report-server/upload-files-to-a-folder.md)  
  
  
