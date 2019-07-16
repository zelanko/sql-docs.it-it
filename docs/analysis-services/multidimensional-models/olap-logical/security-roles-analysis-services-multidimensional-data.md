---
title: I ruoli di sicurezza (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a1e373d4e12cc2d050bc963aeb310e6c2ed53b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165629"
---
# <a name="security-roles--analysis-services---multidimensional-data"></a>Ruoli di sicurezza (Analysis Services - Dati multidimensionali)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  I ruoli vengono utilizzati in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] per gestire la sicurezza di oggetti e dati di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . In termini di base, un ruolo associa gli identificatori di sicurezza (SID) di utenti e gruppi di Microsoft Windows per cui sono stati definiti autorizzazioni e diritti di accesso specifici per gli oggetti gestiti da un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. In [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]sono disponibili due tipi di ruoli:  
  
-   Ruolo del server, ovvero un ruolo fisso che garantisce l'accesso come amministratore a un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   Ruoli di database, ruoli definiti dagli amministratori per controllare l'accesso a oggetti e dati per gli utenti non amministratori.  
  
 In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] la sicurezza è gestita mediante i ruoli e le autorizzazioni. I ruoli sono gruppi di utenti. Gli utenti, denominati anche membri, possono essere aggiunti o rimossi dai ruoli. Le autorizzazioni per gli oggetti sono specificate dai ruoli e tutti i membri di un ruolo possono utilizzare gli oggetti per i quali il ruolo dispone delle autorizzazioni. Tutti i membri di un ruolo dispongono delle stesse autorizzazioni per gli oggetti. Le autorizzazioni sono specifiche degli oggetti: per ciascun oggetto è disponibile una raccolta delle autorizzazioni concesse su di esso. A un oggetto possono essere concessi diversi set di autorizzazioni. A ogni autorizzazione presente nella raccolta delle autorizzazioni dell'oggetto è assegnato un solo ruolo.  
  
## <a name="role-and-role-member-objects"></a>Oggetti ruolo e membri del ruolo  
 Un ruolo è un oggetto contenitore per una raccolta di utenti (membri). Una definizione di ruolo stabilisce l'appartenenza degli utenti in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Poiché le autorizzazioni sono assegnate per ruolo, è necessario che un utente sia membro di un ruolo affinché possa accedere a un oggetto.  
  
 Un oggetto <xref:Microsoft.AnalysisServices.Role> è composto dai parametri Name, ID e Members. Members rappresenta una raccolta di stringhe. Ciascun membro contiene il nome utente nel formato "dominio\nome utente". Name è una stringa che contiene il nome del ruolo. ID è una stringa che contiene l'identificatore univoco del ruolo.  
  
### <a name="server-role"></a>Ruolo del server  
 Il ruolo del server di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] definisce l'accesso amministrativo di utenti e gruppi di Windows a un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. I membri di questo ruolo hanno accesso a tutti i database e gli oggetti di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e possono eseguire le seguenti attività:  
  
-   Eseguire funzioni amministrative a livello di server utilizzando SQL Server Management Studio o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], incluse la creazione di database e l'impostazione di proprietà a livello di server.  
  
-   Eseguire funzioni amministrative a livello di programmazione con la libreria AMO (Analysis Management Objects).  
  
-   Gestire i ruoli di database di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
-   Avviare tracce, per finalità diverse dall'elaborazione degli eventi che può essere eseguita da un ruolo di database con accesso di tipo Process.  
  
 Ogni istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dispone di un ruolo del server che definisce gli utenti che possono amministrare l'istanza. A differenza dei ruoli di database, questo ruolo, con nome e ID "Administrators", non può essere eliminato. Non è inoltre possibile aggiungere o rimuovere autorizzazioni. In altri termini, un utente è un amministratore per un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]o meno a seconda della relativa inclusione nel ruolo del server per tale istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
### <a name="database-roles"></a>Ruoli di database  
 Un ruolo di database di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] definisce l'accesso degli utenti a oggetti e dati di un database di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Un ruolo di database viene creato come oggetto separato in un database di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e viene applicato soltanto al database in cui è stato creato. Utenti e gruppi di Windows vengono inclusi nel ruolo da un amministratore, che definisce inoltre le autorizzazioni all'interno del ruolo.  
  
 Le autorizzazioni di un ruolo consentono ai membri di accedere al database e amministrarlo, in aggiunta agli oggetti e ai dati all'interno del database. A ogni autorizzazione è associato uno o più diritti di accesso, in grado di garantire all'autorizzazione un maggiore controllo sull'accesso a un determinato oggetto del database.  
  
## <a name="permission-objects"></a>Oggetti Permission  
 Le autorizzazioni sono associate a un oggetto (cubo, dimensione e così via) di un determinato ruolo e determinano le operazioni che il membro del ruolo in questione può eseguire sull'oggetto.  
  
 La classe <xref:Microsoft.AnalysisServices.Permission> è astratta. È pertanto necessario utilizzare le classi derivate per definire le autorizzazioni per gli oggetti corrispondenti. Per ogni oggetto è definita una classe derivata dell'autorizzazione.  
  
|Object|Class|  
|------------|-----------|  
|<xref:Microsoft.AnalysisServices.Database>|<xref:Microsoft.AnalysisServices.DatabasePermission>|  
|<xref:Microsoft.AnalysisServices.DataSource>|<xref:Microsoft.AnalysisServices.DataSourcePermission>|  
|<xref:Microsoft.AnalysisServices.Dimension>|<xref:Microsoft.AnalysisServices.DimensionPermission>|  
|<xref:Microsoft.AnalysisServices.Cube>|<xref:Microsoft.AnalysisServices.CubePermission>|  
|<xref:Microsoft.AnalysisServices.MiningStructure>|<xref:Microsoft.AnalysisServices.MiningStructurePermission>|  
|<xref:Microsoft.AnalysisServices.MiningModel>|<xref:Microsoft.AnalysisServices.MiningModelPermission>|  
  
 Nell'elenco sono riportate le azioni possibili attivate dalle autorizzazioni:  
  
|Action|Valori|Spiegazione|  
|------------|------------|-----------------|  
|Process|{**true**, **false**}<br /><br /> Valore predefinito =**false**|Se **true**, i membri possono elaborare l'oggetto e qualsiasi altro oggetto in esso contenuto.<br /><br /> Le autorizzazioni di elaborazione non si applicano ai modelli di data mining. Le autorizzazioni <xref:Microsoft.AnalysisServices.MiningModel> sono ereditate sempre da <xref:Microsoft.AnalysisServices.MiningStructure>.|  
|ReadDefinition|{**None**, **Basic**, **Allowed**}<br /><br /> Valore predefinito =**None**|Specifica se i membri possono leggere la definizione dei dati (ASSL) associata all'oggetto.<br /><br /> Se **Allowed**, i membri possono leggere la definizione ASSL associata all'oggetto.<br /><br /> I valori**Basic** e **Allowed** sono ereditati dagli oggetti contenuti nell'oggetto. **Allowed** sovrascrive **Basic** e **None**.<br /><br /> **Allowed** è richiesto per DISCOVER_XML_METADATA su un oggetto. **Basic** è necessario per creare oggetti collegati e cubi locali.|  
|Lettura|{**None**, **Allowed**}<br /><br /> Valore predefinito =**None** (tranne per DimensionPermission, il cui valore predefinito =**Allowed**)|Specifica se i membri dispongono dell'accesso in lettura al set di righe dello schema e al contenuto dei dati.<br /><br /> **Allowed** fornisce l'accesso in lettura per un database, che consente di individuare un database.<br /><br /> **Consentita** un cubo fornisce l'accesso in lettura in set di righe dello schema e l'accesso al contenuto del cubo (a meno che non vincolato dal <xref:Microsoft.AnalysisServices.CellPermission> e <xref:Microsoft.AnalysisServices.CubeDimensionPermission>).<br /><br /> **Consentita** una dimensione concede l'autorizzazione in tutti gli attributi nella dimensione di lettura (a meno che non vincolato da <xref:Microsoft.AnalysisServices.CubeDimensionPermission>). L'autorizzazione alla lettura è utilizzata solamente per l'ereditarietà statica a <xref:Microsoft.AnalysisServices.CubeDimensionPermission>. Il valore**None** per una dimensione nasconde la dimensione e fornisce al membro predefinito solo l'accesso agli attributi aggregabili. Se la dimensione contiene un attributo non aggregabile, viene generato un errore.<br /><br /> **Consentita** su un <xref:Microsoft.AnalysisServices.MiningModelPermission> concede le autorizzazioni per visualizzare gli oggetti nei set di righe dello schema e per l'esecuzione di PREDICTION JOIN.<br /><br /> **NoteAllowed** è necessario per leggere o scrivere su qualsiasi oggetto nel database.|  
|Scrittura|{**None**, **Allowed**}<br /><br /> Valore predefinito =**None**|Specifica se i membri dispongono dell'accesso in scrittura ai dati dell'oggetto padre.<br /><br /> L'accesso si applica alle sottoclassi <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube> e <xref:Microsoft.AnalysisServices.MiningModel>, ma non alle sottoclassi <xref:Microsoft.AnalysisServices.MiningStructure> del database. In questo caso, viene generato un errore di convalida.<br /><br /> **Consentita** su un <xref:Microsoft.AnalysisServices.Dimension> concede l'autorizzazione di scrittura in tutti gli attributi nella dimensione.<br /><br /> **Consentita** su un <xref:Microsoft.AnalysisServices.Cube> concessioni di autorizzazione di scrittura per le celle del cubo delle partizioni definite come tipo = writeback.<br /><br /> **Consentita** su un <xref:Microsoft.AnalysisServices.MiningModel> concede l'autorizzazione per modificare il contenuto del modello.<br /><br /> **Consentita** su una <xref:Microsoft.AnalysisServices.MiningStructure> non ha alcun significato specifico [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Nota: Scrittura non può essere impostata su **Allowed** a meno che non viene impostata su lettura **consentiti**|  
|Amministrazione<br /><br /> Nota: Solo nelle autorizzazioni di Database|{**true**, **false**}<br /><br /> Valore predefinito =**false**|Specifica se i membri possono amministrare un database.<br /><br /> **true** concede ai membri l'accesso a tutti gli oggetti in un database.<br /><br /> Un membro può disporre delle autorizzazioni Administer per un database specifico, ma non per altri database.|  
  
## <a name="see-also"></a>Vedere anche  
 [Le autorizzazioni e diritti di accesso &#40;Analysis Services - dati multidimensionali&#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Autorizzazione dell'accesso a oggetti e operazioni &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
  
