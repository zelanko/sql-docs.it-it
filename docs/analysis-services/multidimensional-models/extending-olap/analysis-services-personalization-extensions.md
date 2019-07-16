---
title: Analysis Services Personalization Extensions | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 85d4761b228a8b79e6c90ca0aa7f0c9a32738a03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208905"
---
# <a name="analysis-services-personalization-extensions"></a>Analysis Services Personalization Extensions
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] le estensioni della personalizzazione sono alla base di base dell'implementazione di un'architettura plug-in. In un'architettura plug-in è possibile sviluppare dinamicamente nuovi oggetti cubo e funzionalità e condividerli facilmente con gli altri sviluppatori. Di conseguenza, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] estensioni della personalizzazione forniscono le funzionalità che rende possibile raggiungere i seguenti obiettivi:  
  
-   **Progettazione e distribuzione dinamiche** immediatamente dopo la progettazione e distribuzione [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] estensioni della personalizzazione, gli utenti hanno accesso a oggetti e alle funzionalità all'inizio della sessione successiva.  
  
-   **Indipendenza dell'interfaccia** indipendentemente dall'interfaccia che consente di creare il [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] estensioni della personalizzazione, gli utenti possono usare qualsiasi interfaccia per accedere a oggetti e alle funzionalità.  
  
-   **Contesto della sessione** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] estensioni della personalizzazione non sono oggetti permanenti nell'infrastruttura esistente e non richiedono il rielaborazione del cubo. Vengono esposti e creati per l'utente al momento della connessione al database e rimangono disponibili per la durata della sessione dell'utente.  
  
-   **Distribuzione rapida** condivisione [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] le estensioni della personalizzazione con altri sviluppatori di software senza dover passare in specifiche dettagliate su dove o come trovare la funzionalità estesa.  
  
 Le estensioni della personalizzazione di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] possono essere utilizzate per diversi scopi. Ad esempio, la propria azienda dispone di vendite che hanno valute diverse. Viene creato un membro calcolato che restituisce le vendite consolidate nella valuta locale della persona che accede al cubo. Tale membro viene creato come estensione della personalizzazione. Il membro calcolato viene quindi condiviso con un gruppo di utenti. Una volta condiviso, tali utenti hanno accesso immediato al membro calcolato non appena si connettono al server. anche se non utilizzano la stessa interfaccia utilizzata durante la creazione del membro calcolato.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] le estensioni della personalizzazione sono una semplice ed elegante modifica all'architettura dell'assembly gestita esistente e vengono esposti in tutta il [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] <xref:Microsoft.AnalysisServices.AdomdServer> dell'oggetto modello, la sintassi MDX (Multidimensional Expressions) e i set di righe dello schema.  
  
## <a name="logical-architecture"></a>Architettura logica  
 L'architettura delle estensioni della personalizzazione di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] è basata sull'architettura dell'assembly gestita e sui quattro elementi di base seguenti:  
  
 Attributo personalizzato [PlugInAttribute]  
 All'avvio del servizio [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carica gli assembly necessari e determina quali classi dispongono di <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> attributo personalizzato.  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] definisce gli attributi personalizzati come un modo per descrivere il codice e influisce sul comportamento in fase di esecuzione. Per altre informazioni, vedere l'argomento "[Cenni preliminari sugli attributi](http://go.microsoft.com/fwlink/?LinkId=82929)," nel [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Guida per sviluppatori su MSDN.  
  
 Per tutte le classi con il <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> dell'attributo personalizzato, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] richiama i costruttori predefiniti. Richiamare tutti i costruttori all'avvio fornisce un percorso comune da cui compilare nuovi oggetti e che è indipendente da qualsiasi attività dell'utente.  
  
 Oltre a compilare una piccola cache di informazioni sulla creazione e sulla gestione di estensioni della personalizzazione, in genere il costruttore sottoscrive gli eventi <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> e <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>. Se la sottoscrizione di tali eventi non riesce, la classe potrebbe essere erroneamente contrassegnata per la pulizia da parte del Garbage Collector del Common Language Runtime.  
  
 Contesto di sessione  
 Per gli oggetti basati sulle estensioni della personalizzazione, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea un ambiente di esecuzione durante la sessione client e compila dinamicamente la maggior parte degli oggetti dell'ambiente. Come qualsiasi altro assembly CLR, tale ambiente di esecuzione dispone anche dell'accesso ad altre funzioni e stored procedure. Al termine della sessione utente, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] rimuove gli oggetti generati dinamicamente e chiude l'ambiente di esecuzione.  
  
 Events  
 La creazione di oggetti viene attivata dagli eventi di sessione **OpenedCubeOpened nel cubo** e **ClosingCubeClosing nel cubo**.  
  
 La comunicazione tra client e server si verifica attraverso eventi specifici. Tali eventi informano il client delle situazioni che portano alla compilazione degli oggetti del client. L'ambiente del client viene creato dinamicamente utilizzando due set di eventi: eventi di sessione ed eventi del cubo.  
  
 Gli eventi di sessione sono associati all'oggetto server. Quando un client accede a un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea una sessione e i trigger di <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> evento. Quando un client termina la sessione nel server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] trigger di <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> evento.  
  
 Gli eventi del cubo sono associati all'oggetto connessione. La connessione a un cubo genera l'evento <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>. La chiusura della connessione a un cubo, tramite la chiusura del cubo o il passaggio a un cubo diverso, genera un evento <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>.  
  
 Tracciabilità e gestione degli errori  
 Tutte le attività sono tracciabili utilizzando [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Gli errori non gestiti vengono segnalati al registro eventi di Windows.  
  
 La creazione e la gestione degli oggetti sono indipendenti dall'architettura e rappresentano l'unica responsabilità degli sviluppatori degli oggetti.  
  
## <a name="infrastructure-foundations"></a>Base dell'infrastruttura  
 Le estensioni della personalizzazione di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sono basate su componenti esistenti. Di seguito è riportato un riepilogo dei miglioramenti forniti dalla funzionalità delle estensioni della personalizzazione.  
  
### <a name="assemblies"></a>Assembly  
 L'attributo personalizzato <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> può essere aggiunto agli assembly personalizzati per identificare le classi delle estensioni della personalizzazione di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
### <a name="changes-to-the-adomdserver-object-model"></a>Modifiche al modello a oggetti AdomdServer  
 Gli oggetti seguenti nel modello a oggetti <xref:Microsoft.AnalysisServices.AdomdServer> sono stati migliorati o aggiunti al modello.  
  
#### <a name="new-adomdconnection-class"></a>Nuova classe AdomdConnection  
 La classe <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> è nuova ed espone molte estensioni della personalizzazione tramite proprietà ed eventi.  
  
 **Proprietà**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.SessionID%2A>, valore della stringa di sola lettura che rappresenta l'ID della sessione della connessione corrente.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.ClientCulture%2A>, riferimento di sola lettura alle impostazioni internazionali del client associate alla sessione corrente.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.User%2A>, riferimento di sola lettura all'interfaccia di identità che rappresenta l'utente corrente.  
  
 **Eventi**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>  
  
#### <a name="new-properties-in-the-context-class"></a>Nuove proprietà nella classe del contesto  
 La classe <xref:Microsoft.AnalysisServices.AdomdServer.Context> ha due nuove proprietà:  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.Server%2A>, riferimento di sola lettura al nuovo oggetto server.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentConnection%2A>, riferimento di sola lettura al nuovo oggetto <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection>.  
  
#### <a name="new-server-class"></a>Nuova classe server  
 La classe <xref:Microsoft.AnalysisServices.AdomdServer.Server> è nuova ed espone molte estensioni della personalizzazione tramite proprietà ed eventi della classe.  
  
 **Proprietà**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Name%2A>, valore della stringa di sola lettura che rappresenta il nome del server.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Culture%2A>, riferimento di sola lettura alla lingua globale associata al server.  
  
 **Eventi**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>  
  
#### <a name="adomdcommand-class"></a>Classe AdomdCommand  
 La classe <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> supporta ora i comandi MDX seguenti:  
  
-   [Istruzione CREATE MEMBER &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)  
  
-   [Istruzione UPDATE membro &#40;MDX&#41;](../../../mdx/mdx-data-definition-update-member.md)  
  
-   [Istruzione DROP membro &#40;MDX&#41;](../../../mdx/mdx-data-definition-drop-member.md)  
  
-   [Istruzione CREATE SET &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-set.md)  
  
-   [Istruzione DROP SET &#40;MDX&#41;](../../../mdx/mdx-data-definition-drop-set.md)  
  
-   [Istruzione CREATE KPI &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-kpi.md)  
  
-   [Istruzione DROP KPI &#40;MDX&#41;](../../../mdx/mdx-data-definition-drop-kpi.md)  
  
### <a name="mdx-extensions-and-enhancements"></a>Estensioni MDX e miglioramenti  
 Il comando CREATE MEMBER è stato migliorato con il **didascalia** proprietà, il **display_folder** proprietà e il **associated_measure_group** proprietà.  
  
 Il comando UPDATE MEMBER è stato aggiunto per evitare di ricreare il membro quando è necessario un aggiornamento, con la conseguente perdita di precedenza nella risoluzione dei calcoli. Gli aggiornamenti non è possibile modificare l'ambito del membro calcolato, spostare il membro calcolato a un padre diverso o definire un diverso **solveorder**.  
  
 Il comando CREATE SET è stato migliorato con il **didascalia** proprietà, il **display_folder** proprietà e il nuovo **statico | DINAMICA** (parola chiave). *Statico* significa che set viene valutato solo al momento della creazione. *Dinamica* significa che il set viene valutato ogni volta che viene usato il set in una query. Il valore predefinito è **statici** se una parola chiave viene omesso.  
  
 I comandi CREATE KPI e DROP KPI sono stati aggiunti alla sintassi MDX. Gli indicatori KPI possono essere creati dinamicamente da qualsiasi script MDX.  
  
### <a name="schema-rowsets-extensions"></a>Estensioni dei set di righe degli schemi  
 In MDSCHEMA_MEMBERS *ambito* viene aggiunta. I valori di ambito sono i seguenti: MDMEMBER_SCOPE_GLOBAL=1 = 1, MDMEMBER_SCOPE_SESSION=2 = 2.  
  
 In MDSCHEMA_SETS *set_evaluation_context* viene aggiunta. Impostare il contesto di valutazione valori sono i seguenti: MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2.  
  
 In MDSCHEMA_KPIS è stata aggiunta la colonna Scope. I valori di ambito sono i seguenti: MDKPI_SCOPE_GLOBAL=1, MDKPI_SCOPE_SESSION=2.  
  
  
