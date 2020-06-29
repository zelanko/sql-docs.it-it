---
title: Installare Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7cc7cb929aa34c9226dbdff9efb6b0c918b546f1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425058"
---
# <a name="install-integration-services"></a>Installazione di Integration Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone di un singolo programma di installazione che consente di installare uno o tutti i componenti, incluso [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Tramite il programma di installazione è possibile installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con o senza gli altri componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un singolo computer.  
  
 In questo argomento sono incluse importanti considerazioni di cui tenere conto prima di installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Le informazioni incluse in questo argomento consentono di valutare le opzioni di installazione per effettuare le selezioni appropriate ai fini di una corretta installazione.  
  
 In questo argomento non sono incluse indicazioni per l'avvio del programma di installazione, l'esecuzione dell'installazione dalla riga di comando o l'utilizzo dell'Installazione guidata. Per istruzioni dettagliate su come avviare il programma di installazione e selezionare i componenti da installare, vedere Guida introduttiva all' [installazione di SQL Server 2014](../../getting-started/quick-start-installation-of-sql-server-2014.md). Per informazioni sulle opzioni della riga di comando per l'installazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , vedere [Install SQL Server 2014 dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="preparing-to-install-integration-services"></a>Preparazione dell'installazione di Integration Services  
 Prima di installare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , esaminare i requisiti seguenti:  
  
-   [Requisiti hardware e software per l'installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Parametri di controllo di Controllo configurazione sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)  
  
-   [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
## <a name="selecting-an-integration-services-configuration"></a>Selezione di una configurazione di Integration Services  
 È possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nelle configurazioni seguenti:  
  
-   È possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un computer in cui non sono presenti istanze precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   È possibile effettuare un'installazione side-by-side di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] e di un'istanza esistente di [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] e [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].  
  
     Se si esegue l'aggiornamento a [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] in un computer con una di queste versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] verrà installato side-by-side con la versione precedente.  
  
     Per altre informazioni sull'aggiornamento di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Aggiornare Integration Services](upgrade-integration-services.md). Per informazioni sulla compatibilità con le versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Compatibilità con le versioni precedenti di Integration Services](../integration-services-backward-compatibility.md).  
  
## <a name="installing-integration-services"></a>installazione di Integration Services  
 Dopo avere esaminato i requisiti di installazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e avere verificato che il computer in uso soddisfi tali requisiti, è possibile installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
> [!NOTE]  
>  Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per impostazione predefinita quando si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tutti gli utenti nel gruppo Utenti dispongono di accesso al servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Quando si installa [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], gli utenti non dispongono di accesso al servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Il servizio è protetto per impostazione predefinita. Dopo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'installazione di, l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] amministratore deve eseguire lo strumento di configurazione DCOM (Dcomcnfg.exe) per concedere a utenti specifici l'accesso a **SQL Server Integration Services 12,0**.  
>   
>  Per istruzioni su come concedere autorizzazioni, vedere [Concedere autorizzazioni al servizio Integration Services](../grant-permissions-to-integration-services-service.md).  
  
 Se per installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]si utilizza l'Installazione guidata, verrà visualizzata una serie di pagine per specificare le opzioni e i componenti desiderati. Di seguito sono riportate le pagine dell'installazione guidata in cui le opzioni selezionate influiscono sull'installazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con le raccomandazioni di selezione:  
  
-   **Selezione delle funzioni**  
  
     Selezionare **Integration Services** per installare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ed eseguire i pacchetti all'esterno dell'ambiente di progettazione.  
  
     Per l'installazione completa di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]con gli strumenti e la documentazione per lo sviluppo e la gestione dei pacchetti, selezionare **Integration Services** e le seguenti **Funzionalità condivise**:  
  
    -   **SQL Server Data Tools** per installare gli strumenti per la progettazione dei pacchetti.  
  
    -   **Strumenti di gestione - Completa** per installare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per la gestione dei pacchetti.  
  
    -   **SDK di strumenti client** per installare assembly gestiti per la programmazione [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Molte soluzioni di data warehousing richiedono anche l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componenti aggiuntivi, ad esempio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Alcuni componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile selezionare per l'installazione nella pagina **Selezione funzionalità** dell'Installazione guidata consentono di installare solo un subset parziale dei componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Tali componenti si rivelano utili per attività specifiche, ma le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] risulteranno limitate. L'opzione **Servizi Motore di database** , ad esempio, consente di installare i componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessari per l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'opzione **SQL Server Data Tools** consente di installare i componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessari per la progettazione di un pacchetto, ma il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non viene installato e non è possibile eseguire pacchetti all'esterno di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Per garantire l'installazione completa di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], è necessario selezionare **Integration Services** nella pagina **Selezione funzionalità** .  
  
     **Installazione in un computer a 64 bit** In un computer a 64 bit la selezione di **Integration Services** durante l'installazione comporta l'installazione solo degli strumenti e del runtime a 64 bit. Se è necessario eseguire pacchetti nella modalità a 32 bit, è necessario selezionare un'opzione aggiuntiva per installare gli strumenti e il runtime a 32 bit:  
  
    -   Se il computer a 64 bit esegue il sistema operativo x86, selezionare **SQL Server Data Tools** o **strumenti di gestione-completa**.  
  
    -   Se nel computer a 64 bit è in esecuzione il [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] sistema operativo, selezionare **strumenti di gestione-completa**.  
  
     **Installazione in un server dedicato per ETL** Per utilizzare un server dedicato per i processi di estrazione, trasformazione e caricamento (ETL), si consiglia di installare un'istanza locale del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] quando si installa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] i pacchetti vengono in genere archiviati in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e la pianificazione di tali pacchetti si basa su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se nel server ETL non è presente un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)], sarà necessario pianificare o eseguire i pacchetti da un server che dispone di un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Ciò significa che i pacchetti non verranno eseguiti nel server ETL, bensì nel server dal quale sono stati avviati. Di conseguenza, le risorse del server ETL dedicato non vengono utilizzate come previsto. Inoltre, le risorse di altri server possono essere violate dai processi ETL in esecuzione.  
  
-   **Configurazione istanza**  
  
     Qualsiasi selezione effettuata nella pagina **Configurazione dell'istanza** non influisce su [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o sul servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     In un computer è possibile installare solo un'istanza del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . È possibile connettersi al servizio utilizzando il nome del computer.  
  
     Per impostazione predefinita, il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è configurato per gestire i pacchetti archiviati nel database **msdb** dell'istanza del Motore di database installata contemporaneamente a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se l'istanza del Motore di database non viene installata contemporaneamente a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene configurato in modo da gestire i pacchetti archiviati nel database **msdb** dell'istanza predefinita locale del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Per gestire i pacchetti archiviati in un'istanza denominata o un'istanza remota del [!INCLUDE[ssDE](../../includes/ssde-md.md)]o in più istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)], è necessario modificare il file di configurazione. Per altre informazioni su come modificare il file di configurazione, vedere [Configurazione del servizio Integration Services &#40;SSIS&#41;](../service/integration-services-service-ssis-service.md).  
  
-   **Configurazione del server**  
  
     Rivedere le impostazioni per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nella scheda **Account di servizio** della pagina **Configurazione server** .  
  
     Se è installato Windows 7 o Windows Server 2008 R2, il [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servizio è registrato per l'esecuzione con l'account virtuale SERVICES\MSDTSSERVER120 NT e il **tipo di avvio** è **automatico**.  Non è necessario immettere una password per l'account virtuale. Se è installato Windows Vista o Windows Server 2008, il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è registrato per l'esecuzione con l'account del servizio di rete predefinito e l'impostazione di **Tipo di avvio** è **Automatico**. Non è necessario immettere una password per l'account Servizio di rete predefinito.  
  
 Per impostazione predefinita, in una nuova installazione, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene configurato in modo da non registrare gli eventi correlati all'esecuzione dei pacchetti nel registro eventi delle applicazioni. Questa impostazione impedisce la creazione di un numero eccessivo di voci nel registro eventi quando si utilizza la funzionalità di raccolta dati di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Gli eventi non registrati includono EventID 12288, che indica che il pacchetto è stato avviato ed EventID 12289 che indica che il pacchetto è stato completato. Per inserire questi due eventi nel registro eventi dell'applicazione, aprire il Registro di sistema per la modifica. Nel Registro di sistema individuare il nodo HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS e modificare il valore DWORD dell'impostazione LogPackageExecutionToEventLog da 0 a 1.  
  
## <a name="understanding-the-integration-services-service"></a>Informazioni sul servizio Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installa il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene installato quando si seleziona l'opzione **Integration Services** nella pagina **Selezione funzionalità** . Quando si accettano le impostazioni predefinite nella pagina **Configurazione server[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], il servizio** viene abilitato e **Tipo di avvio** viene impostato su **Automatico**.  
  
 È possibile installare solo una singola istanza del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un computer. Il servizio non è specifico di una particolare istanza del Motore di database. È possibile connettersi al servizio usando il nome del computer in cui è in esecuzione il servizio stesso.  
  
## <a name="installing-integration-services-on-64-bit-computers"></a>Installazione di Integration Services in computer a 64 bit  
  
### <a name="integration-services-features-installed-on-64-bit-computers"></a>Integrazione delle funzionalità di Integration Services installate in computer a 64 bit  
 Il programma di installazione prevede l'installazione di diverse funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in base alle opzioni di installazione selezionate:  
  
-   Quando si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e si seleziona l'installazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , verranno installati gli strumenti e le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a 64 bit.  
  
-   Se sono necessarie le funzionalità della fase di progettazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , installare anche [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   Se sono necessarie le versioni a 32 bit degli strumenti e del runtime di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per eseguire pacchetti specifici in modalità a 32 bit, installare anche [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Le funzionalità a 64 bit vengono installate nella directory **Programmi** , mentre le funzionalità a 32 bit vengono installate separatamente nella directory **Programmi (x86)** . Non si tratta di un comportamento specifico di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], l'ambiente di sviluppo a 32 bit per pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , non è supportato nel sistema operativo [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] a 64 bit e non viene installato nei server [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] .  
  
  
