---
title: Trasformazioni di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transformations [Integration Services], listed
- transformations [Integration Services], types
- transformations [Integration Services]
- data flow [Integration Services], transformations
- business intelligence transformations [Integration Services]
- join transformations
- split transformations [Integration Services]
- custom transformations [Integration Services]
- row transformations [Integration Services]
- rowset transformations [Integration Services]
ms.assetid: c70c4f6e-82dd-4948-b923-fd5193f67f7e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 26b22a82491d3f4c586c3fb259bf50c6d7216367
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297907"
---
# <a name="integration-services-transformations"></a>Trasformazioni di Integration Services

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Le trasformazioni sono i componenti nel flusso di dati di un pacchetto che aggregano, uniscono, distribuiscono e modificano i dati. Le trasformazioni possono inoltre eseguire operazioni di ricerca e generare set di dati campione. In questa sezione vengono descritte le trasformazioni incluse in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , illustrandone il funzionamento.  
  
## <a name="business-intelligence-transformations"></a>Trasformazioni di Business Intelligence  
 Le trasformazioni seguenti eseguono operazioni di Business Intelligence quali la pulitura dei dati, il text mining e l'esecuzione di query di stima basate su un modello di data mining.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Dimensione a modifica lenta](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)|Trasformazione che configura l'aggiornamento di una dimensione a modifica lenta.|  
|[Trasformazione Raggruppamento fuzzy](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)|Trasformazione che standardizza i valori nei dati delle colonne.|  
|[Trasformazione Ricerca fuzzy](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)|Trasformazione che ricerca valori in una tabella di riferimento utilizzando una corrispondenza fuzzy.|  
|[Trasformazione Estrazione termini](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)|Trasformazione che estrae termini da un testo.|  
|[Trasformazione Ricerca termini](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)|Trasformazione che ricerca termini in una tabella di riferimento e conta i termini estratti dal testo.|  
|[Trasformazione Query di data mining](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|Trasformazione che esegue query di stima di data mining.|  
|[Trasformazione DQS Cleansing](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)|Trasformazione che corregge i dati di un'origine dati connessa applicando regole create per tale origine dati.|  
  
## <a name="row-transformations"></a>Trasformazioni a livello di riga  
 Le trasformazioni elencate di seguito consentono di aggiornare i valori delle colonne e di creare nuove colonne. La trasformazione viene applicata a tutte le righe dell'input.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Mappa caratteri](../../../integration-services/data-flow/transformations/character-map-transformation.md)|Trasformazione che applica funzioni per i valori stringa a dati di tipo carattere.|  
|[Trasformazione Copia colonna](../../../integration-services/data-flow/transformations/copy-column-transformation.md)|Trasformazione che aggiunge copie delle colonne di input al proprio output.|  
|[Trasformazione Conversione dati](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)|Trasformazione che converte il tipo di dati di una colonna in un tipo di dati diverso.|  
|[Trasformazione Colonna derivata](../../../integration-services/data-flow/transformations/derived-column-transformation.md)|Trasformazione che popola colonne con risultati di espressioni.|  
|[Trasformazione Esporta colonna](../../../integration-services/data-flow/transformations/export-column-transformation.md)|Trasformazione che inserisce in un file dati esportati da un flusso di dati.|  
|[Trasformazione Importa colonna](../../../integration-services/data-flow/transformations/import-column-transformation.md)|Trasformazione che legge dati da un file e li aggiunge a un flusso di dati.|  
|[Componente script](../../../integration-services/data-flow/transformations/script-component.md)|Trasformazione che utilizza script per estrarre, trasformare o caricare dati.|  
|[Trasformazione Comando OLE DB](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)|Trasformazione che esegue comandi SQL per ogni riga di un flusso di dati.|  
  
## <a name="rowset-transformations"></a>Trasformazioni a livello di set di righe  
 Le trasformazioni seguenti creano nuovi set di righe. Il set di righe può includere valori aggregati e ordinati, set di righe campione o set di righe trasformati tramite Pivot o UnPivot.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Aggregazione](../../../integration-services/data-flow/transformations/aggregate-transformation.md)|Trasformazione che esegue aggregazioni quali AVERAGE, SUM e COUNT.|  
|[Trasformazione Ordinamento](../../../integration-services/data-flow/transformations/sort-transformation.md)|Trasformazione che ordina i dati.|  
|[Trasformazione Campionamento percentuale](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)|Trasformazione che consente di creare un set di dati campione utilizzando una percentuale per specificare le dimensioni del campione.|  
|[Trasformazione Campionamento righe](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)|Trasformazione che consente di creare un set di dati campione specificando il numero di righe del campione.|  
|[Trasformazione pivot](../../../integration-services/data-flow/transformations/pivot-transformation.md)|Trasformazione che crea una versione meno normalizzata di una tabella normalizzata.|  
|[Trasformazione UnPivot](../../../integration-services/data-flow/transformations/unpivot-transformation.md)|Trasformazione che crea una versione più normalizzata di una tabella non normalizzata.|  
  
## <a name="split-and-join-transformations"></a>Trasformazioni di divisione e di unione  
 Le trasformazioni seguenti distribuiscono le righe tra output diversi, creano copie degli input della trasformazione, uniscono più input in un singolo output ed eseguono operazioni di ricerca.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Suddivisione condizionale](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)|Trasformazione che indirizza righe di dati verso output diversi.|  
|[Trasformazione Multicast](../../../integration-services/data-flow/transformations/multicast-transformation.md)|Trasformazione che distribuisce set di dati tra più output.|  
|[Trasformazione Unione input multipli](../../../integration-services/data-flow/transformations/union-all-transformation.md)|Trasformazione che unisce più set di dati.|  
|[Trasformazione Unione](../../../integration-services/data-flow/transformations/merge-transformation.md)|Trasformazione che unisce due set di dati ordinati.|  
|[Trasformazione Merge join](../../../integration-services/data-flow/transformations/merge-join-transformation.md)|Trasformazione che unisce due set di dati utilizzando un join di tipo FULL, LEFT o INNER.|  
|[Trasformazione Ricerca](../../../integration-services/data-flow/transformations/lookup-transformation.md)|Trasformazione che esegue la ricerca di valori in una tabella di riferimento utilizzando una corrispondenza esatta.|  
|[Trasformazione Cache](../../../integration-services/data-flow/transformations/cache-transform.md)|Trasformazione che scrive dati da un'origine dati connessa nel flusso di dati a una gestione connessione cache che salva i dati in un file di cache. La trasformazione Ricerca esegue ricerche sui dati nel file di cache.|  
|[Trasformazione del server di distribuzione di dati bilanciati](../../../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)|Tramite la trasformazione vengono distribuiti in modo uniforme i buffer di righe in entrata negli output di thread distinti per migliorare le prestazioni di pacchetti SSIS in esecuzione in server a più processori e più core.|  
  
## <a name="auditing-transformations"></a>Trasformazioni di controllo  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include le trasformazioni seguenti per l'aggiunta di informazioni di controllo e il conteggio delle righe.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Controllo](../../../integration-services/data-flow/transformations/audit-transformation.md)|Trasformazione che rende le informazioni sull'ambiente disponibili a un flusso di dati in un pacchetto.|  
|[Trasformazione Conteggio righe](../../../integration-services/data-flow/transformations/row-count-transformation.md)|Trasformazione che conta le righe al suo interno e archivia il totale in una variabile.|  
  
## <a name="custom-transformations"></a>Trasformazioni personalizzate  
 È inoltre possibile creare trasformazioni personalizzate. Per altre informazioni, vedere [Sviluppo di un componente di trasformazione personalizzato con output sincroni](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) e [Sviluppo di un componente di trasformazione personalizzato con output asincroni](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md).  
  
  
