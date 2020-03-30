---
title: Guida sensibile al contesto dell'Aggiornamento guidato pacchetti SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
f1_keywords:
- sql13.is.upgradewizard.ssisupgradewizard.f1
- sql13.is.upgradewizard.selectsourcelocation.f1
- sql13.is.upgradewizard.selectdestinationlocation.f1
- sql13.is.upgradewizard.selectpackagemgtoptions.f1
- sql13.is.upgradewizard.selectpackages.f1
- sql13.is.upgradewizard.completewizard.f1
- sql13.is.upgradewizard.upgradingpackage.f1
ms.assetid: 7fe886ff-1ea5-48d5-9d20-d5da36dd1cd7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 98f0e19bb0e3eb424d742990ce2f63e3fb0af019
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295708"
---
# <a name="ssis-package-upgrade-wizard-f1-help"></a>Guida sensibile al contesto dell'Aggiornamento guidato pacchetti SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Usare l'Aggiornamento guidato pacchetti SSIS per aggiornare i pacchetti creati in versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel formato della versione corrente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 **Per eseguire l'Aggiornamento guidato pacchetti SSIS**  
  
-   [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  

## <a name="ssis-upgrade-wizard"></a>Aggiornamento guidato SSIS
  
### <a name="options"></a>Opzioni  
 **Non visualizzare più questa pagina**  
 Consente di evitare la visualizzazione della pagina introduttiva alla successiva apertura della procedura guidata.  
 
## <a name="select-source-location-page"></a>Pagina Seleziona posizione di origine
 Usare la pagina **Seleziona posizione di origine** per specificare l'origine da cui eseguire l'aggiornamento dei pacchetti.  
  
> [!NOTE]  
>  Tale pagina è disponibile solo quando si esegue l'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o dal prompt dei comandi.  
  
### <a name="static-options"></a>Opzioni statiche  
 **Origine pacchetto**  
 Selezionare il percorso di archiviazione che contiene i pacchetti da aggiornare. Per questa opzione sono disponibili i valori elencati nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**File system**|Indica che i pacchetti da aggiornare si trovano in una cartella nel computer locale.<br /><br /> Per eseguire il backup dei pacchetti originali prima dell'aggiornamento, è necessario archiviare i pacchetti originali nel file system. Per ulteriori informazioni, vedere l'argomento relativo alla procedura.|  
|**Archivio pacchetti SSIS**|Indica che i pacchetti da aggiornare si trovano nell'archivio pacchetti. L'archivio pacchetti è costituito dal set di cartelle del file system gestito dal servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Per altre informazioni, vedere [Gestione dei pacchetti &#40;servizio SSIS&#41;](../integration-services/service/package-management-ssis-service.md).<br /><br /> La selezione di questo valore determina la visualizzazione delle opzioni dinamiche di **Origine pacchetto** corrispondenti.|  
|**Microsoft SQL Server**|Indica che i pacchetti da aggiornare provengono da un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]esistente.<br /><br /> La selezione di questo valore determina la visualizzazione delle opzioni dinamiche di **Origine pacchetto** corrispondenti.|  
  
 **Cartella**  
 Digitare il nome di una cartella che contiene i pacchetti da aggiornare o fare clic su **Sfoglia** e individuare la cartella.  
  
 **Sfoglia**  
 Consente di individuare la cartella che contiene i pacchetti da aggiornare.  
  
### <a name="package-source-dynamic-options"></a>Opzioni dinamiche di Origine pacchetto  
  
#### <a name="package-source--ssis-package-store"></a>Origine pacchetto = Archivio pacchetti SSIS  
 **Server**  
 Digitare il nome del server che contiene i pacchetti da aggiornare oppure selezionare il server nell'elenco.  
  
#### <a name="package-source--microsoft-sql-server"></a>Origine pacchetto = Microsoft SQL Server  
 **Server**  
 Digitare il nome del server che contiene i pacchetti da aggiornare oppure selezionare il server dall'elenco.  
  
 **Usa autenticazione di Windows**  
 Selezionare questa opzione per utilizzare l'autenticazione di Windows per la connessione al server.  
  
 **Usa autenticazione di SQL Server**  
 Selezionare questa opzione per usare l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server. Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
 **Nome utente**  
 Digitare il nome utente usato dall'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server.  
  
 **Password**  
 Digitare la password usata dall'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server.  
 
## <a name="select-destination-location-page"></a>Pagina Seleziona posizione di destinazione
 Usare la pagina **Seleziona posizione di destinazione** per specificare la destinazione in cui salvare i pacchetti aggiornati.  
  
> [!NOTE]  
>  Tale pagina è disponibile solo quando si esegue l'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o dal prompt dei comandi.  
 
### <a name="static-options"></a>Opzioni statiche  
 **Salva in posizione di origine**  
 Consente di salvare i pacchetti aggiornati nella stessa posizione specificata nella pagina **Seleziona posizione di origine** della procedura guidata.  
  
 Se i pacchetti originali sono archiviati nel file system e si desidera eseguire il backup dei pacchetti, selezionare l'opzione **Salva in posizione di origine** . Per altre informazioni, vedere [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
 **Seleziona nuova posizione di destinazione**  
 Consente di salvare i pacchetti aggiornati nella posizione di destinazione specificata nella pagina.  
  
 **Origine pacchetto**  
 Consente di specificare la posizione di archiviazione dei pacchetti di aggiornamento. Per questa opzione sono disponibili i valori elencati nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**File system**|Indica che i pacchetti aggiornati devono essere salvati in una cartella nel computer locale.|  
|**Archivio pacchetti SSIS**|Indica che i pacchetti aggiornati devono essere salvati nell'archivio pacchetti Integration Services. L'archivio pacchetti è costituito dal set di cartelle del file system gestito dal servizio Integration Services. Per altre informazioni, vedere [Gestione dei pacchetti &#40;servizio SSIS&#41;](../integration-services/service/package-management-ssis-service.md).<br /><br /> La selezione di questo valore determina la visualizzazione delle opzioni dinamiche di **Origine pacchetto** corrispondenti.|  
|**Microsoft SQL Server**|Indica che i pacchetti aggiornati devono essere salvati in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]esistente.<br /><br /> La selezione di questo valore determina la visualizzazione delle opzioni dinamiche di **Origine pacchetto** corrispondenti.|  
  
 **Cartella**  
 Digitare il nome della cartella in cui verranno salvati i pacchetti aggiornati oppure fare clic su **Sfoglia** e individuare la cartella.  
  
 **Sfoglia**  
 Consente di individuare la cartella in cui verranno salvati i pacchetti aggiornati.  
  
### <a name="package-source-dynamic-options"></a>Opzioni dinamiche di Origine pacchetto  
  
#### <a name="package-source--ssis-package-store"></a>Origine pacchetto = Archivio pacchetti SSIS  
 **Server**  
 Digitare il nome del server in cui verranno salvati i pacchetti di aggiornamento oppure selezionare un server nell'elenco.  
  
#### <a name="package-source--microsoft-sql-server"></a>Origine pacchetto = Microsoft SQL Server  
 **Server**  
 Digitare il nome del server in cui verranno salvati i pacchetti di aggiornamento oppure selezionare il server nell'elenco.  
  
 **Usa autenticazione di Windows**  
 Selezionare questa opzione per utilizzare l'autenticazione di Windows per la connessione al server.  
  
 **Usa autenticazione di SQL Server**  
 Selezionare questa opzione per usare l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server. Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
 **Nome utente**  
 Digitare il nome utente da usare quando si seleziona l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server.  
  
 **Password**  
 Digitare la password da usare quando si seleziona l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server.  
 
## <a name="select-package-management-options-page"></a>Pagina Seleziona opzioni di gestione pacchetti
  Usare la pagina **Seleziona opzioni di gestione pacchetti** per specificare le opzioni per l'aggiornamento dei pacchetti.  
  
 **Per eseguire l'Aggiornamento guidato pacchetti SSIS**  
  
-   [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
### <a name="options"></a>Opzioni  
 **Aggiorna stringhe di connessione per l'uso di nuovi nomi di provider**  
 Consente di aggiornare le stringhe di connessione per utilizzare i nomi dei provider seguenti per la versione corrente di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Provider OLE DB per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 L'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] consente di aggiornare solo le stringhe di connessione archiviate nelle gestioni connessione. Non vengono aggiornate le stringhe di connessione costruite dinamicamente utilizzando il linguaggio delle espressioni di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o il codice in un'attività Script.  
  
 **Convalida pacchetti di aggiornamento**  
 Consente di convalidare i pacchetti di aggiornamento e di salvare solo i pacchetti che superano la convalida.  
  
 Se non si seleziona questa opzione, i pacchetti di aggiornamento non verranno convalidati. Pertanto, verranno salvati tutti i pacchetti di aggiornamento, indipendentemente dalla loro validità. I pacchetti di aggiornamento vengono salvati nella destinazione specificata alla pagina **Seleziona posizione di destinazione** della procedura guidata.  
  
 La convalida influisce sulla durata del processo di aggiornamento. Si consiglia di non selezionare questa opzione per pacchetti grandi che probabilmente verranno aggiornati in modo corretto.  
  
 **Crea nuovi ID pacchetti**  
 Consente di creare nuovi ID per i pacchetti di aggiornamento.  
  
 **Continua aggiornamento in caso di mancato aggiornamento dei pacchetti**  
 Consente di specificare che quando un pacchetto non può essere aggiornato, l'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] continua ad aggiornare i pacchetti rimanenti.  
  
 **Conflitti di nome pacchetti**  
 Consente di specificare come vengono gestiti i pacchetti che hanno lo stesso nome. Per questa opzione sono disponibili i valori elencati nella tabella seguente.  
  
 **Sovrascrivi file di pacchetto esistenti**  
 Consente di sostituire il pacchetto esistente con il pacchetto di aggiornamento con lo stesso nome.  
  
 **Aggiungi suffissi numerici a nomi di pacchetti di aggiornamento**  
 Consente di aggiungere un suffisso numerico al nome del pacchetto di aggiornamento.  
  
 **Non aggiornare pacchetti**  
 Consente di arrestare l'aggiornamento dei pacchetti e di visualizzare un errore quando la procedura guidata viene completata.  
  
 Queste opzioni non sono disponibili quando si seleziona l'opzione **Salva in posizione di origine** nella pagina **Seleziona posizione di destinazione** della procedura guidata.  
  
 **Ignora configurazioni**  
 Consente di non caricare le configurazioni di pacchetto durante l'aggiornamento. Se si seleziona questa opzione l'aggiornamento del pacchetto richiede meno tempo.  
  
 **Esegui backup pacchetti originali**  
 Consente di eseguire il backup dei pacchetti originali in una cartella **SSISBackupFolder** . Viene creata la cartella **SSISBackupFolder** come sottocartella della cartella che contiene i pacchetti originali e i pacchetti aggiornati.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se si specifica che i pacchetti originali e i pacchetti aggiornati sono archiviati nel file system e nella stessa cartella.  

## <a name="select-packages-page"></a>Pagina Seleziona pacchetti
  Utilizzare la pagina **Seleziona pacchetti** per selezionare i pacchetti da aggiornare. In questa pagina vengono elencati i pacchetti archiviati nel percorso specificato nella pagina **Seleziona posizione di origine** della procedura guidata.  
  
### <a name="options"></a>Opzioni  
 **Nome del pacchetto esistente**  
 Selezionare uno o più pacchetti da aggiornare.  
  
 **Nome del pacchetto di aggiornamento**  
 Consente di specificare il nome del pacchetto di destinazione o di utilizzare il nome predefinito indicato dalla procedura guidata.  
  
> [!NOTE]  
>  È inoltre possibile modificare il nome del pacchetto di destinazione dopo l'aggiornamento. In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], consente di aprire il pacchetto aggiornato e modificare il nome del pacchetto.  
  
 **Password**  
 Consente di specificare la password utilizzata per decrittografare i pacchetti di aggiornamento selezionati.  
  
 **Applica a selezione**  
 Consente di applicare la password specificata per decrittografare i pacchetti di aggiornamento selezionati.  
 
## <a name="complete-the-wizard-page"></a>Pagina Completamento procedura guidata
  Utilizzare la pagina **Completamento procedura guidata** per verificare e confermare le opzioni di aggiornamento del pacchetto selezionate. Si tratta dell'ultima pagina della procedura guidata. È possibile tornare alle pagine precedenti per modificare le opzioni per questa sessione della procedura guidata.  
  
### <a name="options"></a>Opzioni  
 **Riepilogo delle opzioni**  
 Rivedere le opzioni di aggiornamento selezionate nella procedura guidata. Per modificare un'opzione, fare clic su **Indietro** per tornare alle pagine precedenti della procedura guidata.
 
## <a name="upgrading-the-packages-page"></a>Pagina Aggiornamento pacchetti
  Utilizzare la pagina **Aggiornamento pacchetti** per visualizzare lo stato dell'aggiornamento dei pacchetti e per interrompere l'aggiornamento. L'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] consente di aggiornare uno per uno i pacchetti selezionati.  
  
### <a name="options"></a>Opzioni  
 **Riquadro Messaggio**  
 Consente di visualizzare messaggi di stato e informazioni di riepilogo durante il processo di aggiornamento.  
  
 **Azione**  
 Consente di visualizzare le azioni incluse nell'aggiornamento.  
  
 **Status**  
 Consente di visualizzare il risultato di ogni azione.  
  
 **Messaggio**  
 Consente di visualizzare i messaggi di errore generati da ogni azione.  
  
 **Stop**  
 Consente di arrestare l'aggiornamento del pacchetto.  
  
 **Report**  
 Selezionare le operazioni da eseguire nel report che contiene i risultati dell'aggiornamento del pacchetto:  
  
-   Visualizzare il report online.  
  
-   Salvare il report in un file.  
  
-   Copiare il report negli Appunti  
  
-   Inviare il report come messaggio di posta elettronica.  

## <a name="view-upgraded-packages"></a>Visualizzare i pacchetti aggiornati
### <a name="view-upgraded-packages-that-were-saved-to-a-sql-server-database-or-to-the-package-store"></a>Visualizzare i pacchetti aggiornati salvati in un database di SQL Server o nell'archivio pacchetti
  
In [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], in Esplora oggetti connettersi a un'istanza locale di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], quindi espandere il nodo **Pacchetti archiviati** per visualizzare i pacchetti aggiornati.  
  
### <a name="view-upgraded-packages-that-were-upgraded-from-sql-server-data-tools"></a>Visualizzare i pacchetti aggiornati da SQL Server Data Tools  
  
In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], in Esplora soluzioni aprire il progetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , quindi espandere il nodo **Pacchetti SSIS** per visualizzare i pacchetti aggiornati.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare pacchetti di Integration Services](../integration-services/install-windows/upgrade-integration-services-packages.md)  
  
  
