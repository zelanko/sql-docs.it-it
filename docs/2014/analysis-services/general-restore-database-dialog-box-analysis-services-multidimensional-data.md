---
title: Generale (finestra di dialogo Ripristina database) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.f1
ms.assetid: 319e7ef5-c9c7-4e50-8690-02a90aed006f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ebc1bc72a15545412adcc71d10feb08f3f05b16
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080950"
---
# <a name="general-restore-database-dialog-box-analysis-services---multidimensional-data"></a>Generale (finestra di dialogo Ripristina Database) (Analysis Services - Dati multidimensionali)
  Utilizzare la pagina **Generale** della finestra di dialogo **Ripristina database** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per specificare il file di backup e le impostazioni generali da utilizzare per ripristinare un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Per ogni file di backup, l'utente che esegue il comando di ripristino deve disporre delle autorizzazioni per leggere dal percorso di backup specificato per ogni file. Per ripristinare un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non installato nel server, l'utente deve inoltre essere un membro del ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] specifica. Per sovrascrivere un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , l'utente deve avere uno dei ruoli seguenti: deve essere un membro del ruolo del server per l'istanza [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o un membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) sul database da ripristinare.  
  
> [!NOTE]  
>  Dopo avere ripristinato un database esistente, l'utente che ha effettuato l'operazione potrebbe perdere l'accesso al database ripristinato. Può verificarsi questa perdita di accesso se, al momento dell’esecuzione del backup, l'utente non era un membro del ruolo del server o non era un membro del ruolo del database con autorizzazioni Controllo completo (amministratore).  
  
 **Per visualizzare la pagina Generale nella finestra di dialogo Ripristina Database**  
  
-   In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], fare clic con il pulsante destro del mouse sulla cartella **Database** di un'istanza [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o sul database in **Esplora oggetti**, fare clic su **Ripristina**, quindi su **Seleziona una pagina**fare clic su **Generale**.  
  
## <a name="options"></a>Opzioni  
 **Script**  
 Crea uno script di ripristino basato sulle opzioni selezionate nella finestra di dialogo. Lo script di ripristino è scritto in ASSL ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Scripting Language).  
  
 Facendo clic sull'icona **Script** lo script di ripristino viene inviato in una nuova finestra Query, per impostazione predefinita.  
  
 Facendo clic sulla freccia **Script** viene visualizzato un menu che consente di scegliere dove inviare lo script di ripristino:  
  
-   A una nuova finestra Query (impostazione predefinita).  
  
-   A un file.  
  
-   Negli Appunti.  
  
-   A un processo.  
  
 **Ripristina database**  
 Consente di selezionare il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] da ripristinare.  
  
 **Da file di backup**  
 Consente di selezionare il file di backup dal quale ripristinare il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selezionato.  
  
 **Sfoglia**  
 Fare clic su questo pulsante per visualizzare la finestra di dialogo **Trova file di database** e selezionare il percorso e il nome del file di backup da usare. Per altre informazioni sulla finestra di dialogo **Trova file di database**, vedere [Finestra di dialogo Individua file di database &#40;Analysis Services - Dati multidimensionali&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Consenti sostituzione database**  
 Selezionare questa opzione per consentire a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] di ripristinare il contenuto del file di backup selezionato sostituendolo a qualsiasi oggetto esistente nel database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selezionato.  
  
 **Includi informazioni di sicurezza**  
 Selezionare questa opzione per copiare le eventuali informazioni di sicurezza archiviate nel file di backup sul database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Selezionando questa opzione viene reso disponibile un elenco a discesa che consente di scegliere la quantità di informazioni di sicurezza. Sono disponibili le opzioni seguenti:  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Copia tutto**|Ripristina i ruoli del database inclusi nel file di backup, nonché agli account utente associati ai ruoli.|  
|**Ignora appartenenze**|Ripristina i ruoli del database inclusi nel file di backup, ma non ripristina gli account utente associati ai ruoli.|  
  
 **Password**  
 Se il file di backup è crittografato, digitare la password utilizzata per crittografare il file di backup.  
  
## <a name="see-also"></a>Vedi anche  
 [Finestra di dialogo Ripristina database &#40;Analysis Services-Dati multidimensionali&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Partizioni &#40;finestra di dialogo Ripristina database&#41; &#40;Analysis Services Dati multidimensionali&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Backup e ripristino di database di Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
