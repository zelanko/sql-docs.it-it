---
title: Specifica delle impostazioni di configurazione per la distribuzione di soluzioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, configuration settings
- input files [Analysis Services]
- configuration options [Analysis Services]
- Analysis Services deployments, configuration settings
- deploying [Analysis Services], configuration settings
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
author: minewiskan
ms.author: owend
ms.openlocfilehash: 31f269e601900535c3d375ed6e76376fa2bcdf63
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546843"
---
# <a name="specifying-configuration-settings-for-solution-deployment"></a>Definizione delle impostazioni di configurazione per la distribuzione di soluzioni
  La [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuzione guidata legge le opzioni di distribuzione delle partizioni e dei ruoli utilizzate nello script di distribuzione dal \<*project name*> file con estensione ConfigSettings. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]crea questo file quando si compila il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Usa le impostazioni di configurazione del progetto corrente per creare il \<*project name*> file con estensione ConfigSettings.  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a>Esame delle opzioni di configurazione per la distribuzione  
 Di seguito sono riportate le impostazioni di configurazione archiviate nel \<*project name*> file con estensione configsettings:  
  
-   **Stringhe di connessione origine dati** Stringhe di connessione per ciascuna origine dati basate sui valori specificati nel progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . L'ID utente e la password vengono sempre rimossi dalla stringa di connessione prima che il resto della stringa venga archiviato nel file. Se invece viene eseguita la distribuzione direttamente in un'istanza di Analysis Services, è possibile aggiungere le informazioni appropriate relative a ID utente e password all'interno della Distribuzione guidata per garantire l'elaborazione corretta del database di distribuzione. Queste informazioni di connessione non vengono archiviate nello script di distribuzione eventualmente salvato dalla Distribuzione guidata.  
  
-   **Impostazioni di rappresentazione** Questa impostazione definisce il nome utente usato da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per eseguire istruzioni in ciascuna origine dati. Se non è stato specificato alcun account di rappresentazione, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà utilizzato l'account di accesso per eseguire le istruzioni. Se all'account di accesso [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene concesso l'accesso diretto all'origine dati, tutti gli amministratori del database di tutti i database dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] avranno accesso all'origine dati attraverso l'account di accesso. Se vengono specificati un account utente e una password, tali informazioni vengono sempre rimosse prima che le impostazioni di rappresentazione vengano archiviate nel file. Se invece viene eseguita la distribuzione direttamente in un'istanza di Analysis Services, è possibile aggiungere le informazioni appropriate relative a ID utente e password all'interno della Distribuzione guidata per garantire l'elaborazione corretta del database di distribuzione. Queste impostazioni di rappresentazione non vengono archiviate nello script di distribuzione eventualmente salvato dalla Distribuzione guidata.  
  
-   **File di log degli errori di chiave** Questa impostazione definisce il nome e il percorso del file di log degli errori di chiave di ciascun cubo, gruppo di misure, partizione e dimensione del database.  
  
-   **Percorsi di archiviazione** Questa impostazione definisce la posizione di archiviazione di ciascun cubo, gruppo di misure e partizione del database. Se non è stato specificato alcun valore per un oggetto, Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizza la posizione predefinita per tale oggetto. Le partizioni utilizzano ad esempio la posizione del gruppo di misure, i gruppi di misure utilizzano la posizione del cubo e i cubi utilizzano la posizione predefinita degli oggetti dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La posizione di archiviazione può essere un percorso locale o un percorso UNC (Universal Naming Convention).  
  
-   **Server di report** Questa impostazione definisce il server di report e la posizione della cartella per ciascuna azione report definita in ciascun cubo del database.  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a>Modifica delle impostazioni di configurazione per la distribuzione  
 In alcuni casi, potrebbe essere necessario distribuire il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto utilizzando impostazioni di configurazione diverse da quelle archiviate nel \<*project name*> file con estensione ConfigSettings. Potrebbe ad esempio essere preferibile modificare la stringa di connessione per una o più origini dati o specificare posizioni di archiviazione per particolari partizioni o gruppi di misure.  
  
 Per modificare la distribuzione di partizioni e ruoli in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto, è necessario modificare queste informazioni all'interno del \<*project name*> file con estensione configsettings, come descritto nella procedura seguente. Non è possibile modificare le impostazioni delle partizioni e dei ruoli all'interno del progetto perché nella finestra *\<project name>* di dialogo **pagine delle proprietà** di non vengono [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] visualizzate queste opzioni.  
  
> [!NOTE]  
>  Le impostazioni di configurazione possono essere applicate a tutti gli oggetti o solo ai nuovi oggetti creati. Le impostazioni di configurazione possono essere applicate solo ai nuovi oggetti creati quando si distribuiscono oggetti aggiuntivi a un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuito precedentemente e non si desidera sovrascrivere gli oggetti esistenti. Per specificare se le impostazioni di configurazione si applicano a tutti gli oggetti o solo a quelle appena create, impostare questa opzione nel \<*project name*> file con estensione deploymentoptions. Per altre informazioni, vedere [Impostazione delle opzioni di distribuzione dei ruoli e delle partizioni](deployment-script-files-partition-and-role-deployment-options.md).  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a>Per modificare le opzioni di configurazione dopo la generazione dei file di input  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modo interattivo e specificare le impostazioni di configurazione per gli oggetti da distribuire nella pagina **Impostazione proprietà di configurazione** .  
  
     -oppure-  
  
-   Eseguire Distribuzione guidata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] attraverso il prompt dei comandi e impostarla in modo che venga eseguita in modalità file di risposte. Per altre informazioni sulla modalità file di risposte, vedere [Esecuzione della Distribuzione guidata Analysis Services](running-the-analysis-services-deployment-wizard.md).  
  
     -oppure-  
  
-   Modificare il \<*project name*> file con estensione configsettings utilizzando un editor di testo.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione della destinazione di installazione](deployment-script-files-specifying-the-installation-target.md)   
 [Impostazione delle opzioni di distribuzione di partizioni e ruoli](deployment-script-files-partition-and-role-deployment-options.md)   
 [Impostazione delle opzioni di elaborazione](deployment-script-files-specifying-processing-options.md)  
  
  
