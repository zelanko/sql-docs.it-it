---
title: Ruoli (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77114194f36ac24ff34e48b580513a939d8a4467
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66066632"
---
# <a name="roles-ssas-tabular"></a>Ruoli (SSAS tabulare)
  I ruoli, nei modelli tabulari, consentono di definire le autorizzazioni dei membri per un modello. In ogni ruolo sono contenuti membri, in base al nome utente o gruppo di Windows, e autorizzazioni, ad esempio per la lettura, l'elaborazione e l'amministratore. I membri del ruolo possono eseguire azioni sul modello, come definito dall'autorizzazione del ruolo. I ruoli definiti con autorizzazioni di lettura possono garantire inoltre sicurezza aggiuntiva a livello di riga tramite i relativi filtri.  
  
> [!IMPORTANT]  
>  Affinché gli utenti possano connettersi a un modello distribuito tramite un'applicazione client di creazione report e di analisi dei dati, è necessario creare come minimo un ruolo che disponga almeno dell'autorizzazione di lettura di cui tali utenti sono membri.  
  
 Le informazioni contenute in questo argomento sono destinate agli autori di modelli tabulari che definiscono i ruoli tramite la finestra di dialogo Gestione ruoli in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. I ruoli definiti durante la creazione di modelli vengono applicati al database dell'area di lavoro modello. Al termine della distribuzione di un database modello, gli amministratori di tale database possono gestire, aggiungere, modificare o eliminare membri del ruolo usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni sulla gestione di membri di ruoli in un database distribuito, vedere [Ruoli nei modelli tabulari &#40;SSAS tabulare&#41;](tabular-model-roles-ssas-tabular.md).  
  
 [Modellazione tabulare &#40;esercitazione di AdventureWorks&#41;](../tabular-modeling-adventure-works-tutorial.md) include informazioni aggiuntive e lezioni su come usare questa funzionalità.  
  
 Sezioni dell'argomento:  
  
-   [Informazioni sui ruoli](#bkmk_underst)  
  
-   [Permissions](#bkmk_permissions)  
  
-   [Filtri di riga](#bkmk_rowfliters)  
  
-   [Test dei ruoli](#bkmk_testroles)  
  
-   [Attività correlate](#bkmk_rt)  
  
##  <a name="bkmk_underst"></a> Informazioni sui ruoli  
 I ruoli vengono usati in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per gestire la sicurezza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e dei dati. Sono disponibili due tipi di ruoli in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   Ruolo del server, ovvero un ruolo fisso che garantisce l'accesso come amministratore a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Ruoli del database, ovvero ruoli definiti dagli autori e amministratori di modelli per controllare l'accesso al database modello e ai dati per utenti non amministratori.  
  
 I ruoli definiti per un modello tabulare sono ruoli del database. Ovvero, nei ruoli sono inclusi membri costituiti da utenti o gruppi di Windows che dispongono di autorizzazioni specifiche mediante le quali è possibile definire l'azione che possono intraprendere tali membri sul database modello. Un ruolo del database viene creato come oggetto separato nel database e viene applicato soltanto al database in cui è stato creato tale ruolo. Gli utenti e/o gruppi di Windows sono inclusi nel ruolo dall'autore del modello che, per impostazione predefinita, dispone delle autorizzazioni di amministratore sul server del database dell'area di lavoro e, per un modello distribuito, da un amministratore.  
  
 I ruoli nei modelli tabulari possono essere definiti ulteriormente con filtri di riga. Per questi ultimi vengono utilizzate le espressioni DAX per definire le righe in una tabella e tutte le righe correlate nelle numerose direzioni in cui un utente può effettuare query. I filtri di riga tramite espressioni DAX possono essere definiti solo per le autorizzazioni di lettura e di lettura ed elaborazione. Per altre informazioni, vedere la sezione [Filtri di riga](#bkmk_rowfliters) più avanti in questo argomento.  
  
 Per impostazione predefinita, quando si crea un nuovo progetto di modello tabulare, il progetto di modello non dispone di alcun ruolo. I ruoli possono essere definiti tramite la finestra di dialogo Gestione ruoli di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Quando i ruoli vengono definiti durante la creazione di modelli, essi vengono applicati al database dell'area di lavoro modello. Quando viene distribuito il modello, gli stessi ruoli vengono applicati al modello distribuito. Al termine della distribuzione di un modello, i membri dei ruoli server (amministratore di[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ) e gli amministratori di database possono gestire i ruoli associati al modello e i membri associati a ciascun ruolo tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  Per i ruoli definiti per un modello configurato per la modalità DirectQuery non possono essere utilizzati filtri di riga; tuttavia, verranno applicate le autorizzazioni definite per ogni ruolo.  
  
##  <a name="bkmk_permissions"></a> Autorizzazioni  
 Ogni ruolo dispone di una singola autorizzazione definita per il database, eccetto l'autorizzazione combinata di lettura ed elaborazione. Per impostazione predefinita, un nuovo ruolo disporrà dell'autorizzazione Nessuno. Ovvero, una volta che i membri sono stati aggiunti al ruolo con l'autorizzazione Nessuno, non possono modificare il database, eseguire operazioni di elaborazione, eseguire query sui dati né esaminare il database, a meno che non venga concessa un'autorizzazione diversa.  
  
 Un gruppo o utente di Windows può essere membro di un qualsiasi numero di ruoli, ognuno dei quali con un'autorizzazione diversa. Se un utente è membro di più ruoli, le autorizzazioni definite per ogni ruolo sono cumulative. Ad esempio, se un utente è membro di un ruolo con l'autorizzazione di lettura, e anche membro di un ruolo con l'autorizzazione Nessuno, tale utente disporrà delle autorizzazioni di lettura.  
  
 Ciascun ruolo può disporre di una delle seguenti autorizzazioni definite:  
  
|Permissions|Descrizione|Filtri di riga tramite DAX|  
|-----------------|-----------------|----------------------------|  
|None|I membri non possono apportare alcuna modifica allo schema del database modello, né eseguire query sui dati.|Filtri di riga non applicabili. Agli utenti con questo ruolo non è visibile alcun dato.|  
|lettura|I membri possono eseguire query sui dati, in base ai filtri di riga, ma non possono visualizzare il database modello in SSMS, né possono apportare modifiche allo schema del database modello e l'utente non può elaborare il modello.|Filtri di riga applicabili. Agli utenti sono visibili solo i dati specificati nella formula DAX del filtro di riga.|  
|Lettura ed elaborazione|I membri possono eseguire query sui dati in base ai filtri a livello di riga ed effettuare operazioni di elaborazione eseguendo uno script o un pacchetto contenente un comando di elaborazione, ma non possono apportare alcuna modifica al database, né visualizzare il database modello in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|Filtri di riga applicabili. È possibile eseguire query solo sui dati specificati nella formula DAX del filtro di riga.|  
|Process|I membri possono effettuare operazioni di elaborazione eseguendo uno script o un pacchetto contenente un comando di elaborazione. Non è possibile modificare lo schema del database modello, Non è eseguire query sui dati. Non è possibile eseguire query sul database modello in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|Filtri di riga non applicabili. Non è possibile eseguire query sui dati in questo ruolo|  
|Amministratore|I membri possono apportare modifiche allo schema del modello ed eseguire query su tutti i dati in Progettazione modelli, nel client di creazione report e in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|Filtri di riga non applicabili. È possibile eseguire query su tutti i dati in questo ruolo.|  
  
##  <a name="bkmk_rowfliters"></a> Filtri di riga  
 I filtri di riga consentono di definire su quali righe di una tabella i membri di un determinato ruolo possono eseguire query e vengono definiti per ogni tabella in un modello tramite formule DAX.  
  
 I filtri di riga possono essere definiti solo per ruoli con le autorizzazioni di lettura e di lettura ed elaborazione. Per impostazione predefinita, se per una particolare tabella non è stato definito alcun filtro di riga, i membri di un ruolo con l'autorizzazione di lettura o di lettura ed elaborazione saranno in grado di eseguire query su tutte le righe della tabella, a meno che non venga applicato il filtro incrociato da un'altra tabella.  
  
 Una volta definito un filtro di riga per una determinata tabella, una formula DAX da cui deve essere restituito un valore TRUE o FALSE, tale filtro consente di definire le righe in cui i membri di tale particolare ruolo possono eseguire query. Non sarà possibile eseguire query sulle righe non incluse nella formula DAX. Ad esempio, per i membri del ruolo relativo alle vendite, la tabella Customers con la riga seguente espressione dei filtri, *= Customers [Country] = 'USA'*, i membri del ruolo relativo alle vendite, sarà solo in grado di visualizzare i clienti negli Stati Uniti.  
  
 I filtri di riga vengono applicati alle righe specificate e a quelle correlate. Quando una tabella dispone di più relazioni, tramite i filtri viene applicata la sicurezza alla relazione che è attiva. I filtri di riga saranno intersecati con altri relativi filtri definiti per le tabelle correlate, ad esempio:  
  
|Tabella|Espressione DAX|  
|-----------|--------------------|  
|Region|= Area [Paese] = 'USA'|  
|ProductCategory|= ProductCategory [nome] = "Biciclette"|  
|Transazioni|=Transactions[Year]=2008|  
  
 Il risultato finale di queste autorizzazioni nella tabella Transactions è che i membri potranno eseguire query sulle righe di dati se il cliente si trova negli Stati Uniti, la categoria di prodotto è quella delle biciclette e l'anno è il 2008. Gli utenti non saranno in grado di eseguire query su alcuna transazione al di fuori degli Stati Uniti, che non riguardi biciclette o che non appartenga al 2008, a meno che non siano membri di un altro ruolo che garantisce tali autorizzazioni.  
  
 È possibile usare il filtro, *=FALSE()*, per negare l'accesso a tutte le righe per un'intera tabella.  
  
### <a name="dynamic-security"></a>Sicurezza dinamica  
 La sicurezza dinamica offre una modalità per definire la sicurezza a livello di riga in base al nome dell'utente attualmente connesso o alla proprietà CustomData restituita da una stringa di connessione. Per implementare la sicurezza dinamica, è necessario includere nel modello una tabella con i valori di accesso (nome utente di Windows) per gli utenti e un campo che è possibile utilizzare per definire una particolare autorizzazione; ad esempio, una tabella dimEmployees con un ID di accesso (dominio\nomeutente) e un valore di reparto per ogni dipendente.  
  
 Per implementare la sicurezza dinamica, è possibile utilizzare le funzioni seguenti come parte di una formula DAX per restituire il nome dell'utente attualmente connesso o la proprietà CustomData in una stringa di connessione:  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[USERNAME Function &#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)|Viene restituito il valore dominio\nomeutente dell'utente attualmente connesso.|  
|[Funzione CUSTOMDATA &#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)|Viene restituita la proprietà CustomData in una stringa di connessione.|  
  
 È possibile utilizzare la funzione LOOKUPVALUE per restituire valori per una colonna in cui il nome utente di Windows corrisponde al nome utente restituito dalla funzione USERNAME o una stringa restituita dalla funzione CustomData. Le query possono quindi essere limitate nel caso in cui i valori restituiti da LOOKUPVALUE corrispondono ai valori nella stessa tabella o in una tabella correlata.  
  
 Ad esempio, utilizzando la formula:  
  
 `='dimDepartmentGroup'[DepartmentGroupId]=LOOKUPVALUE('dimEmployees'[DepartmentGroupId], 'dimEmployees'[LoginId], USERNAME(), 'dimEmployees'[LoginId], 'dimDepartmentGroup'[DepartmentGroupId])`  
  
 La funzione LOOKUPVALUE restituisce valori per la colonna dimEmployees[DepartmentId] dove dimEmployees[LoginId] corrisponde al valore LoginID dell'utente attualmente connesso, restituito da USERNAME e i valori per dimEmployees[DepartmentId] corrispondono ai valori per dimDepartmentGroup[DepartmentId]. I valori in DepartmentId restituiti da LOOKUPVALUE vengono quindi utilizzati per limitare le righe in cui vengono eseguite query nella tabella dimDepartment e qualsiasi tabella correlata da DepartmentId. Vengono restituite solo le righe in cui DepartmentId è presente anche nei valori per DepartmentId restituiti da LOOKUPVALUE.  
  
 **dimEmployees**  
  
|LastName|FirstName|LoginID|DepartmentName|DepartmentId|  
|--------------|---------------|-------------|--------------------|------------------|  
|Brown|Kevin|Adventure-works\kevin0|Marketing|7|  
|Bradley|David|Adventure-works\david0|Marketing|7|  
|Dobney|JoLynn|Adventure-works\JoLynn0|Production|4|  
|Baretto DeMattos|Paula|Adventure-works\Paula0|Human Resources|2|  
  
 **dimDepartment**  
  
|DepartmentId|DepartmentName|  
|------------------|--------------------|  
|1|Corporate|  
|2|Executive General and Administration|  
|3|Inventory Management|  
|4|Manufacturing|  
|5|Quality Assurance|  
|6|Research and Development|  
|7|Sales and Marketing|  
  
##  <a name="bkmk_testroles"></a> Test dei ruoli  
 Quando si crea un progetto di modello, è possibile utilizzare la funzionalità Analizza in Excel in Progettazione modelli per eseguire un test circa l'efficacia dei ruoli definiti. Se si sceglie **Analizza in Excel** dal menu **Modello**in Progettazione modelli prima che venga aperto Excel, viene visualizzata la finestra di dialogo **Choose Credentials and Perspective** (Scegli credenziali e prospettiva). In questa finestra di dialogo è possibile specificare il nome utente corrente, un nome utente diverso, un ruolo e una prospettiva che verranno utilizzati per la connessione al modello dell'area di lavoro come origine dati. Per altre informazioni, vedere la sezione [Analizzare in Excel &#40;SSAS tabulare&#41;](analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Creare e gestire ruoli &#40;SSAS tabulare&#41;](create-and-manage-roles-ssas-tabular.md)|Nelle attività di questo argomento viene descritto come creare e gestire ruoli tramite la finestra di dialogo **Gestione ruoli** .|  
  
## <a name="see-also"></a>Vedere anche  
 [Prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md)   
 [Analizzare in Excel &#40;SSAS tabulare&#41;](analyze-in-excel-ssas-tabular.md)   
 [USERNAME Function &#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)   
 [Funzione LOOKUPVALUE &#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx)   
 [Funzione CUSTOMDATA &#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)  
  
  
