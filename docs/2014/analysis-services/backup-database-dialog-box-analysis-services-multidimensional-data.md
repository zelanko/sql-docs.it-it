---
title: Finestra di dialogo Backup database (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Backup.f1
ms.assetid: 7811ce7d-6c37-4189-bfa6-ef36fb4932db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a99ce67c4b42cc1def10127c8b1862a859d20723
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66064375"
---
# <a name="backup-database-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Backup database (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Backup database** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per eseguire il backup di un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in un file di backup in formato file di backup di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con estensione abf.  
  
> [!IMPORTANT]  
>  Per ogni file di backup, l'utente che esegue il comando di backup deve disporre delle autorizzazioni per scrivere nel percorso di backup specificato per ogni file. Inoltre, l'utente deve avere uno dei ruoli seguenti: deve essere un membro di un ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oppure un membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) sul database di cui eseguire il backup.  
  
 **Per visualizzare la finestra di dialogo Backup database**  
  
-   In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sulla cartella **Database** di un'istanza [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o su un database in **Esplora oggetti**, quindi fare clic su **Backup**.  
  
## <a name="options"></a>Opzioni  
 **Script**  
 Crea uno script di backup basato sulle opzioni selezionate nella finestra di dialogo. Lo script di ripristino è scritto in ASSL ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Scripting Language).  
  
 Facendo clic sull'icona **Script** lo script di backup viene inviato in una nuova finestra Query, per impostazione predefinita.  
  
 Facendo clic sulla freccia **Script** viene visualizzato un menu che consente di scegliere dove inviare lo script di backup:  
  
-   A una nuova finestra Query (impostazione predefinita).  
  
-   A un file.  
  
-   Negli Appunti.  
  
-   A un processo.  
  
 **Database**  
 Consente di visualizzare il nome del database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] attualmente selezionato.  
  
 **File di backup**  
 Consente di digitare il percorso completo e il nome di file del file di backup da utilizzare.  
  
 **Sfoglia**  
 Fare clic su questo pulsante per visualizzare la finestra di dialogo **Salva file con nome** e selezionare il percorso e il nome di file del file di backup da usare. Per altre informazioni sulla finestra di dialogo **Salva file con nome** vedere [Finestra di dialogo Salva file con nome &#40;Analysis Services - Dati multidimensionali&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Consenti sostituzione file**  
 Selezionare questa opzione per sovrascrivere un file di backup esistente o un file di backup remoto, se disponibile.  
  
> [!NOTE]  
>  Se questa opzione non è selezionata e il file di backup specificato in file di **backup** o in un file di backup remoto specificato in **file di backup remoto** esiste, si verificherà un errore.  
  
 **Applica compressione**  
 Selezionare questa opzione per comprimere il contenuto del file di backup e dei file di backup remoti eventualmente specificati.  
  
 **Crittografa file di backup**  
 Selezionare questa opzione per crittografare il file di backup utilizzando la password specificata in **Password**.  
  
 **Password**  
 Consente di digitare la password da utilizzare per la crittografia del file di backup e dei file di backup remoti eventualmente specificati.  
  
> [!NOTE]  
>  Questa opzione è abilitata solo se è selezionato **Crittografa file di backup** .  
  
 **Conferma password**  
 Consente di digitare la password immessa in **Password** per confermare la password per il file di backup e i file di backup remoti eventualmente specificati.  
  
> [!NOTE]  
>  Questa opzione è abilitata solo se è selezionato **Crittografa file di backup** .  
  
 **Backup partizioni remote**  
 Selezionare questa opzione per includere le informazioni sulla partizione e i dati per le partizioni remote nel file di backup.  
  
> [!NOTE]  
>  Questa opzione è attivata solo se il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] attualmente selezionato utilizza partizioni remote.  
  
 **Percorso backup partizioni remote**  
 Consente di visualizzare il percorso delle partizioni remote associate al database selezionato, nonché il file di backup remoto utilizzato per il backup di dati e metadati per le partizioni remote. Sono disponibili le colonne seguenti.  
  
|Colonna|Descrizione|  
|------------|-----------------|  
|**Server**|Visualizza l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che gestisce le partizioni remote.|  
|**Database**|Visualizza il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che contiene le partizioni remote.|  
|**Elenco partizioni**|Visualizza l'elenco delle partizioni remote contenute nel database visualizzato in **Database**.|  
|**File di backup remoto**|Digitare il percorso completo e il nome di file del file di backup remoto da usare oppure fare clic sul pulsante con i puntini di sospensione (**...**) per visualizzare la finestra di dialogo **Salva file con nome** e selezionare il percorso e il nome di file del file di backup remoto da usare. Per altre informazioni sulla finestra di dialogo **Salva file con nome** vedere [Finestra di dialogo Salva file con nome &#40;Analysis Services - Dati multidimensionali&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Backup e ripristino di database di Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
