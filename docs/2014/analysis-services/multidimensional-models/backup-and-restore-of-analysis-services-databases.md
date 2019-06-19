---
title: Backup e ripristino di database di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.Backup.f1
- sql12.asvs.ssmsimbi.Restore.f1
helpviewer_keywords:
- backing up databases [Analysis Services]
- encryption [Analysis Services]
- databases [Analysis Services], restoring
- cryptography [Analysis Services]
- databases [Analysis Services], backing up
- restoring databases [Analysis Services]
- recovery [Analysis Services]
ms.assetid: 947eebd2-3622-479e-8aa6-57c11836e4ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f591a5a8c8099e496c10958b43694e98ae7a24b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077025"
---
# <a name="backup-and-restore-of-analysis-services-databases"></a>Backup e ripristino di database di Analysis Services
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è disponibile una funzionalità di backup e ripristino per poter eseguire il recupero temporizzato di un database e dei relativi oggetti. Tale funzionalità rappresenta anche una tecnica valida per l'esecuzione della migrazione dei database a server aggiornati, per lo spostamento di database tra server o per la distribuzione di un database in un server di produzione. Per il recupero dei dati, se non è già disponibile un piano di backup per i dati importanti, è consigliabile progettarlo e implementarlo appena possibile.  
  
 I comandi di backup e ripristino vengono eseguiti su un database di Analysis Services distribuito. Per progetti e soluzioni disponibili in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], è necessario utilizzare il controllo del codice sorgente per assicurarsi di poter recuperare versioni specifiche dei file di origine e quindi creare un piano di recupero dati per il repository del sistema di controllo del codice sorgente che si utilizza.  
  
 Per ottenere un backup completo in cui siano inclusi i dati di origine, è necessario eseguire il backup del database contenente i dati di dettaglio. In particolare, se si utilizza l'archiviazione di database ROLAP o DirectQuery, i dati di dettaglio vengono archiviati in un database relazionale di SQL Server esterno che è diverso dal database di Analysis Services. In alternativa, se tutti gli oggetti sono tabulari o multidimensionali, nel backup di Analysis Services saranno inclusi sia i metadati che i dati di origine.  
  
 Un vantaggio ovvio dell'automazione del backup consiste nel fatto che lo snapshot dei dati verrà sempre aggiornato in base alla frequenza corrispondente specificata. L'esecuzione dei backup è garantita dalle utilità di pianificazione automatizzate. È inoltre possibile automatizzare il ripristino di un database, ottenendo in tal modo una strategia valida per la replica dei dati, ma è necessario verificare che sia stato eseguito il backup del file della chiave di crittografia nell'istanza in cui si esegue la replica. La funzionalità di sincronizzazione è riservata alla replica dei database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ma solo per i dati non aggiornati. È possibile implementare tutte le caratteristiche sopra indicate tramite l'interfaccia utente, mediante comandi XML/A o l'esecuzione a livello di programmazione nella libreria AMO.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
-   [Preparazione del backup](#bkmk_prep)  
  
-   [Backup di un database multidimensionale o tabulare](#bkmk_cube)  
  
-   [Ripristino di un database di Analysis Services](#bkmk_restore)  
  
##  <a name="bkmk_prereq"></a> Prerequisiti  
 È necessario avere autorizzazioni amministrative sull'istanza di Analysis Services o autorizzazioni Controllo completo (amministratore) sul database di cui si sta eseguendo il backup.  
  
 Il percorso di ripristino deve essere un'istanza di Analysis Services che è la stessa versione, o una versione più recente, dell'istanza da cui è stato eseguito il backup. Anche se non è possibile ripristinare un database da un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a una versione precedente di Analysis Services, è pratica comune ripristinare un database della versione precedente, ad esempio SQL Server 2012, in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] più recente.  
  
 Il percorso di ripristino deve essere lo stesso tipo di server. È possibile ripristinare database tabulari solo in Analysis Services in esecuzione in modalità tabulare. Per i database multidimensionali è richiesta un'istanza in esecuzione in modalità multidimensionale.  
  
##  <a name="bkmk_prep"></a> Preparazione del backup  
 Per la preparazione del backup utilizzare il seguente elenco di controllo:  
  
-   Controllare il percorso in cui verrà archiviato il file di backup. Se si utilizza un percorso remoto, è necessario specificarlo come cartella UNC. Verificare che sia possibile accedere al percorso UNC.  
  
-   Controllare le autorizzazioni sulla cartella per assicurarsi che l'account del servizio Analysis Services disponga di autorizzazioni di lettura/scrittura sulla cartella.  
  
-   Verificare che lo spazio su disco sul server di destinazione sia sufficiente.  
  
-   Verificare la presenza di file con lo stesso nome. Se esiste già un file con lo stesso nome, il backup non riuscirà a meno che non si specificano le opzioni per sovrascrivere il file.  
  
##  <a name="bkmk_cube"></a> Backup di un database multidimensionale o tabulare  
 Gli amministratori possono eseguire il backup di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un singolo file di backup (con estensione abf) di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , indipendentemente dalle dimensioni del database. Per istruzioni dettagliate, vedere [come eseguire il backup di un database di Analysis Services (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Backup_an_Analysis_Services_Database.html) e [Automatizzare il backup di un database di Analysis Services (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Automate_Backup_of_Analysis_Services_Database.html).  
  
> [!NOTE]  
>  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], utilizzato per il caricamento e l'esecuzione di query sui modelli di dati PowerPivot in un ambiente SharePoint, carica i relativi modelli dai database del contenuto di SharePoint. Questi database di contenuto sono relazionali e vengono eseguiti nel motore di database relazionale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Di conseguenza, non è prevista alcuna strategia di backup e ripristino di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per i modelli di dati PowerPivot. Se si dispone di un piano di recupero in atto per il contenuto di SharePoint, tale piano include i modelli di dati PowerPivot archiviati nei database di contenuto.  
  
 **Partizioni remote**  
  
 Se nel database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono contenute partizioni remote, è consigliabile eseguire il backup anche di tali partizioni. In tal caso, il backup di tutte le partizioni remote in ogni server remoto viene eseguito rispettivamente in un singolo file di ognuno di tali server remoti. Se pertanto si desidera creare i backup remoti all'esterno dei rispettivi computer host, sarà necessario copiare manualmente tali file nelle aree di archiviazione designate.  
  
 **Contenuto di un file di backup**  
  
 Il backup di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un file di backup il cui contenuto varia in base alla modalità di archiviazione utilizzata dagli oggetti del database. Tale differenza di contenuto dei backup è dovuta al fatto che ogni modalità di archiviazione memorizza effettivamente un set di informazioni diverso all'interno di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Ad esempio, partizioni e dimensioni OLAP ibrido (HOLAP) multidimensionali archiviano nel database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le aggregazioni e i metadati, mentre partizioni e dimensioni OLAP relazionale (ROLAP) archiviano nel database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo i metadati. Poiché il contenuto effettivo di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] varia in base alla modalità di archiviazione di ogni partizione, varia anche il contenuto del file di backup. Nella tabella seguente viene associato il contenuto del file di backup alla modalità di archiviazione utilizzata dagli oggetti.  
  
|Modalità di archiviazione|Contenuto del file di backup|  
|------------------|-----------------------------|  
|Partizioni e dimensioni MOLAP multidimensionali|Metadati, dati di origine e aggregazioni|  
|Partizioni e dimensioni HOLAP multidimensionali|Metadati e aggregazioni|  
|Partizioni e dimensioni ROLAP multidimensionali|Metadati|  
|Modelli tabulari in memoria|Metadati e dati di origine|  
|Modelli tabulari DirectQuery|Solo metadati|  
  
> [!NOTE]  
>  Nel backup di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non vengono inclusi i dati delle origini sottostanti, ad esempio di un database relazionale. Viene eseguito solo il backup dei contenuti del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Quando si esegue il backup di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile scegliere tra le opzioni seguenti:  
  
-   Comprimere o meno tutti i backup di database. Per impostazione predefinita, i backup vengono compressi.  
  
-   Crittografare o meno il contenuto dei file di backup e richiedere una password prima di consentire la decrittografia e il ripristino dei file. Per impostazione predefinita, i dati di backup non vengono crittografati.  
  
    > [!IMPORTANT]  
    >  Per ogni file di backup, l'utente che esegue il comando di backup deve disporre delle autorizzazioni per scrivere nel percorso di backup specificato per ogni file. Inoltre, l'utente deve avere uno dei ruoli seguenti: deve essere un membro di un ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oppure un membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) sul database di cui eseguire il backup.  
  
 Per altre informazioni sul backup di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , vedere [Opzioni di backup](backup-options.md).  
  
##  <a name="bkmk_restore"></a> Ripristino di un database di Analysis Services  
 Gli amministratori possono ripristinare un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a partire da uno o più file di backup.  
  
> [!NOTE]  
>  Se un file di backup è crittografato, è necessario digitare la password specificata durante il backup per poter ripristinare un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da tale file.  
  
 Durante il ripristino, è possibile scegliere tra le opzioni seguenti:  
  
-   È possibile ripristinare il database utilizzando il nome originale oppure specificando un nuovo nome.  
  
-   È possibile sovrascrivere un database esistente. In tal caso, è necessario specificare espressamente che si desidera sovrascrivere il database esistente.  
  
-   È possibile scegliere se ripristinare le informazioni di sicurezza esistenti o ignorare le informazioni di sicurezza sulle appartenenze.  
  
-   È possibile scegliere di utilizzare il comando di ripristino per modificare la cartella di ripristino per ogni partizione da ripristinare. È possibile ripristinare le partizioni locali in qualsiasi percorso di cartella locale dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui si intende ripristinare il database. È possibile ripristinare le partizioni remote in qualsiasi cartella di qualsiasi server diverso dal server locale. Non è possibile trasformare le partizioni remote in partizioni locali.  
  
    > [!IMPORTANT]  
    >  Per ogni file di backup, l'utente che esegue il comando di ripristino deve disporre delle autorizzazioni per leggere dal percorso di backup specificato per ogni file. Per ripristinare un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non installato nel server, l'utente deve inoltre essere un membro del ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specifica. Per sovrascrivere un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , l'utente deve avere uno dei ruoli seguenti: deve essere un membro del ruolo del server per l'istanza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o un membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) sul database da ripristinare.  
  
    > [!NOTE]  
    >  Dopo avere ripristinato un database esistente, l'utente che ha effettuato l'operazione potrebbe perdere l'accesso al database ripristinato. Può verificarsi questa perdita di accesso se, al momento dell’esecuzione del backup, l'utente non era un membro del ruolo del server o non era un membro del ruolo del database con autorizzazioni Controllo completo (amministratore).  
  
 Per altre informazioni sul ripristino di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , vedere [Opzioni di ripristino](restore-options.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Backup, ripristino e sincronizzazione di database &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)   
 [Analysis Services PowerShell](../analysis-services-powershell.md)  
  
  
