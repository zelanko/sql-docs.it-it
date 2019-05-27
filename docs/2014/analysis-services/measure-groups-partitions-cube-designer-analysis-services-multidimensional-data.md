---
title: Misurare i gruppi (scheda partizioni, Progettazione cubi) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitionspane.measuregroupdetail.f1
ms.assetid: 58e44b24-cfcd-4908-b445-d4374b961b98
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 587b3ef7c784b48c1347276646d366eae5570c97
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077904"
---
# <a name="measure-groups-partitions-tab-cube-designer-analysis-services---multidimensional-data"></a>Gruppi di misure (scheda Partizioni, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare il riquadro **Gruppi di misure** della scheda **Partizioni** di Progettazione cubi per gestire le partizioni associate a ogni gruppo di misure nel cubo.  
  
## <a name="options"></a>Opzioni  
 **Partizioni**  
 Consente di visualizzare una griglia contenente l'elenco delle partizioni che supportano il gruppo di misure selezionato. La griglia include le colonne seguenti:  
  
 **(Ordinale)**  
 Consente di visualizzare la posizione ordinale della partizione all'interno del gruppo di misure.  
  
 Fare clic per selezionare l'intera riga per la partizione.  
  
 **Nome partizione**  
 Consente di digitare il nome della partizione selezionata.  
  
 **Origine**  
 Consente di digitare il nome della tabella (per l'associazione di tabelle) o della query (per l'associazione di query) che fornisce i dati della tabella dei fatti per la partizione selezionata.  
  
 Fare clic sul pulsante **...** per visualizzare la finestra di dialogo **Origine partizione** e definire l'origine per la partizione selezionata.  
  
 **Aggregazione**  
 Consente di visualizzare le modalità di aggregazione e archiviazione della partizione. La modalità di archiviazione, ovvero ROLAP (Relational Online Analytical Processing), MOLAP (Multidimensional Online Analytical Processing) oppure HOLAP (Hybrid Online Analytical Processing), viene visualizzata per prima. La modalità di aggregazione viene visualizzata come percentuale dell'ottimizzazione richiesta, come misura dello spazio richiesto o utilizzato oppure come numero di aggregazioni create. Fare clic sul pulsante **...** per visualizzare la **Progettazione guidata aggregazioni** e definire la progettazione delle aggregazioni per la partizione specificata.  
  
 **Descrizione**  
 Consente di digitare una descrizione facoltativa della partizione.  
  
 **Nuova partizione...**  
 Fare clic per visualizzare la **Creazione guidata partizione** e creare una nuova partizione nel gruppo di misure selezionato.  
  
 **Impostazioni di archiviazione...**  
 Fare clic per visualizzare la finestra di dialogo **Impostazioni di archiviazione** e specificare la modalità di archiviazione, la memorizzazione nella cache attiva e le impostazioni di notifica per la partizione selezionata.  
  
> [!NOTE]  
>  Questa opzione è attivata solo se nella griglia **Partizioni** del gruppo di misure selezionato è stata selezionata una qualsiasi cella di una partizione.  
  
 **Impostazioni writeback...**  
 Fare clic su questo pulsante per visualizzare la finestra di dialogo **Abilita/Disabilita writeback** e specificare le impostazioni writeback per il gruppo di misure selezionato.  
  
## <a name="context-menu"></a>Menu di scelta rapida  
 Le opzioni seguenti sono disponibili nel menu di scelta rapida che viene visualizzato quando si fa clic con il pulsante destro del mouse su una riga della griglia **Partizioni** di un gruppo di misure selezionato:  
  
|Opzione|Definizione|  
|------------|----------------|  
|**Aggiungere funzionalità di Business Intelligence**|Fare clic su questa opzione per visualizzare la **Configurazione guidata funzionalità di Business Intelligence** e aggiungere funzionalità di Business Intelligence al cubo. Per altre informazioni sulla **Configurazione guidata funzionalità di Business Intelligence**, vedere [Guida sensibile al contesto della Configurazione guidata funzionalità di Business Intelligence](business-intelligence-wizard-f1-help.md).|  
|**Nuova partizione**|Fare clic per visualizzare la **Creazione guidata partizione** e creare una nuova partizione nel gruppo di misure selezionato.|  
|**Rinomina partizione**|Selezionare questa opzione per rinominare la partizione selezionata.|  
|**Elimina**|Fare clic per visualizzare la finestra di dialogo **Elimina oggetti** ed eliminare l'azione selezionata.<br /><br /> Nota: Questa opzione è disabilitata se è stata selezionata una partizione writeback.|  
|**Progettare le aggregazioni**|Fare clic per visualizzare la **Progettazione guidata aggregazioni** e creare una progettazione delle aggregazioni per la partizione selezionata.<br /><br /> Nota: Questa opzione è disabilitata se è stata selezionata una partizione writeback.|  
|**Impostazioni di archiviazione**|Fare clic per visualizzare la finestra di dialogo **Impostazioni di archiviazione** e specificare la modalità di archiviazione, la memorizzazione nella cache attiva e le impostazioni di notifica per la partizione selezionata.|  
|**Impostazioni writeback**|Fare clic su questo pulsante per visualizzare la finestra di dialogo **Abilita/Disabilita writeback** e specificare le impostazioni writeback per il gruppo di misure contenente la partizione selezionata.|  
|**Ottimizzazione basata sulle statistiche sull'utilizzo**|Fare clic per visualizzare l' **Ottimizzazione guidata basata sulle statistiche di utilizzo** e creare una progettazione delle aggregazioni basata su modelli di utilizzo esistenti per la partizione selezionata.<br /><br /> Nota: Questa opzione è disabilitata se è stata selezionata una partizione writeback.|  
|**Process**|Fare clic per visualizzare la finestra di dialogo **Elabora** ed elaborare la partizione selezionata.|  
|**Copia**|Questa opzione è disabilitata.|  
|**Incolla**|Questa opzione è disabilitata.|  
|**Proprietà**|Selezionare questa opzione per visualizzare la finestra di dialogo **Proprietà** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per la partizione selezionata.|  
  
  
