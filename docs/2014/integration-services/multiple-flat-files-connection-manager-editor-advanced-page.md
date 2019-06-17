---
title: Per più file Flat dell'Editor gestione connessione (pagina avanzate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.advanced.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: fc883131-c03d-4ab3-8220-b51cbe243a82
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: de238c1012a255ceb59086e542d5529b8b907915
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057553"
---
# <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>Editor gestione connessione per più file flat (pagina Avanzate)
  Usare la pagina **Avanzate** della finestra di dialogo **Editor gestione connessione per più file flat** per impostare proprietà come il tipo di dati e i delimitatori di ogni colonna nei file di testo a cui si connette la gestione connessione per i file flat.  
  
 Per impostazione predefinita, la lunghezza delle colonne di stringhe è di 50 caratteri. È possibile valutare i dati di esempio e ridimensionare automaticamente la lunghezza di queste colonne per evitare che i dati siano troncati o che la colonna sia eccessivamente larga. È possibile aggiornare anche altri metadati per attivare la compatibilità con le colonne di destinazione. È possibile ad esempio modificare il tipo di dati di una colonna che contiene solo dati integer impostando un tipo di dati numeric, come DT_I2.  
  
 Per ulteriori informazioni sulla gestione connessione per più file flat, vedere [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la gestione connessione per più file flat nel flusso di lavoro. Il nome specificato verrà visualizzato nell'area **Gestioni connessioni** in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la gestione connessione. È consigliabile includere nella descrizione informazioni sugli scopi della gestione connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Configurare le proprietà delle singole colonne**  
 È possibile selezionare una colonna nel riquadro sinistro per visualizzarne le proprietà in quello destro. Nella tabella seguente è disponibile una descrizione delle proprietà dei tipi di dati. Alcune delle proprietà incluse nell'elenco possono essere configurate solo per alcuni formati di file flat.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**ColumnType**|Indica se la colonna è delimitata, a larghezza fissa o non allineata a destra. Questa proprietà è di sola lettura. I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa ad eccezione dell'ultima, per la quale viene utilizzato il delimitatore di riga.|  
|**OutputColumnWidth**|Consente di specificare il valore da archiviare come conteggio di byte. Nel caso dei file Unicode tale valore verrà visualizzato come conteggio di caratteri. Nell'attività Flusso di dati questo valore viene utilizzato per impostare la larghezza della colonna di output per l'origine file flat.<br /><br /> Nota: Nel modello a oggetti il nome di questa proprietà è MaximumWidth.|  
|**DataType**|Consente di selezionare i tipi di dati disponibili nell'apposito elenco. Per altre informazioni, vedere [Tipi di dati di Integration Services](data-flow/integration-services-data-types.md).|  
|**TextQualified**|Consente di specificare se i dati di testo sono qualificati mediante un carattere qualificatore di testo. I valori validi sono:<br /><br /> **True**: i dati di tipo testo nel file flat sono qualificati.<br /><br /> **False**: i dati di tipo testo nel file flat non sono qualificati.|  
|**Name**|Consente di specificare un nome per la colonna. Per impostazione predefinita, si tratta di un elenco numerato di colonne. È comunque possibile scegliere qualsiasi nome descrittivo univoco.|  
|**DataScale**|Consente di specificare la scala dei dati numerici. Per scala si intende il numero di posizioni decimali. Per altre informazioni, vedere [Tipi di dati di Integration Services](data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Consente di selezionare i delimitatori di colonna disponibili nell'apposito elenco. Scegliere come delimitatori caratteri che non siano già presenti nel testo. Questo valore viene ignorato per le colonne a larghezza fissa.<br /><br /> **{CR}{LF}** : le colonne sono delimitate dalla combinazione di caratteri ritorno a capo/avanzamento riga<br /><br /> **{CR}** : le colonne sono delimitate da un ritorno a capo<br /><br /> **{LF}** : le colonne sono delimitate da un avanzamento riga<br /><br /> **Punto e virgola {;}** : le colonne sono delimitate da un punto e virgola<br /><br /> **Due punti {:}** : le colonne sono delimitate da due punti<br /><br /> **Virgola {,}{,}** : le colonne sono delimitate da una virgola<br /><br /> **Tabulazione {t}** : le colonne sono delimitate da una tabulazione<br /><br /> **Barra verticale {&#124;}** : le colonne sono delimitate da una barra verticale|  
|**DataPrecision**|Consente di specificare la precisione dei dati numerici. Per precisione si intende il numero di cifre. Per altre informazioni, vedere [Tipi di dati di Integration Services](data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Consente di specificare il valore da archiviare come conteggio di byte. Nel caso dei file Unicode tale valore verrà visualizzato come conteggio di caratteri. Questo valore viene ignorato nelle colonne delimitate.<br /><br /> **Nota** : nel modello a oggetti il nome di questa proprietà è ColumnWidth.|  
  
 **Nuova**  
 Consente di aggiungere una **nuova**colonna. Per impostazione predefinita, il pulsante **Nuova** aggiunge una colonna alla fine dell'elenco. Il pulsante offre inoltre le opzioni seguenti che è possibile selezionare dall'elenco a discesa.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Aggiungi colonna**|Consente di aggiungere una nuova colonna alla fine dell'elenco.|  
|**Inserisci prima**|Consente di inserire una nuova colonna prima di quella selezionata.|  
|**Inserisci dopo**|Consente di inserire una nuova colonna dopo quella selezionata.|  
  
 **Elimina**  
 Consente di selezionare una colonna e quindi di **rimuoverla**.  
  
 **Suggerisci tipi**  
 Usare la finestra di dialogo **Suggerisci tipi di colonne** per restituire dati di esempio nel primo file selezionato e ottenere suggerimenti relativi al tipo di dati e alla lunghezza di ogni colonna. Per altre informazioni, vedere [Riferimento all'interfaccia utente della finestra di dialogo Suggerisci tipi di colonne](connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor gestione connessione per più file flat &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor gestione connessione per più file flat &#40;pagina Colonne&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [Editor gestione connessione per più file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
