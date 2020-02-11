---
title: Aggiornare pacchetti di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a1ff35cfc7d5e8611c06981b2e3a9fe9dd6e82fd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768997"
---
# <a name="upgrade-integration-services-packages"></a>Aggiornare pacchetti di Integration Services
  Quando si aggiorna un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] alla versione corrente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di, i pacchetti esistenti [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] non vengono aggiornati automaticamente al formato del pacchetto usato dalla versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] corrente. A tale scopo, sarà necessario selezionare un metodo di aggiornamento e aggiornare manualmente i pacchetti.  
  
 Quando si aggiorna un [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , esegue la migrazione degli script in qualsiasi attività script e componente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] di script a Tools for Applications (VSTA). In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]gli script nelle attività script o nei componenti di script [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] utilizzati per le applicazioni (VSA). Per altre informazioni sulle modifiche che potrebbe essere necessario apportare agli script prima della migrazione e sull'errore di conversione degli script, vedere [Migrare script a VSTA](../../sql-server/install/migrate-scripts-to-vsta.md).  
  
 Per informazioni sull'aggiornamento dei pacchetti quando si converte un progetto nel modello di distribuzione del progetto, vedere [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md).  
  
## <a name="sql-server-2000-data-transformation-services-packages"></a>Pacchetti di SQL Server 2000 Data Transformation Services  
 Il supporto per la migrazione o l'esecuzione di pacchetti di Data Transformation Services (DTS) non è più disponibile nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]versione corrente di. Le seguenti funzionalità DTS non sono più utilizzate.  
  
-   DTS Runtime  
  
-   API DTS  
  
-   Migrazione guidata pacchetti per la migrazione dei pacchetti DTS alla versione successiva di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Supporto per la gestione di pacchetti DTS in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Attività Esegui pacchetto DTS 2000  
  
-   Analisi di pacchetti DTS in Preparazione aggiornamento.  
  
 Per la migrazione di pacchetti DTS sono disponibili le opzioni seguenti.  
  
-   Effettuare la migrazione dei pacchetti in [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], quindi effettuare l'aggiornamento dei pacchetti a [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].  
  
     Per informazioni sulla migrazione dei pacchetti DTS in [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] e [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], vedere [Migrazione dei pacchetti Data Transformation Services](https://go.microsoft.com/fwlink/?LinkId=251870) (2005) e [Migrazione dei pacchetti Data Transformation Services](https://go.microsoft.com/fwlink/?LinkId=251871) (2008).  
  
-   Ricreare i pacchetti DTS utilizzando [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].  
  
     Per informazioni sulle nuove funzionalità in [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)], vedere [Novità &#40;Integration Services&#41;](../what-s-new-in-integration-services-in-sql-server-2016.md). Per una panoramica della struttura dei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Pacchetti di Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md).  
  
## <a name="selecting-an-upgrade-method"></a>Selezione di un metodo di aggiornamento  
 Sono disponibili diversi metodi per l’aggiornamento dei pacchetti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Per alcuni di questi metodi l'aggiornamento è solo temporaneo, mentre per altri è permanente. Nella tabella seguente viene descritto ciascun metodo e viene indicato se l'aggiornamento è temporaneo o permanente.  
  
> [!NOTE]  
>  Quando si esegue un pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite l'utilità **dtexec** (dtexec.exe) installata con la versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'aggiornamento temporaneo del pacchetto aumenta il tempo di esecuzione. La frequenza di aumento del tempo di esecuzione varia a seconda della dimensione del pacchetto. Per evitare un aumento del tempo di esecuzione, si consiglia di aggiornare il pacchetto prima di eseguirlo.  
  
|Metodo di aggiornamento|Tipo di aggiornamento|  
|--------------------|---------------------|  
|Usare l'utilità **dtexec** (dtexec.exe) installata con la versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire un pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> Per altre informazioni, vedere [dtexec Utility](../packages/dtexec-utility.md).|L'aggiornamento del pacchetto è temporaneo. Per un pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], la migrazione degli script è temporanea.<br /><br /> Le modifiche non possono essere salvate.|  
|Aprire un file di pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|L'aggiornamento del pacchetto è permanente se si salva il pacchetto; in caso contrario, è temporaneo.<br /><br /> Per un pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], la migrazione degli script è permanente se si salva il pacchetto; in caso contrario, è temporanea.|  
|Aggiungere un pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a un progetto esistente in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|L'aggiornamento del pacchetto è permanente. Per un pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], la migrazione degli script è permanente.|  
|Aprire un file di progetto [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], quindi utilizzare l'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] per aggiornare più pacchetti nel progetto.<br /><br /> Per altre informazioni, vedere [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md) e [Guida sensibile al contesto dell'Aggiornamento guidato pacchetti SSIS](../ssis-package-upgrade-wizard-f1-help.md).|L'aggiornamento del pacchetto è permanente. Per un pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], la migrazione degli script è permanente.|  
|Eseguire l'utilità <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> per aggiornare uno o più pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|L'aggiornamento del pacchetto è permanente. Per un pacchetto di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], la migrazione degli script è permanente.|  
  
## <a name="custom-applications-and-custom-components"></a>Applicazioni e componenti personalizzati  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] non funzionano con la versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 È possibile usare la versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per eseguire e gestire pacchetti in cui sono inclusi i componenti personalizzati di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssIS](../../includes/ssis-md.md)]. Sono state aggiunte quattro regole di reindirizzamento di associazione nei file seguenti per consentire di reindirizzare gli assembly di runtime dalla versione 10.0.0.0 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]) alla versione 11.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 Per utilizzare [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] per progettare pacchetti che includono [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] componenti personalizzati, è necessario modificare il file devenv. exe. config che si trova in * \<unità>*: \Programmi\Microsoft Visual Studio 10.0 \ Common7\IDE.  
  
 Per utilizzare questi pacchetti con le applicazioni dei clienti che vengono compilate con il runtime per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], includere le regole di reindirizzamento nella sezione di configurazione del file *.exe.config per il file eseguibile. Tramite le regole gli assembly di runtime vengono reindirizzati alla versione 11.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). Per altre informazioni sul reindirizzamento della versione dell'assembly, vedere [Elemento \<assemblyBinding> per \<runtime>](https://msdn.microsoft.com/library/twy1dw1e.aspx).  
  
### <a name="locating-the-assemblies"></a>Individuazione degli assembly  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]gli assembly [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono stati aggiornati a .NET 4.0. È disponibile una Global Assembly Cache separata per .NET 4 in *\<unità>* :\Windows\Microsoft.NET\assembly. Tutti gli assembly di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] possono essere individuati in questo percorso, generalmente nella cartella GAC_MSIL.  
  
 Come nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i file [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dll di estendibilità principali si trovano anche nell' * \<unità>*: \Programmi\Microsoft SQL Server\100\SDK\Assemblies.  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>Informazioni sui risultati dell'aggiornamento dei pacchetti di SQL Server  
 Durante il processo di aggiornamento dei pacchetti, la maggior parte dei componenti e delle funzionalità dei pacchetti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] viene convertita in modo semplice nella controparte corrispondente nella versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Diversi componenti e funzionalità, tuttavia, non verranno aggiornati o avranno risultati di cui è consigliabile tenere conto. Nella tabella seguente vengono identificati tali componenti e funzionalità.  
  
> [!NOTE]  
>  Per identificare i pacchetti interessati dai problemi inclusi nella tabella, eseguire Preparazione aggiornamento. Per altre informazioni, vedere [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
|Componente o funzionalità|Risultati dell'aggiornamento|  
|--------------------------|---------------------|  
|Stringhe di connessione|Per i pacchetti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], i nomi di alcuni provider sono stati modificati e nelle stringhe di connessione vengono richiesti valori diversi. Per aggiornare le stringhe di connessione, utilizzare una delle procedure seguenti:<br /><br /> -Utilizzare l' [!INCLUDE[ssIS](../../includes/ssis-md.md)] aggiornamento guidato pacchetti per aggiornare il pacchetto e selezionare l'opzione **Aggiorna stringhe di connessione per l'utilizzo di nuovi nomi di provider** .<br /><br /> -In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], nella pagina generale della finestra di dialogo Opzioni, selezionare l'opzione **Aggiorna stringhe di connessione per l'utilizzo di nuovi nomi di provider** . Per ulteriori informazioni su questa opzione, vedere la [pagina generale](../general-page-of-integration-services-designers-options.md).<br /><br /> - In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] aprire il pacchetto e modificare manualmente il testo della proprietà ConnectionString.<br /><br /> Non è possibile usare le procedure precedenti per aggiornare una stringa di connessione quando è archiviata in un file di configurazione o in un file di origine dati oppure quando un'espressione imposta la proprietà `ConnectionString`. In questi casi, per aggiornare la stringa di connessione è necessario aggiornare manualmente il file o l'espressione.<br /><br /> Per altre informazioni sulle origini dati, vedere [Origini dati](../connection-manager/data-sources.md).|  
|Trasformazione Ricerca|Per i pacchetti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] il processo di aggiornamento consente di aggiornare automaticamente la trasformazione Ricerca nella versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. La versione corrente di questo componente, tuttavia, include funzionalità aggiuntive che potrebbero risultare utili.<br /><br /> Per altre informazioni, vedere [trasformazione Ricerca](../data-flow/transformations/lookup-transformation.md).|  
|Attività e componente Script|Per i pacchetti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], il processo di aggiornamento consente di effettuare automaticamente la migrazione degli script nell'attività e nel componente Script da VSA a VSTA.<br /><br /> Per altre informazioni sulle modifiche che potrebbe essere necessario apportare agli script prima della migrazione e sull'errore di conversione degli script, vedere [Migrare script a VSTA](../../sql-server/install/migrate-scripts-to-vsta.md).|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>Script che dipendono da ADODB.dll  
 Script dell'attività Script e del componente script che fanno riferimento in modo esplicito ad ADODB.dll non possono essere aggiornati o eseguiti in computer senza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] installato. Per aggiornare questi script Attività script o Componente script, si consiglia di rimuovere la dipendenza da ADODB.dll.  Ado.Net è l'alternativa consigliata per il codice gestito, ad esempio gli script VB e C#.  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Pagina sull'articolo tecnico relativo a [5 suggerimenti per un semplice aggiornamento di SSIS a SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=235321) sul sito msdn.microsoft.com.  
  
-   Intervento nel blog relativo all' [utilizzo delle applicazioni e delle estensioni SSIS personalizzate esistenti in Denali](https://go.microsoft.com/fwlink/?LinkId=238157)sul sito blogs.msdn.com.  
  
-   Webcast relativo all'[aggiornamento dei pacchetti SSIS a SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=258674)sul sito Web channel9.msdn.com.  
  
  
