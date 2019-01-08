---
title: Gestione di assembly di modelli multidimensionali | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5b7b04f074dcd11eec022a689f865454681d2ae8
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215790"
---
# <a name="multidimensional-model-assemblies-management"></a>Gestione di assembly di modelli multidimensionali
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] offre una vasta gamma di funzioni intrinseche da usare con i linguaggi MDX (Multidimensional Expressions) e DMX (Data Mining Extensions), progettate per eseguire qualsiasi tipo di operazione, dai calcoli statistici standard all'attraversamento dei membri di una gerarchia. Come avviene per qualsiasi altro prodotto complesso e affidabile, tuttavia, si avverte sempre l'esigenza di estendere ulteriormente la funzionalità di questo servizio.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente pertanto di aggiungere assembly a un database o a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Gli assembly consentono di creare funzioni esterne definite dall'utente mediante qualsiasi linguaggio Common Language Runtime (CLR), ad esempio Microsoft Visual Basic .NET o Microsoft Visual C#. È inoltre possibile utilizzare linguaggi di automazione COM (Component Object Model), ad esempio Microsoft Visual Basic o Microsoft Visual C++.  
  
> [!IMPORTANT]  
>  Gli assembly COM potrebbero comportare un rischio per la sicurezza. A causa di tale rischio e di altre considerazioni, gli assembly COM sono stati deprecati in [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)] e potrebbero non essere supportati nelle versioni future.  
  
 Gli assembly consentono di estendere la funzionalità business dei linguaggi MDX e DMX. È necessario compilare la funzionalità desiderata in una libreria, ad esempio in una libreria a collegamento dinamico (DLL), e aggiungerla come assembly a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . I metodi pubblici della libreria vengono quindi esposti come funzioni definite dall'utente in espressioni MDX e DMX, procedure, calcoli, azioni e applicazioni client.  
  
 Un assembly con nuove procedure e funzioni può essere aggiunto al server. È possibile utilizzare gli assembly per migliorare o aggiungere funzionalità personalizzate non fornite dal server. Gli assembly consentono di aggiungere nuove funzioni in formato MDX (Multidimensional Expressions) e DMX (Data Mining Extensions) o stored procedure. Gli assembly vengono caricati dal percorso di esecuzione dell'applicazione personalizzata e una copia del file binario dell'assembly viene salvata nel server insieme ai dati del database. La rimozione di un assembly implica anche la rimozione dell'assembly copiato dal server.  
  
 Gli assembly possono essere di due tipi diversi: COM e CLR. Gli assembly CLR sono sviluppati nei linguaggi di programmazione .NET Framework, ad esempio C#, Visual Basic .NET e C++ gestito. Gli assembly COM sono librerie COM che devono essere registrate nel server.  
  
 È possibile aggiungere gli assembly a oggetti <xref:Microsoft.AnalysisServices.Server> o <xref:Microsoft.AnalysisServices.Database> . Gli assembly del server possono essere chiamati da qualsiasi utente connesso al server o da un oggetto nel server. Gli assembly del database possono essere chiamati solo da oggetti <xref:Microsoft.AnalysisServices.Database> o utenti connessi al database.  
  
 Un oggetto <xref:Microsoft.AnalysisServices.Assembly> semplice è composto da informazioni di base (Nome e ID), dalla raccolta di file e dalle specifiche di sicurezza.  
  
 La raccolta di file fa riferimento ai file di assembly caricati e ai file di debug corrispondenti con estensione pdb, se i file di debug sono stati caricati con i file di assembly. I file di assembly vengono caricati dal percorso in cui sono stati definiti dall'applicazione e una copia viene salvata nel server insieme ai dati. La copia del file di assembly viene utilizzata per caricare l'assembly a ogni avvio del servizio.  
  
 Le specifiche di sicurezza includono il set di autorizzazioni e la rappresentazione utilizzata per l'esecuzione dell'assembly.  
  
## <a name="calling-user-defined-functions"></a>chiamate a funzioni definite dall'utente  
 La chiamata in un assembly di una funzione definita dall'utente viene eseguita esattamente come la chiamata di una funzione intrinseca, tranne per il fatto che è necessario utilizzare un nome completo. Una funzione definita dall'utente che restituisce un tipo previsto dal linguaggio MDX, ad esempio, viene inclusa in una query MDX come illustrato nell'esempio seguente:  
  
```  
Select MyAssembly.MyClass.MyStoredProcedure(a, b, c) on 0 from Sales  
```  
  
 È inoltre possibile chiamare le funzioni definite dall'utente mediante la parola chiave CALL. È necessario utilizzare la parola chiave CALL per le funzioni definite dall'utente che restituiscono recordset o valori void, mentre non è possibile utilizzare tale parola chiave se la funzione definita dall'utente dipende da un oggetto nel contesto dell'istruzione o dello script MDX o DMX, ad esempio il cubo o il modello di data mining corrente. In genere, una funzione chiamata al di fuori di una query MDX o DMX viene utilizzata per eseguire funzioni amministrative mediante il modello a oggetti AMO. Se ad esempio si desidera utilizzare la funzione `MyVoidProcedure(a, b, c)` in un'istruzione MDX, è necessario applicare la sintassi seguente:  
  
```  
Call MyAssembly.MyClass.MyVoidProcedure(a, b, c)  
```  
  
 Gli assembly semplificano lo sviluppo di database consentendo di scrivere una sola volta il codice comune e di archiviarlo in una singola posizione. Gli sviluppatori di software client possono creare librerie di funzioni per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e distribuirle con le applicazioni stesse.  
  
 Gli assembly e le funzioni definite dall'utente possono duplicare i nomi delle funzioni della libreria di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o di altri assembly. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzerà la procedura corretta a condizione che la funzione definita dall'utente venga chiamata utilizzando il relativo nome completo. Al fine di garantire la sicurezza ed evitare che venga chiamato un nome duplicato in una diversa libreria di classi, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] richiede l'utilizzo esclusivamente di nomi completi per le stored procedure.  
  
 Per chiamare una funzione definita dall'utente da un assembly CLR specifico, è necessario che tale funzione sia preceduta dal nome dell'assembly, dal nome completo della classe e dal nome della procedura, come illustrato di seguito:  
  
 *NomeAssembly*.*NomeCompletoClasse*.*NomeProcedura*(*Argomento1*, *Argomento2*, ...)  
  
 Per assicurare la compatibilità con le versioni precedenti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è possibile utilizzare anche la sintassi seguente:  
  
 *NomeAssembly*!*NomeCompletoClasse*!*NomeProcedura*(*Argomento1*, *Argomento2*, ...)  
  
 Se una libreria COM supporta più interfacce, è inoltre possibile utilizzare l'ID dell'interfaccia per risolvere il nome della procedura, come illustrato di seguito:  
  
 *NomeAssembly*!*IDInterfaccia*!*NomeProcedura*(*Argomento1*, *Argomento2*, ...)  
  
## <a name="security"></a>Sicurezza  
 La sicurezza degli assembly è basata sul modello di sicurezza dall'accesso di codice di .NET Framework. .NET Framework supporta un meccanismo di sicurezza dall'accesso di codice che presume che il run-time possa ospitare codice completamente o parzialmente attendibile. In genere, la sicurezza delle risorse mediante sicurezza dall'accesso di codice di .NET Framework viene eseguita tramite wrapping delle risorse con codice gestito, che richiede l'autorizzazione corrispondente prima di consentire l'accesso alla risorsa. La richiesta di autorizzazione viene soddisfatta solo se tutti i chiamanti a livello di assembly nello stack di chiamate dispongono dell'autorizzazione corrispondente per la risorsa.  
  
 Per gli assembly, l'autorizzazione relativa all'esecuzione viene passata con la proprietà **PermissionSet** sull'oggetto **Assembly** . Le autorizzazioni ricevute dal codice gestito sono determinate dai criteri di sicurezza attivi. Esistono già tre livelli di criteri in vigore in non [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ambiente ospitato: enterprise, computer e utente. L'elenco effettivo delle autorizzazioni ricevute dal codice è determinato dall'intersezione delle autorizzazioni ottenute da questi tre livelli.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] offre criteri di sicurezza a livello host per CLR, quando ospita tale ambiente. Questo livello di criteri aggiuntivo è sottostante ai tre livelli sempre attivi e viene impostato per ogni dominio applicazione creato da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 I criteri a livello host di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono una combinazione dei criteri fissi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per gli assembly di sistema e dei criteri specificati dall'utente per gli assembly utente. La parte dei criteri host di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] definita dall'utente è basata su uno dei tre bucket di autorizzazione specificati per ogni assembly dal relativo proprietario:  
  
|Impostazione dell'autorizzazione|Descrizione|  
|------------------------|-----------------|  
|**Safe**|Garantisce l'autorizzazione per calcoli interni. Questo bucket non assegna autorizzazioni per l'accesso alle risorse protette di .NET Framework. Rappresenta il bucket di autorizzazione predefinito per un assembly se non ne è stato specificato uno con la proprietà **PermissionSet** .|  
|**ExternalAccess**|Assicura lo stesso accesso dell'impostazione **Safe** , con la possibilità aggiuntiva di accedere a risorse di sistema esterne. Sebbene sia possibile proteggere questo scenario, tale bucket di autorizzazione non offre garanzie di sicurezza ma di affidabilità.|  
|**Unsafe**|Non prevede alcuna restrizione. Per il codice gestito eseguito con questo set di autorizzazioni non è possibile offrire garanzie di sicurezza o di affidabilità. A questo livello di attendibilità viene concessa infatti qualsiasi autorizzazione, anche un'autorizzazione personalizzata inclusa dall'amministratore.|  
  
 Quando CLR è ospitato in un ambiente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], il controllo delle autorizzazioni basato sul percorso stack viene arrestato al confine con il codice [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nativo. Qualsiasi codice gestito negli assembly di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rientra sempre in una delle tre categorie di autorizzazione elencate in precedenza.  
  
 Le routine di assembly COM o non gestiti non supportano il modello di sicurezza CLR.  
  
### <a name="impersonation"></a>Rappresentazione  
 Ogni volta che il codice gestito accede a una risorsa esterna a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] segue le regole associate all'impostazione della proprietà **ImpersonationMode** dell'assembly per assicurare che l'accesso venga eseguito nel contesto di sicurezza di Windows appropriato. Poiché gli assembly che usano l'impostazione di autorizzazione **Safe** non possono accedere alle risorse esterne a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], tali regole sono applicabili solo agli assembly che usano le impostazioni di autorizzazione **ExternalAccess** e **Unsafe** .  
  
-   Se il contesto di esecuzione corrente corrisponde all'account di accesso con autenticazione di Windows ed è identico al contesto del chiamante originale, ovvero non è incluso EXECUTE AS, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rappresenterà l'account di accesso con autenticazione di Windows prima di accedere alla risorsa.  
  
-   Se esiste un EXECUTE AS intermedio che ha modificato il contesto rispetto a quello del chiamante originale, il tentativo di accesso alla risorsa esterna non riuscirà.  
  
 È possibile impostare la proprietà **ImpersonationMode** su **ImpersonateCurrentUser** o su **ImpersonateAnonymous**. L'impostazione predefinita **ImpersonateCurrentUser**esegue un assembly con l'account di accesso di rete dell'utente corrente. Se viene usata l'impostazione **ImpersonateAnonymous** , il contesto di esecuzione corrisponde all'account utente di accesso di Windows IUSER_*servername* nel server. Questo rappresenta l'account Internet Guest, che dispone di privilegi limitati sul server. Un assembly eseguito in questo contesto può accedere solo a risorse limitate nel server locale.  
  
### <a name="application-domains"></a>Domini delle applicazioni  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non espone direttamente i domini delle applicazioni. Per mezzo del set degli assembly in esecuzione nello stesso dominio dell'applicazione, tali domini possono individuarsi a vicenda in fase di esecuzione usando lo spazio dei nomi **System.Reflection** di .NET Framework o in altro modo, nonché eseguire chiamate all'interno con associazione tardiva. Tali chiamate saranno soggette ai controlli delle autorizzazioni utilizzati dalla sicurezza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 La ricerca degli assembly nello stesso dominio dell'applicazione non è affidabile, poiché il confine e gli assembly di ogni dominio dell'applicazione vengono definiti dall'implementazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione della sicurezza per stored procedure](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)   
 [Definizione delle stored procedure](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
