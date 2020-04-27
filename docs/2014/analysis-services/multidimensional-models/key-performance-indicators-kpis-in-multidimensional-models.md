---
title: Indicatori di prestazioni chiave (KPI) nei modelli multidimensionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- viewing Key Performance Indicators
- Key Performance Indicators [Analysis Services]
- KPIs [Analysis Services]
- OLAP objects [Analysis Services], performance indicators
- weights [Analysis Services]
- displaying Key Performance Indicators
- parent KPIs [Analysis Services]
- child KPIs
ms.assetid: 73aee2da-da30-44f1-829c-0a4c078a7768
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35482dc6206f0ad8807cb0f9a3e46902d14061ab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074801"
---
# <a name="key-performance-indicators-kpis-in-multidimensional-models"></a>Indicatori KPI nei modelli multidimensionali
  Nella terminologia aziendale, un indicatore di prestazioni chiave (KPI) rappresenta una misurazione quantificabile per la valutazione dei risultati aziendali e  
  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]un indicatore KPI è costituito da una raccolta di calcoli associati a un gruppo di misure in un cubo e usati per valutare il successo aziendale. Questi calcoli sono in genere una combinazione di espressioni MDX (Multidimensional Expressions) o di membri calcolati. Gli indicatori KPI dispongono inoltre di metadati aggiuntivi che offrono informazioni sulla modalità di visualizzazione dei risultati dei calcoli degli indicatori stessi nelle applicazioni client.  
  
 Un indicatore KPI gestisce le informazioni su un set di obiettivi, la formula effettiva delle prestazioni registrate nel cubo e la misurazione per la visualizzazione della tendenza e dello stato delle prestazioni. Gli oggetti AMO sono utilizzati per specificare le formule e altre definizioni relative ai valori di un indicatore di prestazioni chiave. Un QI (Query Interface), ad esempio ADOMD.NET, viene utilizzato dall'applicazione client per recuperare i valori KPI ed esporli all'utente finale. Per altre informazioni vedere [Sviluppo con ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net).  
  
 Un oggetto <xref:Microsoft.AnalysisServices.Kpi> semplice è composto da informazioni di base, dall'obiettivo, dal valore effettivo raggiunto, da un valore di stato, da un valore di tendenza e da una cartella in cui viene visualizzato l'indicatore KPI. Le informazioni di base includono il nome e descrizione dell'indicatore KPI. L'obiettivo è un'espressione MDX che restituisce un numero. Il valore effettivo è un'espressione MDX che restituisce un numero. I valori di stato e di tendenza sono espressioni MDX che restituiscono un numero. La cartella è un percorso consigliato per l'indicatore KPI da presentare al client.  
  
 Nella terminologia aziendale, un indicatore di prestazioni chiave (KPI) rappresenta una misurazione quantificabile per la valutazione dei risultati aziendali e viene stimato con una frequenza spesso elevata. Il reparto vendite di un'organizzazione potrebbe ad esempio utilizzare il profitto lordo mensile come indicatore di prestazioni chiave, mentre il reparto risorse umane della stessa organizzazione potrebbe basarsi sull'avvicendamento trimestrale dei dipendenti. Ognuno di questi rappresenta un esempio di utilizzo di un indicatore KPI. I dirigenti aziendali utilizzano spesso indicatori di prestazioni chiave raggruppati in una scorecard aziendale per ottenere un riepilogo cronologico immediato e accurato del successo aziendale.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], un indicatore KPI è una raccolta di calcoli, associati a un gruppo di misure in un cubo, utilizzati per valutare il successo aziendale. Questi calcoli sono in genere una combinazione di espressioni MDX (Multidimensional Expressions) e di membri calcolati. Gli indicatori di prestazioni chiave dispongono inoltre di metadati aggiuntivi che offrono informazioni su come devono venire visualizzati i risultati dei calcoli dell'indicatore nelle applicazioni client.  
  
 Un vantaggio fondamentale degli indicatori KPI in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consiste nel fatto che si tratta di indicatori basati sul server che possono essere utilizzati da diverse applicazioni client. Un indicatore di prestazioni chiave basato sul server presenta un'unica versione di verità, rispetto alle diverse versioni di verità di più applicazioni client. Si possono inoltre ottenere vantaggi in termini di prestazioni grazie alla possibilità di eseguire calcoli talvolta complessi nel server anziché in ogni computer client.  
  
## <a name="common-kpi-terms"></a>Terminologia comune relativa agli indicatori di prestazioni chiave  
 Nella tabella seguente vengono definiti i termini comuni relativi agli indicatori di prestazioni chiave in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Termine|Definizione|  
|----------|----------------|  
|Obiettivo|Calcolo o espressione numerica MDX che restituisce il valore di destinazione dell'indicatore di prestazioni chiave.|  
|valore|Espressione numerica MDX che restituisce il valore effettivo dell'indicatore di prestazioni chiave.|  
|Stato|Espressione MDX che rappresenta lo stato dell'indicatore di prestazioni chiave in un punto nel tempo specifico.<br /><br /> L'espressione MDX relativa allo stato deve restituire un valore normalizzato compreso tra -1 e 1. I valori minori o uguali a -1 vengono interpretati come "errati" o "bassi". Un valore pari a zero (0) viene interpretato come "accettabile" o "medio". I valori maggiori di o uguali a 1 vengono interpretati come "buoni" o "alti".<br /><br /> Facoltativamente, può venire restituito un numero illimitato di valori intermedi e questi valori possono essere utilizzati per visualizzare un numero qualsiasi di stati aggiuntivi, se l'applicazione client lo consente.|  
|Tendenza|Espressione MDX che valuta il valore dell'indicatore di prestazioni chiave nel tempo. La tendenza può essere rappresentata da qualsiasi criterio basato sul tempo che sia utile in un contesto aziendale specifico.<br /><br /> L'espressione MDX relativa alla tendenza consente a un utente aziendale di determinare se l'indicatore di prestazioni chiave sta migliorando o peggiorando nel tempo.|  
|Indicatore di stato|Elemento visivo che offre un'indicazione immediata dello stato dell'indicatore di prestazioni chiave. Il tipo di visualizzazione dell'elemento è determinato dal valore dell'espressione MDX che valuta lo stato.|  
|Indicatore di tendenza|Elemento visivo che offre un'indicazione immediata della tendenza dell'indicatore di prestazioni chiave. Il tipo di visualizzazione dell'elemento è determinato dal valore dell'espressione MDX che valuta la tendenza.|  
|Cartella di visualizzazione|Cartella in cui l'indicatore di prestazioni chiave viene visualizzato quando un utente esplora il cubo.|  
|KPI padre|Riferimento a un indicatore di prestazioni chiave esistente che utilizza il valore dell'indicatore di prestazioni chiave figlio per i calcoli eseguiti. Talvolta un singolo indicatore di prestazioni chiave è costituito da un calcolo eseguito con i valori di altri indicatori di prestazioni chiave. Questa proprietà semplifica la visualizzazione corretta degli indicatori di prestazioni chiave figlio sotto l'indicatore di prestazioni chiave padre nelle applicazioni client.|  
|Membro temporale corrente|Espressione MDX che restituisce il membro che identifica il contesto temporale dell'indicatore di prestazioni chiave.|  
|Peso|Espressione numerica MDX che assegna un'importanza relativa a un indicatore di prestazioni chiave. Se l'indicatore di prestazioni chiave è assegnato a un KPI padre, il peso viene utilizzato per modificare in modo proporzionale i risultati del valore dell'indicatore di prestazioni chiave figlio quando si calcola il valore del KPI padre.|  
  
## <a name="parent-kpis"></a>Indicatori di prestazioni chiave padre  
 In un'organizzazione potrebbe essere necessario tenere traccia di metriche aziendali diverse a più livelli. Potrebbero ad esempio venire utilizzati solo due o tre indicatori di prestazioni chiave per valutare il successo aziendale, ma questi indicatori validi per l'intera azienda potrebbero essere basati su altri tre o quattro indicatori di prestazioni chiave calcolati dalle business unit nella società. Le business unit di una società potrebbero inoltre utilizzare dati statistici diversi per calcolare lo stesso indicatore di prestazioni chiave, dei cui risultati è possibile eseguire il rollup nell'indicatore di prestazioni chiave valido per l'intera azienda.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile definire una relazione padre-figlio tra indicatori di prestazioni chiave. Questa relazione padre-figlio consente di utilizzare i risultati dell'indicatore di prestazioni chiave figlio per calcolare i risultati dell'indicatore di prestazioni chiave padre. Questa relazione può inoltre essere utilizzata dalle applicazioni client per visualizzare in modo corretto gli indicatori di prestazioni chiave padre e figlio.  
  
## <a name="weights"></a>Pesi  
 È possibile assegnare pesi anche agli indicatori di prestazioni chiave figlio. I pesi consentono ad [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di modificare in modo proporzionale i risultati dell'indicatore di prestazioni chiave figlio quando si calcola il valore dell'indicatore di prestazioni chiave padre.  
  
## <a name="retrieving-and-displaying-kpis"></a>Recupero e visualizzazione di indicatori di prestazioni chiave  
 La visualizzazione degli indicatori di prestazioni chiave dipende dall'implementazione dell'applicazione client. Se, ad esempio, si fa clic su **Visualizzazione Esplorazione** sulla barra degli strumenti nella scheda **KPI** di Progettazione cubi, viene visualizzata una possibile implementazione client, con elementi grafici usati per visualizzare gli indicatori di stato e di tendenza, cartelle di visualizzazione utilizzate per raggruppare gli indicatori di prestazioni chiave e indicatori di prestazioni chiave figlio visualizzati sotto gli indicatori di prestazioni chiave padre.  
  
 È possibile utilizzare le funzioni MDX per recuperare singole sezioni dell'indicatore di prestazioni chiave, ad esempio il valore o l'obiettivo, da utilizzare in script, istruzioni ed espressioni MDX.  
  
  
