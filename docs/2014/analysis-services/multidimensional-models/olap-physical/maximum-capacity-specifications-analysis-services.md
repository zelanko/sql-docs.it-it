---
title: Specifiche di capacità massima (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
author: minewiskan
ms.author: owend
ms.openlocfilehash: d0495ed563585a5b7427655428a257174673fc02
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545918"
---
# <a name="maximum-capacity-specifications-analysis-services"></a>Specifiche di capacità massima (Analysis Services)
  Nelle tabelle seguenti vengono indicate le dimensioni e le quantità massime dei diversi oggetti definiti nei componenti di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] con diverse modalità di distribuzione del server.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Multidimensionale e Data Mining (DeploymentMode=0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode=1)](#bkmk_sharepoint)  
  
 [Tabulare (DeploymentMode=2)](#bkmk_vertipaq)  
  
##  <a name="multidimensional-and-data-mining-deploymentmode0"></a><a name="bkmk_OLAP"></a>Multidimensionale e data mining (DeploymentMode = 0)  
 La modalità di archiviazione MOLAP, che prevede l'archiviazione sia di dati che di metadati, prevede limiti fisici aggiuntivi relativi alle dimensioni dei file. Per impostazione predefinita, la dimensione massima dei file di archivio delle stringhe è di 4 GB. Se sono necessari file più grandi per gli archivi di stringhe, è possibile specificare un'architettura di archiviazione di stringhe diversa. Per altre informazioni, vedere [configurare l'archiviazione di stringhe per dimensioni e partizioni](../configure-string-storage-for-dimensions-and-partitions.md).  
  
|Oggetto|Quantità/dimensioni massime|  
|------------|----------------------------|  
|Database in un'istanza|2^31-1 = 2.147.483.647|  
|Dimensioni in un database|2^31-1 = 2.147.483.647|  
|Attributi in una dimensione|2^31-1 = 2.147.483.647|  
|Membri in un attributo di dimensione|2^31-1 = 2.147.483.647|  
|Gerarchie definite dall'utente in una dimensione|2^31-1 = 2.147.483.647|  
|Livelli in una gerarchia definita dall'utente|2^31-1 = 2.147.483.647|  
|Cubi in un database|2^31-1 = 2.147.483.647|  
|Gruppi di misure in un cubo|2^31-1 = 2.147.483.647|  
|Misure in un gruppo di misure|2^31-1 = 2.147.483.647|  
|Calcoli in un cubo|2^31-1 = 2.147.483.647|  
|Indicatori di prestazioni chiave in un cubo|2^31-1 = 2.147.483.647|  
|Azioni in un cubo|2^31-1 = 2.147.483.647|  
|Partizioni in un cubo|2^31-1 = 2.147.483.647|  
|Traduzioni in un cubo|2^31-1 = 2.147.483.647|  
|Aggregazioni in una partizione|2^31-1 = 2.147.483.647|  
|Celle restituite da una query|2^31-1 = 2.147.483.647|  
|Dimensioni dei record della query di origine|64 KB|  
|Lunghezza dei nomi degli oggetti|100 caratteri|  
|Numero massimo di stati distinti in una colonna attributo del modello di data mining|2^31-1 = 2.147.483.647|  
|Numero massimo di attributi considerati (caratteristica di selezione degli attributi)|2^31-1 = 2.147.483.647|  
  
 Per ulteriori informazioni sulle linee guida per la denominazione degli oggetti, vedere [oggetti ASSL e caratteristiche degli](../scripting-language-assl/assl-objects-and-object-characteristics.md)oggetti.  
  
 Per ulteriori informazioni sulle limitazioni delle origini dati per Online Analytical Processing (OLAP) e data mining, vedere [origini dati supportate &#40;&#41;multidimensionali di SSAS ](../supported-data-sources-ssas-multidimensional.md), [origini dati supportate &#40;ssas multidimensionale&#41;](../supported-data-sources-ssas-multidimensional.md)e [oggetti ASSL e caratteristiche degli](../scripting-language-assl/assl-objects-and-object-characteristics.md)oggetti.  
  
##  <a name="sharepoint-deploymentmode1"></a><a name="bkmk_sharepoint"></a>SharePoint (DeploymentMode = 1)  
  
|Oggetto|Quantità/dimensioni massime|  
|------------|----------------------------|  
|Database in un'istanza|2^31-1 = 2.147.483.647|  
|Tabelle in un database|2^31-1 = 2.147.483.647|  
|Colonne in una tabella|2 ^ 31-1 = 2.147.483.647 **Avviso:** il numero totale di colonne in una tabella dipende dal numero totale di misure e colonne calcolate associate alla stessa tabella. Il numero massimo di "colonne + misure + colonne calcolate" per una tabella è di 2^31-1 = 2.147.483.647|  
|Righe in una tabella|**Avviso illimitato:** con la restrizione che nessuna colonna singola può contenere più di 1.999.999.997 valori distinti.|  
|Gerarchie in una tabella|2^31-1 = 2.147.483.647|  
|Livelli in una gerarchia|2^31-1 = 2.147.483.647|  
|Relazioni|2^31-1 = 2.147.483.647|  
|Colonne chiave in una tabella|2^31-1 = 2.147.483.647|  
|Misure in una tabella|2 ^ 31-1 = 2.147.483.647 **Avviso:** il numero totale di misure in una tabella dipende dal numero totale di colonne e colonne calcolate associate alla stessa tabella. Il numero massimo di "colonne + misure + colonne calcolate" per una tabella è di 2^31-1 = 2.147.483.647|  
|Colonne calcolate in una tabella|2 ^ 31-1 = 2.147.483.647 **Avviso:** il numero totale di colonne calcolate in una tabella dipende dal numero totale di colonne e misure associate alla stessa tabella. Il numero massimo di "colonne + misure + colonne calcolate" per una tabella è di 2^31-1 = 2.147.483.647|  
|Celle restituite da una query|2^31-1 = 2.147.483.647|  
|Dimensioni dei record della query di origine|64 KB|  
|Lunghezza dei nomi degli oggetti|100 caratteri|  
  
##  <a name="tabular-deploymentmode2"></a><a name="bkmk_vertipaq"></a>Tabulare (DeploymentMode = 2)  
  
|Oggetto|Quantità/dimensioni massime|  
|------------|----------------------------|  
|Database in un'istanza|2^31-1 = 2.147.483.647|  
|Tabelle in un database|2^31-1 = 2.147.483.647|  
|Colonne in una tabella|2 ^ 31-1 = 2.147.483.647 **Avviso:** il numero totale di colonne in una tabella dipende dal numero totale di misure e colonne calcolate associate alla stessa tabella. Il numero massimo di "colonne + misure + colonne calcolate" per una tabella è di 2^31-1 = 2.147.483.647|  
|Righe in una tabella|**Avviso illimitato:** con la restrizione che nessuna colonna singola nella tabella può contenere più di 1.999.999.997 valori distinti.|  
|Gerarchie in una tabella|2^31-1 = 2.147.483.647|  
|Livelli in una gerarchia|2^31-1 = 2.147.483.647|  
|Relazioni|2^31-1 = 2.147.483.647|  
|Colonne chiave in una tabella|2^31-1 = 2.147.483.647|  
|Misure in una tabella|2 ^ 31-1 = 2.147.483.647 **Avviso:** il numero totale di misure in una tabella dipende dal numero totale di colonne e colonne calcolate associate alla stessa tabella. Il numero massimo di "colonne + misure + colonne calcolate" per una tabella è di 2^31-1 = 2.147.483.647|  
|Colonne calcolate in una tabella|2 ^ 31-1 = 2.147.483.647 **Avviso:** il numero totale di colonne calcolate in una tabella dipende dal numero totale di colonne e misure associate alla stessa tabella. Il numero massimo di "colonne + misure + colonne calcolate" per una tabella è di 2^31-1 = 2.147.483.647|  
|Celle restituite da una query|2^31-1 = 2.147.483.647|  
|Dimensioni dei record della query di origine|64 KB|  
|Lunghezza dei nomi degli oggetti|100 caratteri|  
  
## <a name="see-also"></a>Vedere anche  
 [Determinare la modalità server di un'istanza di Analysis Services](../../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Proprietà generali](../../server-properties/general-properties.md)  
  
  
