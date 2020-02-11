---
title: Autorizzazione dell'accesso a oggetti e operazioni (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.membership.f1
- sql12.asvs.roledesignerdialog.general.f1
helpviewer_keywords:
- access rights [Analysis Services], users
- permissions [Analysis Services], users
- security [Analysis Services], user access
- user access rights [Analysis Services]
- granting permissions [Analysis Services], users
ms.assetid: af28524e-5eca-4dce-a050-da4f406ee1c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d6962452b5615b9b2607007ed86c09eed495f6f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077018"
---
# <a name="authorizing-access-to-objects-and-operations-analysis-services"></a>Autorizzazione dell'accesso a oggetti e operazioni (Analysis Services)
  L'accesso degli utenti non amministratori a cubi, dimensioni e modelli di data mining all'interno di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene concesso tramite l'appartenenza a uno o più ruoli del database. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gli amministratori creano questi ruoli del database, concedendo le autorizzazioni di Lettura o Lettura/Scrittura sugli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi assegnando utenti e gruppi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows a ciascun ruolo.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina le autorizzazioni valide per un utente o un gruppo di Windows specifico combinando le autorizzazioni associate a ogni ruolo del database a cui l'utente o il gruppo appartiene. Di conseguenza, se un ruolo del database non concede a un utente o a un gruppo l'autorizzazione per visualizzare una dimensione, una misura o un attributo, ma l'autorizzazione viene concessa a tale utente o gruppo da un ruolo del database diverso, l'utente o il gruppo disporrà comunque di questa autorizzazione.  
  
> [!IMPORTANT]  
>  I membri del ruolo di amministratore del server di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e i membri di un ruolo del database che dispone di autorizzazioni Controllo completo (amministratore) possono accedere a tutti i dati e i metadati nel database e non necessitano di autorizzazioni aggiuntive per visualizzare oggetti specifici. Ai membri del ruolo del server di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , inoltre, non è possibile negare l'accesso ad alcun oggetto nei database, mentre ai membri di un ruolo del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che dispone di autorizzazioni Controllo completo (amministratore) all'interno di un database non è possibile negare l'accesso ad alcun oggetto incluso nel database. Le operazioni amministrative specializzate quali l'elaborazione possono essere autorizzate tramite ruoli separati con minori autorizzazioni. Per informazioni dettagliate, vedere [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md).  
  
## <a name="list-roles-defined-for-your-database"></a>Visualizzare un elenco dei ruoli definiti per il database  
 Gli amministratori possono eseguire una semplice query DMV in SQL Server Management Studio per ottenere un elenco di tutti i ruoli definiti nel server.  
  
1.  In SSMS fare clic con il pulsante destro del mouse su un database e scegliere **nuova query** | **MDX**.  
  
2.  Digitare la query seguente e premere F5 per avviare l'esecuzione:  
  
    ```  
    Select * from $SYSTEM.DBSCHEMA_CATALOGS  
    ```  
  
     I risultati includono il nome del database, la descrizione, il nome del ruolo e la data dell'ultima modifica. Partendo da queste informazioni è possibile passare ai singoli database per controllare l'appartenenza e le autorizzazioni di un ruolo specifico.  
  
## <a name="top-down-overview-of-analysis-services-authorization"></a>Panoramica dall'alto verso il basso dell'autorizzazione di Analysis Services  
 Questa sezione descrive il flusso di lavoro di base per la configurazione delle autorizzazioni.  
  
 **Passaggio 1: amministrazione del server**  
  
 Decidere innanzitutto chi dovrà disporre dei diritti di amministratore a livello di server. Durante l'installazione, l'amministratore locale che installa SQL Server deve specificare uno o più account di Windows come amministratore del server di Analysis Services. Gli amministratori del server dispongono di tutte le autorizzazioni possibili in un server, compresa l'autorizzazione per visualizzare, modificare ed eliminare un oggetto nel server o visualizzare i dati associati. Al termine dell'installazione, un amministratore del server può aggiungere o rimuovere gli account per modificare l'appartenenza di questo ruolo. Per informazioni dettagliate su questo livello di autorizzazione, vedere [concedere le autorizzazioni di amministratore del Server &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) .  
  
 **Passaggio 2: amministrazione del database**  
  
 Una volta creata, la soluzione multidimensionale o tabulare viene distribuita nel server come database. Un amministratore del server può delegare le attività di amministrazione del database definendo un ruolo con autorizzazioni di Controllo completo per il database specifico. I membri di questo ruolo possono elaborare o eseguire query sugli oggetti nonché creare ruoli aggiuntivi per l'accesso a cubi, dimensioni e altri oggetti all'interno del database stesso. Per altre informazioni, vedere [Concedere autorizzazioni per il database &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md).  
  
 **Passaggio 3: abilitare l'accesso al cubo o al modello per i carichi di lavoro di elaborazione e query**  
  
 Per impostazione predefinita, solo gli amministratori del server e del database dispongono dell'accesso ai cubi e ai modelli tabulari. Per rendere queste strutture di dati disponibili ad altri utenti dell'organizzazione sono necessarie assegnazioni di ruolo aggiuntive che eseguono il mapping degli account utente e di gruppo di Windows ai cubi o modelli oltre alle autorizzazioni che specificano i privilegi `Read`. Per informazioni dettagliate, vedere [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md).  
  
 Le attività di elaborazione possono essere isolate dalle altre funzioni amministrative consentendo agli amministratori del server e del database di delegare questa attività ad altri utenti o di configurare l'elaborazione automatica specificando gli account del servizio che eseguono il software di pianificazione. Per informazioni dettagliate, vedere [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md).  
  
> [!NOTE]  
>  Gli utenti non necessitano di alcuna autorizzazione per le tabelle relazionali nel database relazionale sottostante da cui [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] carica i dati, né di alcuna autorizzazione a livello di file nel computer in cui è in esecuzione l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **Passaggio 4 (facoltativo): consentire o negare l'accesso agli oggetti interni del cubo**  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornisce le impostazioni di sicurezza per impostare le autorizzazioni su singoli oggetti, compresi i membri della dimensione e le celle all'interno di un modello di dati. Per informazioni dettagliate, vedere [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) e [Concedere l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md).  
  
 È anche possibile modificare le autorizzazioni in base all'identità utente. Tale operazione viene in genere definita sicurezza dinamica e viene implementata mediante la funzione [UserName &#40;MDX&#41;](/sql/mdx/username-mdx)  
  
## <a name="best-practices"></a>Procedure consigliate  
 Per migliorare la gestione delle autorizzazioni, è consigliabile adottare un approccio simile al seguente:  
  
1.  Creare i ruoli in base alla funzione, ad esempio dbadmin, cubedeveloper, processadmin, in modo tale che chiunque gestisca i ruoli possa visualizzare subito l'attività consentita dal ruolo. Come indicato altrove, è possibile definire i ruoli nella definizione del modello, mantenendo pertanto tali ruoli nelle distribuzioni successive della soluzione.  
  
2.  Creare un gruppo di sicurezza di Windows corrispondente in Active Directory e quindi mantenere il gruppo di sicurezza in Active Directory per assicurarsi che contenga i singoli account appropriati. In questo modo la responsabilità dell'appartenenza al gruppo di sicurezza viene affidata agli esperti della sicurezza che già conoscono gli strumenti e i processi usati per la gestione degli account nell'organizzazione.  
  
3.  Generare gli script in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in modo tale da poter replicare rapidamente le assegnazioni dei ruoli ogni volta che il modello viene ridistribuito dai relativi file di origine in un server. Per informazioni dettagliate su come generare velocemente uno script, vedere [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md).  
  
4.  Adottare una convenzione di denominazione che rifletta l'ambito e l'appartenenza del ruolo. I nomi dei ruoli sono visibili solo negli strumenti di progettazione e amministrazione. Usare pertanto una convenzione di denominazione appropriata per gli esperti della sicurezza dei cubi. Ad esempio, **processadmin-windowsgroup1** indica l'accesso in lettura oltre ai diritti di elaborazione agli utenti dell'organizzazione i cui singoli account utente di Windows sono membri del gruppo di sicurezza **windowsgroup1** .  
  
     Se si includono le informazioni sull'account è possibile tenere traccia degli account usati nei vari ruoli. Poiché i ruoli si sommano tra loro, l'insieme dei ruoli associati a **windowsgroup1** costituisce il set effettivo di autorizzazioni per gli utenti appartenenti al gruppo di sicurezza.  
  
5.  Gli sviluppatori dei cubi richiedono le autorizzazioni di Controllo completo per i modelli e i database in fase di sviluppo, ma una volta che il database viene implementato in un server di produzione sono sufficienti le autorizzazioni di Lettura. Ricordarsi di sviluppare le definizioni dei ruoli e le assegnazioni per tutti gli scenari, tra cui sviluppo, test e distribuzioni di produzione.  
  
 L'uso di un approccio come questo riduce la varianza nelle definizioni dei ruoli e nell'appartenenza ai ruoli all'interno del modello nonché fornisce visibilità nelle assegnazioni dei ruoli semplificando l'implementazione e la gestione delle autorizzazioni dei cubi.  
  
## <a name="see-also"></a>Vedere anche  
 [Concedere le autorizzazioni di amministratore del server &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Ruoli e autorizzazioni &#40;Analysis Services&#41;](roles-and-permissions-analysis-services.md)   
 [Metodologie di autenticazione supportate da Analysis Services](../instances/authentication-methodologies-supported-by-analysis-services.md)  
  
  
