---
title: Amministrare server tramite la gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- facet See facets
- Declarative Management Framework See Policy-Based Management
- surface area configuration [SQL Server], Policy-Based Management
- Policy-Based Management
- facets [Policy-Based Management]
- Policy-Based Management, administering
- conditions [Policy-Based Management]
- facets [Policy-Based Management], about facets
- PolicyAdministratorRole role
ms.assetid: ef2a7b3b-614b-405d-a04a-2464a019df40
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cb9d48156ecd1ca98dc36c10c2680883160582c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157095"
---
# <a name="administer-servers-by-using-policy-based-management"></a>Amministrazione di server tramite la gestione basata su criteri
  La gestione basata su criteri è un sistema per la gestione di una o più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando gli amministratori dei criteri di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzano la gestione basata su criteri, utilizzano [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare criteri per la gestione di entità nel server, quali l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], database o altri oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="benefits-of-policy-based-management"></a>Vantaggi della gestione basata su criteri  
 La gestione basata su criteri è utile per risolvere i problemi che si presentano negli scenari seguenti:  
  
-   I criteri di una società impediscono l'abilitazione di Posta elettronica database o di SQL Mail. Vengono creati i criteri per controllare lo stato del server di queste due funzionalità. Un amministratore confronta lo stato del server con i criteri. Se lo stato del server non è conforme, l'amministratore sceglie la modalità di configurazione e la conformità dello stato del server viene ripristinata dai criteri.  
  
-   Il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] utilizza una convenzione di denominazione che richiede che tutti i nomi delle stored procedure inizino con le lettere AW_. A tale scopo, vengono creati criteri. Un amministratore testa i criteri e riceve un elenco di stored procedure che non sono conformi. Se stored procedure successive non saranno conformi a questa convenzione di denominazione, le istruzioni di creazione per le stored procedure avranno esito negativo.  
  
> [!NOTE]  
>  I criteri possono influire sul funzionamento di alcune funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La funzionalità Change Data Capture e la replica transazionale, ad esempio, utilizzano entrambe la tabella systranschemas, che non dispone di un indice. Se si abilitano criteri in base ai quali tutte le tabelle devono includere un indice, l'applicazione della conformità ai criteri comporterà il mancato funzionamento di tali funzionalità.  
  
 I criteri vengono creati e gestiti tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Il processo include i passaggi seguenti:  
  
1.  Selezionare un facet della gestione basata su criteri che contiene le proprietà da configurare.  
  
2.  Definire una condizione che specifica lo stato di un facet di gestione.  
  
3.  Definire i criteri contenenti la condizione, condizioni aggiuntive per filtrare i set di destinazioni e la modalità di valutazione.  
  
4.  Verificare se un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è conforme ai criteri.  
  
 Per i criteri con errori, in Esplora oggetti viene restituito un avviso di integrità critica come icona rossa accanto alla destinazione e ai nodi di livello superiore nell'albero.  
  
> [!NOTE]  
>  Durante il calcolo del set di oggetti per i criteri, per impostazione predefinita gli oggetti di sistema sono esclusi.  Ad esempio, se il set di oggetti dei criteri si riferisce a tutte le tabelle, i criteri non verranno applicati alle tabelle di sistema. Se gli utenti desiderano valutare i criteri negli oggetti di sistema, possono aggiungere in modo esplicito questi oggetti al set di oggetti. Tuttavia, sebbene tutti i criteri siano supportati per la modalità di valutazione **Controllo su pianificazione** , per motivi di prestazioni, non tutti i criteri con i set di oggetti arbitrari sono supportati per la modalità di valutazione **Controllo su modifiche** . Per altre informazioni, vedere [https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="policy-based-management-concepts"></a>Concetti relativi alla gestione basata su criteri  
 Nella gestione basata su criteri sono inclusi tre componenti:  
  
-   Gestione dei criteri  
  
     Gli amministratori dei criteri creano i criteri.  
  
-   Amministrazione esplicita  
  
     Gli amministratori selezionano una o più destinazioni gestite e verificano in modo esplicito che tali destinazioni siano conformi a criteri specifici oppure operano in modo esplicito per rendere le destinazioni conformi ai criteri.  
  
-   Modalità di valutazione  
  
     Sono disponibili quattro modalità di valutazione, tre delle quali possono essere automatizzate:  
  
    -   **Su richiesta**. Questa modalità consente di valutare i criteri quando questi vengono specificati direttamente dall'utente.  
  
    -   **Su modifica: impedisci esecuzione**. Questa modalità automatica utilizza trigger DDL per impedire violazioni dei criteri.  
  
        > [!IMPORTANT]  
        >  Se l'opzione della configurazione del server relativa ai trigger nidificati è disabilitata, la modalità **Su modifica: impedisci esecuzione** non funzionerà correttamente. La gestione basata su criteri si basa su trigger DDL per rilevare ed eseguire il rollback di operazioni DDL non conformi ai criteri che utilizzano questa modalità di valutazione. La rimozione dei trigger DDL della gestione basata su criteri o la disabilitazione dei trigger nidificati provocherà un comportamento imprevisto o la mancata esecuzione di questa modalità di valutazione.  
  
    -   **Su modifica: solo log**. Questa modalità automatica utilizza la notifica degli eventi per valutare i criteri quando viene apportata una modifica importante.  
  
    -   **Su pianificazione**. Questa modalità automatica utilizza un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per valutare periodicamente i criteri  
  
     Quando i criteri automatici non sono abilitati, la gestione basata su criteri non influisce sulle prestazioni del sistema.  
  
## <a name="policy-based-management-terms"></a>Terminologia relativa alla gestione basata su criteri  
 Destinazione gestita della gestione basata su criteri  
 Entità gestite tramite la gestione basata su criteri, ad esempio un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], un database, una tabella o un indice. Tutte le destinazioni in un'istanza del server formano una gerarchia di destinazioni. Un set di destinazioni è il set risultante dall'applicazione di un set di filtri di destinazione alla gerarchia di destinazioni, ad esempio tutte le tabelle del database di proprietà dello schema HumanResources.  
  
 Facet della gestione basata su criteri  
 Set di proprietà logiche che definiscono il comportamento o le caratteristiche di certi tipi di destinazioni gestite. Il numero e le caratteristiche delle proprietà vengono incorporati nel facet e possono essere aggiunti o rimossi solo dal creatore del facet. Un tipo di destinazione può implementare uno o più facet di gestione e un facet di gestione può essere implementato da uno o più tipi di destinazione. Alcune proprietà di un facet possono essere valide solo per una versione specifica.  
  
 Condizione della gestione basata su criteri  
 Espressione booleana che specifica un set di stati consentiti per una destinazione gestita tramite la gestione basata su criteri in relazione a un facet di gestione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta di osservare le regole di confronto in caso di valutazione di una condizione. Quando le regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non corrispondono esattamente a quelle di Windows, testare la condizione per determinare come risolvere i conflitti dell'algoritmo.  
  
 Criteri di gestione basata su criteri  
 Condizione della gestione basata su criteri e comportamento previsto, ad esempio la modalità di valutazione, i filtri di destinazione e la pianificazione. I criteri possono contenere solo una condizione. I criteri possono essere abilitati o disabilitati. I criteri vengono archiviati nel database msdb.  
  
 Categoria di criteri della gestione basata su criteri  
 Categoria definita dall'utente per semplificare la gestione dei criteri. Gli utenti possono classificare i criteri in diverse categorie. I criteri appartengono esclusivamente a un'unica categoria di criteri. Le categorie di criteri si applicano a database e server. Applicare le condizioni seguenti a livello di database:  
  
-   I proprietari del database possono sottoscrivere un set di categorie di criteri per un database.  
  
-   Solo i criteri delle categorie sottoscritte possono controllare un database.  
  
-   Tutti i database sottoscrivono implicitamente la categoria di criteri predefinita.  
  
 A livello di server, le categorie di criteri possono essere applicate a tutti i database.  
  
 Criteri validi  
 Vengono considerati validi per una destinazione i criteri che la controllano. I criteri sono validi in relazione a una destinazione solo se si verificano tutte le condizioni seguenti:  
  
-   I criteri sono abilitati.  
  
-   La destinazione appartiene al set di destinazioni dei criteri.  
  
-   La destinazione o uno dei predecessori delle destinazioni sottoscrive il gruppo di criteri che contiene i criteri.  
  
## <a name="policy-based-management-tasks"></a>Attività di gestione basata su criteri  
 La gestione basata su criteri è un sistema basato su criteri per la gestione di una o più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilizzare la gestione basata su criteri per creare condizioni contenenti espressioni. Creare quindi i criteri per l'applicazione delle condizioni a oggetti di destinazione del database.  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritta la modalità di archiviazione dei criteri della gestione basata su criteri.|Archiviazione di gestione basata su criteri|  
|Viene descritto come configurare gli avvisi per notificare errori dei criteri agli amministratori.|[Configurare avvisi per notificare agli amministratori eventuali errori dei criteri](configure-alerts-to-notify-policy-administrators-of-policy-failures.md)|  
|Viene descritto come creare, visualizzare, modificare ed eliminare una condizione di gestione basata su criteri.|[Creare una nuova condizione della gestione basata su criteri](create-a-new-policy-based-management-condition.md)<br /><br /> [Eliminare una condizione della gestione basata su criteri](delete-a-policy-based-management-condition.md)<br /><br /> [Visualizzare o modificare le proprietà di una condizione della gestione basata su criteri](view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
|Viene descritto come creare, visualizzare, modificare ed eliminare criteri di gestione basata su criteri|[Creare i criteri della gestione basata su criteri](create-a-policy-based-management-policy.md)<br /><br /> [Eliminare i criteri della gestione basata su criteri](delete-a-policy-based-management-policy.md)<br /><br /> [Visualizzare o modificare le proprietà dei criteri della gestione basata su criteri](view-or-modify-the-properties-of-a-policy-based-management-policy.md)|  
|Viene descritto come esportare e importare criteri di gestione basata su criteri.|[Esportare i criteri della gestione basata su criteri](export-a-policy-based-management-policy.md)<br /><br /> [Importare i criteri della gestione basata su criteri](import-a-policy-based-management-policy.md)|  
|Viene descritto come verificare che un'istanza server, un database, un oggetto server o un oggetto di database sia conforme ai criteri.|[Valutare i criteri della gestione basata su criteri da un oggetto](evaluate-a-policy-based-management-policy-from-an-object.md)<br /><br /> [Valutare i criteri della gestione basata su criteri da quei criteri](evaluate-a-policy-based-management-policy-from-that-policy.md)<br /><br /> [Valutare i criteri della gestione basata su criteri in una pianificazione](evaluate-a-policy-based-management-policy-on-a-schedule.md)|  
|Viene descritto come visualizzare e copiare uno stato facet di gestione basata su criteri in un file.|[Utilizzo della copia di facet della gestione basata su criteri](working-with-policy-based-management-facets.md)|  
|È disponibile un set di file di criteri che è possibile importare per le procedure consigliate e viene descritto come valutare i criteri rispetto a un set di destinazione con istanze, oggetti di istanza, database e oggetti di database.|[Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](monitor-and-enforce-best-practices-by-using-policy-based-management.md)|  
|Sono inclusi gli argomenti della Guida F1 relativi al nodo **Gestione criteri** di Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|[Nodo Gestione criteri di &#40;Esplora oggetti&#41;](../../ssms/object/object-explorer.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di Gestione basata su criteri &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/policy-based-management-views-transact-sql)  
  
  
