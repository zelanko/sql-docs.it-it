---
title: Le partizioni remote - finestra di dialogo Impostazioni (Analysis Services - dati multidimensionali) avanzate | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.advancedrestoresettings.f1
ms.assetid: a03bb7e1-efaf-47c8-b0ee-f3e4438311cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ca3f12ff53c4291d8bbe7c8eb97ce8e47172ea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070377"
---
# <a name="remote-partitions---advanced-settings-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Partizioni remote – Impostazioni avanzate (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Partizioni remote - Impostazioni avanzate** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per modificare le impostazioni avanzate, quali la stringa di connessione dell'origine dati che rappresenta il database remoto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che gestisce le partizioni remote, durante il ripristino di partizioni remote da un file di backup remoto in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tramite la finestra di dialogo **Ripristina database**. Per visualizzare la finestra di dialogo **Partizioni remote - Impostazioni avanzate** dalla pagina **Partizioni** della finestra di dialogo **Ripristina database** , è possibile fare clic sul pulsante con i puntini di sospensione ( **...** ) per una partizione remota dopo aver selezionato l'opzione **Ripristina partizioni remote** .  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Nome origine dati**|Consente di visualizzare il nome dell'origine dei dati che rappresenta il database remoto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che gestisce le partizioni remote elencate.|  
|**File di backup**|Consente di visualizzare il nome del file di backup remoto che contiene i dati da ripristinare per le partizioni remote elencate.<br /><br /> Nota: Viene visualizzato alcun file di backup se è stato specificato un file di backup remoto nel **file di Backup** colonna sul **partizioni** pagina del **Restore Database** nella finestra di dialogo.|  
|**Stringa di connessione**|Consente di visualizzare la stringa di connessione per l'origine dati visualizzata in **Nome origine dati**.|  
|**Modifica**|Fare clic su questo pulsante per visualizzare la finestra di dialogo **Proprietà di Data Link** e modificare le proprietà contenute nella stringa di connessione.|  
|**Elenco partizioni**|Selezionare questa opzione per specificare percorsi diversi in cui ripristinare le partizioni remote. Si noti che è possibile modificare solo la cartella di ripristino di una partizione remota nel caso in cui sia stato specificato un percorso diverso dal percorso predefinito per tale partizione remota nel cubo. Quando si seleziona questa opzione, viene attivata la griglia seguente che consente di specificare una cartella di ripristino per ogni partizione remota:<br /><br /> **Cubo**: Consente di visualizzare il nome del cubo contenente la partizione remota.<br /><br /> **MeasureGroup**: Consente di visualizzare il nome del gruppo di misure contenente la partizione remota.<br /><br /> **Partizione**: Consente di visualizzare il nome della partizione remota.<br /><br /> **Dimensioni (MB)** : Consente di visualizzare le dimensioni in megabyte della partizione remota.<br /><br /> **Cartella originale**: Consente di visualizzare il nome della cartella originale in cui è stata archiviata la partizione remota.<br /><br /> **Cartella ripristino**: Digitare il nome della cartella di ripristino per la partizione remota oppure fare clic sul pulsante con i puntini di sospensione ( **...** ) per visualizzare la finestra di dialogo **Cerca cartella remota** e selezionare il percorso della cartella da usare. Per altre informazioni sulla finestra di dialogo **Cerca cartella remota**, vedere [Finestra di dialogo Cerca cartella remota &#40;Analysis Services - Dati multidimensionali&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Partizioni &#40;dialogo Ripristina Database&#41; &#40;Analysis Services - dati multidimensionali&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Backup e ripristino di database di Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
