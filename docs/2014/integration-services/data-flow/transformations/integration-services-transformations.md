---
title: Trasformazioni di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e90e459e5243d623ae0744ed2d7298cfd27eee5e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939472"
---
# <a name="integration-services-transformations"></a>Trasformazioni di Integration Services
  Le trasformazioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sono i componenti nel flusso di dati di un pacchetto che aggregano, uniscono, distribuiscono e modificano i dati. Le trasformazioni possono inoltre eseguire operazioni di ricerca e generare set di dati campione. In questa sezione vengono descritte le trasformazioni incluse in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , illustrandone il funzionamento.  
  
## <a name="business-intelligence-transformations"></a>Trasformazioni di Business Intelligence  
 Le trasformazioni seguenti eseguono operazioni di Business Intelligence quali la pulitura dei dati, il text mining e l'esecuzione di query di stima basate su un modello di data mining.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Dimensione a modifica lenta](slowly-changing-dimension-transformation.md)|Trasformazione che configura l'aggiornamento di una dimensione a modifica lenta.|  
|[Trasformazione Raggruppamento fuzzy](fuzzy-grouping-transformation.md)|Trasformazione che standardizza i valori nei dati delle colonne.|  
|[Trasformazione Ricerca fuzzy](lookup-transformation.md)|Trasformazione che ricerca valori in una tabella di riferimento utilizzando una corrispondenza fuzzy.|  
|[Trasformazione Estrazione termini](term-extraction-transformation.md)|Trasformazione che estrae termini da un testo.|  
|[Trasformazione Ricerca termini](term-lookup-transformation.md)|Trasformazione che ricerca termini in una tabella di riferimento e conta i termini estratti dal testo.|  
|[Trasformazione Query di data mining](data-mining-query-transformation.md)|Trasformazione che esegue query di stima di data mining.|  
|[Trasformazione DQS Cleansing](dqs-cleansing-transformation.md)|Trasformazione che corregge i dati di un'origine dati connessa applicando regole create per tale origine dati.|  
  
## <a name="row-transformations"></a>Trasformazioni a livello di riga  
 Le trasformazioni elencate di seguito consentono di aggiornare i valori delle colonne e di creare nuove colonne. La trasformazione viene applicata a tutte le righe dell'input.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Mappa caratteri](character-map-transformation.md)|Trasformazione che applica funzioni per i valori stringa a dati di tipo carattere.|  
|[Trasformazione Copia colonna](copy-column-transformation.md)|Trasformazione che aggiunge copie delle colonne di input al proprio output.|  
|[Trasformazione Conversione dati](data-conversion-transformation.md)|Trasformazione che converte il tipo di dati di una colonna in un tipo di dati diverso.|  
|[Trasformazione Colonna derivata](derived-column-transformation.md)|Trasformazione che popola colonne con risultati di espressioni.|  
|[Trasformazione Esporta colonna](export-column-transformation.md)|Trasformazione che inserisce in un file dati esportati da un flusso di dati.|  
|[Trasformazione Importa colonna](import-column-transformation.md)|Trasformazione che legge dati da un file e li aggiunge a un flusso di dati.|  
|[Componente script](script-component.md)|Trasformazione che utilizza script per estrarre, trasformare o caricare dati.|  
|[Trasformazione Comando OLE DB](ole-db-command-transformation.md)|Trasformazione che esegue comandi SQL per ogni riga di un flusso di dati.|  
  
## <a name="rowset-transformations"></a>Trasformazioni a livello di set di righe  
 Le trasformazioni seguenti creano nuovi set di righe. Il set di righe può includere valori aggregati e ordinati, set di righe campione o set di righe trasformati tramite Pivot o UnPivot.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Aggregazione](aggregate-transformation.md)|Trasformazione che esegue aggregazioni quali AVERAGE, SUM e COUNT.|  
|[Trasformazione Ordinamento](sort-transformation.md)|Trasformazione che ordina i dati.|  
|[Trasformazione Campionamento percentuale](percentage-sampling-transformation.md)|Trasformazione che consente di creare un set di dati campione utilizzando una percentuale per specificare le dimensioni del campione.|  
|[Trasformazione Campionamento righe](row-sampling-transformation.md)|Trasformazione che consente di creare un set di dati campione specificando il numero di righe del campione.|  
|[Trasformazione pivot](pivot-transformation.md)|Trasformazione che crea una versione meno normalizzata di una tabella normalizzata.|  
|[Trasformazione UnPivot](unpivot-transformation.md)|Trasformazione che crea una versione più normalizzata di una tabella non normalizzata.|  
  
## <a name="split-and-join-transformations"></a>Trasformazioni di divisione e di unione  
 Le trasformazioni seguenti distribuiscono le righe tra output diversi, creano copie degli input della trasformazione, uniscono più input in un singolo output ed eseguono operazioni di ricerca.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Suddivisione condizionale](conditional-split-transformation.md)|Trasformazione che indirizza righe di dati verso output diversi.|  
|[Trasformazione Multicast](multicast-transformation.md)|Trasformazione che distribuisce set di dati tra più output.|  
|[Trasformazione Unione input multipli](union-all-transformation.md)|Trasformazione che unisce più set di dati.|  
|[Trasformazione Unione](merge-transformation.md)|Trasformazione che unisce due set di dati ordinati.|  
|[Trasformazione Merge join](merge-join-transformation.md)|Trasformazione che unisce due set di dati utilizzando un join di tipo FULL, LEFT o INNER.|  
|[Trasformazione Ricerca](lookup-transformation.md)|Trasformazione che esegue la ricerca di valori in una tabella di riferimento utilizzando una corrispondenza esatta.|  
|[Trasformazione Cache](cache-transform.md)|Trasformazione che scrive dati da un'origine dati connessa nel flusso di dati a una gestione connessione cache che salva i dati in un file di cache. La trasformazione Ricerca esegue ricerche sui dati nel file di cache.|  
|[Trasformazione Distribuzione di dati bilanciati](balanced-data-distributor-transformation.md)|Tramite la trasformazione vengono distribuiti in modo uniforme i buffer di righe in entrata negli output di thread distinti per migliorare le prestazioni di pacchetti SSIS in esecuzione in server a più processori e più core.|  
  
## <a name="auditing-transformations"></a>Trasformazioni di controllo  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include le trasformazioni seguenti per l'aggiunta di informazioni di controllo e il conteggio delle righe.  
  
|Trasformazione|Descrizione|  
|--------------------|-----------------|  
|[Trasformazione Controllo](audit-transformation.md)|Trasformazione che rende le informazioni sull'ambiente disponibili a un flusso di dati in un pacchetto.|  
|[Trasformazione Conteggio righe](row-count-transformation.md)|Trasformazione che conta le righe al suo interno e archivia il totale in una variabile.|  
  
## <a name="custom-transformations"></a>Trasformazioni personalizzate  
 È inoltre possibile creare trasformazioni personalizzate. Per altre informazioni, vedere [Sviluppo di un componente di trasformazione personalizzato con output sincroni](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) e [Sviluppo di un componente di trasformazione personalizzato con output asincroni](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md).  
  
  
