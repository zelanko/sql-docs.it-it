---
title: Dialogo Ripristina Database (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Restore.f1
ms.assetid: a3990d47-55e2-424e-8eac-87edc937e806
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42649fd9fe8284e89aebd37c2d9b668a3ac34a2f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070256"
---
# <a name="restore-database-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Ripristina Database (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Ripristina database** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per ripristinare un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] da un file di backup usando il formato file di backup di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con estensione abf.  
  
> [!IMPORTANT]  
>  Per ogni file di backup, l'utente che esegue il comando di ripristino deve disporre delle autorizzazioni per leggere dal percorso di backup specificato per ogni file. Per ripristinare un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non installato nel server, l'utente deve inoltre essere un membro del ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] specifica. Per sovrascrivere un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , l'utente deve avere uno dei ruoli seguenti: deve essere un membro del ruolo del server per l'istanza [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o un membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) per il database da ripristinare.  
  
> [!NOTE]  
>  Dopo avere ripristinato un database esistente, l'utente che ha effettuato l'operazione potrebbe perdere l'accesso al database ripristinato. Può verificarsi questa perdita di accesso se, al momento dell’esecuzione del backup, l'utente non era un membro del ruolo del server o non era un membro del ruolo del database con autorizzazioni Controllo completo (amministratore).  
  
 **Per visualizzare la finestra di dialogo Ripristina Database**  
  
-   In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], fare clic con il pulsante destro del mouse sulla cartella **Database** di un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o su un database in **Esplora oggetti**e quindi fare clic su **Ripristina**.  
  
 La finestra di dialogo **Ripristina database** include le seguenti pagine.  
  
## <a name="pages"></a>Pages  
 **Generale**  
 Utilizzare questa pagina per selezionare il database da ripristinare, il file di backup dal quale eseguire il ripristino del database, le opzioni generali e la password da utilizzare per il ripristino del database. Per altre informazioni su questa pagina, vedere [Generale &#40;finestra di dialogo Ripristina database&#41; &#40;Analysis Services - Dati multidimensionali&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Partizioni**  
 Utilizzare questa pagina per ripristinare le partizioni locali nei percorsi specificati e per ripristinare le partizioni remote da file di backup remoti. Per altre informazioni su questa pagina, vedere [Partizioni &#40;finestra di dialogo Ripristina database&#41; &#40;Analysis Services - Dati multidimensionali&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Backup e ripristino di database di Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
