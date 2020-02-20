---
title: Caricare un file o un report nel server di report | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b54290c582dab62b7e0f5b8a1cb7ca4dd2eb642c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65573304"
---
# <a name="upload-a-file-or-report-in-the-report-server"></a>Caricare un file o un report nel server di report
Il portale Web del server di report include una caratteristica di caricamento che consente di aggiungere report e altri file a un server di report senza pubblicarli da un'applicazione client. I file caricati da un file system vengono archiviati come elementi in un server di report. Il tipo di file caricato determina le modalità di archiviazione:  
  
-   I file con estensione rdl vengono archiviati come report impaginati.  
  
-   Tutti gli altri file, ad esempio i file dell'origine dati condivisa (con estensione rds), vengono caricate come risorse. Le risorse non vengono elaborate da un server di report, ma possono essere visualizzate nel portale Web se il server di report supporta il tipo MIME del file.  
  
### <a name="to-upload-a-file-or-report"></a>Per caricare un file o un report  
  
1.  Nel portale Web fare clic su **Carica**.  
  
4.  Passare al file da caricare. È possibile caricare un file di definizione del report, un'immagine, un documento o qualsiasi altro file che si desidera rendere disponibile nel server di report.  
  
5.  Digitare un nome per il nuovo elemento. Il nome di un elemento può includere spazi, ma non i seguenti caratteri riservati: \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|.  
  
6.  Se si desidera sostituire un elemento esistente con il nuovo elemento, selezionare **Sovrascrivi se esistente**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche   
[Creare, modificare ed eliminare origini dati condivise](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)
[Caricare file in una cartella](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
