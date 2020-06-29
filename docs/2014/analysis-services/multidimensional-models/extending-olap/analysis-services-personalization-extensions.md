---
title: Estensioni della personalizzazione di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0cd36cb2882659bff902d9830af0c5acefd98444
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468976"
---
# <a name="analysis-services-personalization-extensions"></a>Analysis Services Personalization Extensions
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]le estensioni della personalizzazione sono la base dell'idea di implementare un'architettura plug-in. In un'architettura plug-in è possibile sviluppare dinamicamente nuovi oggetti cubo e funzionalità e condividerli facilmente con gli altri sviluppatori. Di conseguenza, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] le estensioni della personalizzazione forniscono la funzionalità che consente di ottenere gli elementi seguenti:  
  
-   **Progettazione dinamica e distribuzione** Subito dopo la progettazione e [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] la distribuzione delle estensioni di personalizzazione, gli utenti possono accedere agli oggetti e alle funzionalità all'inizio della sessione utente successiva.  
  
-   **Indipendenza dall'interfaccia** Indipendentemente dall'interfaccia utilizzata per creare le [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] estensioni di personalizzazione, gli utenti possono utilizzare qualsiasi interfaccia per accedere agli oggetti e alle funzionalità.  
  
-   **Contesto sessione** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] le estensioni di personalizzazione non sono oggetti permanenti nell'infrastruttura esistente e non richiedono la rielaborazione del cubo. Vengono esposti e creati per l'utente al momento della connessione al database e rimangono disponibili per la durata della sessione dell'utente.  
  
-   **Distribuzione rapida** Condividi [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] le estensioni di personalizzazione con altri sviluppatori software senza dover passare a specifiche dettagliate su dove o come trovare questa funzionalità estesa.  
  
 Le estensioni della personalizzazione di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] possono essere utilizzate per diversi scopi. Ad esempio, la propria azienda dispone di vendite che hanno valute diverse. Viene creato un membro calcolato che restituisce le vendite consolidate nella valuta locale della persona che accede al cubo. Tale membro viene creato come estensione della personalizzazione. Il membro calcolato viene quindi condiviso con un gruppo di utenti. Una volta condiviso, gli utenti dispongono dell'accesso immediato al membro calcolato non appena si connettono al server, anche se non utilizzano la stessa interfaccia utilizzata durante la creazione del membro calcolato.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]le estensioni della personalizzazione rappresentano una semplice ed elegante modifica all'architettura dell'assembly gestito esistente e vengono esposte nel [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] modello a oggetti [Microsoft. AnalysisServices. AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120)) , nella sintassi MDX (Multidimensional Expressions) e nei set di righe dello schema.  
  
## <a name="logical-architecture"></a>Architettura logica  
 L'architettura delle estensioni della personalizzazione di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] è basata sull'architettura dell'assembly gestita e sui quattro elementi di base seguenti:  
  
 Attributo personalizzato [PlugInAttribute]  
 Quando si avvia il servizio, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carica gli assembly necessari e determina quali classi hanno l'attributo personalizzato [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120)) .  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] definisce gli attributi personalizzati come un modo per descrivere il codice e influisce sul comportamento in fase di esecuzione. Per ulteriori informazioni, vedere l'argomento "[Cenni preliminari sugli attributi](https://go.microsoft.com/fwlink/?LinkId=82929)" nella [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Guida per gli sviluppatori su MSDN.  
  
 Per tutte le classi con l'attributo personalizzato [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120)) , [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] richiama i costruttori predefiniti. La richiamata di tutti i costruttori all'avvio fornisce un percorso comune, indipendente dalle attività dell'utente, dal quale è possibile compilare nuovi oggetti.  
  
 Oltre a creare una piccola cache di informazioni sulla creazione e la gestione delle estensioni di personalizzazione, il costruttore della classe in genere sottoscrive gli eventi [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) e [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) . Se la sottoscrizione di tali eventi non riesce, la classe potrebbe essere erroneamente contrassegnata per la pulizia da parte del Garbage Collector del Common Language Runtime.  
  
 Contesto di sessione  
 Per gli oggetti basati sulle estensioni della personalizzazione, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea un ambiente di esecuzione durante la sessione client e compila dinamicamente la maggior parte degli oggetti dell'ambiente. Come qualsiasi altro assembly CLR, tale ambiente di esecuzione dispone anche dell'accesso ad altre funzioni e stored procedure. Al termine della sessione utente, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] rimuove gli oggetti creati dinamicamente e chiude l'ambiente di esecuzione.  
  
 Eventi  
 La creazione degli oggetti viene attivata dagli eventi di sessione `On-Cube-OpenedCubeOpened` e `On-Cube-ClosingCubeClosing`.  
  
 La comunicazione tra client e server si verifica attraverso eventi specifici. Tali eventi informano il client delle situazioni che portano alla compilazione degli oggetti del client. L'ambiente del client viene creato dinamicamente utilizzando due set di eventi: eventi di sessione ed eventi del cubo.  
  
 Gli eventi di sessione sono associati all'oggetto server. Quando un client accede a un server, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Crea una sessione e attiva l'evento [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) . Quando un client termina la sessione nel server, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] attiva l'evento [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) .  
  
 Gli eventi del cubo sono associati all'oggetto connessione. La connessione a un cubo attiva l'evento [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeOpened](/previous-versions/sql/sql-server-2014/bb630581(v=sql.120)) . La chiusura della connessione a un cubo, tramite la chiusura del cubo o la modifica di un cubo diverso, comporta l'attivazione di un evento [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeClosing](/previous-versions/sql/sql-server-2014/bb630371(v=sql.120)) .  
  
 Tracciabilità e gestione degli errori  
 Tutte le attività sono tracciabili utilizzando [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Gli errori non gestiti vengono segnalati al registro eventi di Windows.  
  
 La creazione e la gestione degli oggetti sono indipendenti dall'architettura e rappresentano l'unica responsabilità degli sviluppatori degli oggetti.  
  
## <a name="infrastructure-foundations"></a>Base dell'infrastruttura  
 Le estensioni della personalizzazione di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sono basate su componenti esistenti. Di seguito è riportato un riepilogo dei miglioramenti forniti dalla funzionalità delle estensioni della personalizzazione.  
  
### <a name="assemblies"></a>Assembly  
 È possibile aggiungere l'attributo personalizzato [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120))agli assembly personalizzati per identificare [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] le classi delle estensioni di personalizzazione.  
  
### <a name="changes-to-the-adomdserver-object-model"></a>Modifiche al modello a oggetti AdomdServer  
 Gli oggetti seguenti nel modello a oggetti [Microsoft. AnalysisServices. AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120)) sono stati migliorati o aggiunti al modello.  
  
#### <a name="new-adomdconnection-class"></a>Nuova classe AdomdConnection  
 La classe [Microsoft. AnalysisServices. AdomdServer. AdomdConnection](/previous-versions/sql/sql-server-2014/bb678193(v=sql.120)) è nuova ed espone diverse estensioni della personalizzazione tramite proprietà ed eventi.  
  
 **Proprietà**  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. SessionID *](/previous-versions/sql/sql-server-2014/bb678099(v=sql.120)), un valore stringa di sola lettura che rappresenta l'ID di sessione della connessione corrente.  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. ClientCulture *](/previous-versions/sql/sql-server-2014/bb677433(v=sql.120)), un riferimento di sola lettura alle impostazioni cultura client associate alla sessione corrente.  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. User *](/previous-versions/sql/sql-server-2014/bb630315(v=sql.120)), un riferimento di sola lettura all'interfaccia di identità che rappresenta l'utente corrente.  
  
 **Events**  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeOpened](/previous-versions/sql/sql-server-2014/bb630581(v=sql.120))  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeClosing](/previous-versions/sql/sql-server-2014/bb630371(v=sql.120))  
  
#### <a name="new-properties-in-the-context-class"></a>Nuove proprietà nella classe del contesto  
 La classe [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) presenta due nuove proprietà:  
  
-   [Microsoft. AnalysisServices. AdomdServer. Context. Server *](/previous-versions/sql/sql-server-2014/bb678098(v=sql.120)), un riferimento di sola lettura al nuovo oggetto server.  
  
-   [Microsoft. AnalysisServices. AdomdServer. Context. CurrentConnection *](/previous-versions/sql/sql-server-2014/bb630975(v=sql.120)), un riferimento di sola lettura al nuovo oggetto [Microsoft. AnalysisServices. AdomdServer. AdomdConnection](/previous-versions/sql/sql-server-2014/bb678193(v=sql.120)) .  
  
#### <a name="new-server-class"></a>Nuova classe server  
 La classe [Microsoft. AnalysisServices. AdomdServer. Server](/previous-versions/sql/sql-server-2014/bb677955(v=sql.120)) è nuova ed espone diverse estensioni di personalizzazione tramite gli eventi e le proprietà della classe.  
  
 **Proprietà**  
  
-   [Microsoft.AnalysisServices.AdomdServer.Server.Name *](/previous-versions/sql/sql-server-2014/bb677694(v=sql.120)), valore stringa di sola lettura che rappresenta il nome del server.  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. culture *](/previous-versions/sql/sql-server-2014/bb677437(v=sql.120)), un riferimento di sola lettura alle impostazioni cultura globali associate al server.  
  
 **Events**  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))  
  
#### <a name="adomdcommand-class"></a>Classe AdomdCommand  
 La classe [Microsoft. AnalysisServices. AdomdServer. AdomdCommand](/previous-versions/sql/sql-server-2014/ms143286(v=sql.120)) supporta ora i comandi MDX seguenti:  
  
-   [Istruzione CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)  
  
-   [Istruzione UPDATE MEMBER &#40;&#41;MDX](/sql/mdx/mdx-data-definition-update-member)  
  
-   [Istruzione DROP MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-member)  
  
-   [Istruzione CREATE SET &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)  
  
-   [Istruzione DROP SET &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-set)  
  
-   [Istruzione CREATE KPI &#40;&#41;MDX](/sql/mdx/mdx-data-definition-create-kpi)  
  
-   [Istruzione DROP KPI &#40;&#41;MDX](/sql/mdx/mdx-data-definition-drop-kpi)  
  
### <a name="mdx-extensions-and-enhancements"></a>Estensioni MDX e miglioramenti  
 Il comando CREATE MEMBER è stato migliorato con le proprietà `caption`, `display_folder` e `associated_measure_group`.  
  
 Il comando UPDATE MEMBER è stato aggiunto per evitare di ricreare il membro quando è necessario un aggiornamento, con la conseguente perdita di precedenza nella risoluzione dei calcoli. Gli aggiornamenti non sono in grado di modificare l'ambito del membro calcolato, di spostare il membro calcolato in un elemento padre diverso o di definire un diverso `solveorder`.  
  
 Il comando CREATE SET è stato migliorato con le proprietà `caption` e `display_folder` e con la nuova parola chiave `STATIC | DYNAMIC`. *Static* significa che il set viene valutato solo al momento della creazione. *Dynamic* significa che il set viene valutato ogni volta che il set viene utilizzato in una query. Se la parola chiave viene omessa, il valore predefinito è `STATIC`.  
  
 I comandi CREATE KPI e DROP KPI sono stati aggiunti alla sintassi MDX. Gli indicatori KPI possono essere creati dinamicamente da qualsiasi script MDX.  
  
### <a name="schema-rowsets-extensions"></a>Estensioni dei set di righe degli schemi  
 In MDSCHEMA_MEMBERS colonna *ambito* viene aggiunto. I valori di ambito sono i seguenti: MDMEMBER_SCOPE_GLOBAL=1, MDMEMBER_SCOPE_SESSION=2.  
  
 MDSCHEMA_SETS viene aggiunta la colonna *set_evaluation_context* . I valori di contesto di valutazione dei set sono i seguenti: MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2.  
  
 In MDSCHEMA_KPIS è stata aggiunta la colonna Scope. I valori di ambito sono i seguenti: MDKPI_SCOPE_GLOBAL=1, MDKPI_SCOPE_SESSION=2.  
  
  
