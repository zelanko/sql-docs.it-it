---
title: Finestra di dialogo Associazioni gruppo di misure (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.measuregroupbindings.f1
helpviewer_keywords:
- Measure Group Bindings dialog box
ms.assetid: ed642780-5350-438e-af73-b9ceab3f876d
author: minewiskan
ms.author: owend
ms.openlocfilehash: b4fb4b20fcccdabdf29aaf57dab65b1604a80a9e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541603"
---
# <a name="measure-group-bindings-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Associazioni gruppo di misure (Analysis Services - Dati multidimensionali)
  La finestra di dialogo **Associazioni gruppo di misure** consente di creare e modificare le relazioni dirette tra gli attributi di non granularità di una dimensione del cubo e le colonne di un gruppo di misure per una relazione tra dimensioni regolari nonché di specificare nella finestra di dialogo **Definisci relazione** le opzioni di elaborazione dei valori Null per tutti gli attributi di una dimensione del cubo.  
  
## <a name="options"></a>Opzioni  
 **Tabella del gruppo di misure**  
 Consente di visualizzare il nome della tabella dei fatti per il gruppo di misure selezionato.  
  
 **Attributes (Attributi)**  
 Consente di visualizzare una griglia di attributi e di tabelle delle dimensioni. Selezionare un attributo per creare o modificare le proprietà di **Relazione** per l'attributo selezionato. La griglia include le colonne seguenti:  
  
|Opzione|Definizione|  
|------------|----------------|  
|**Nome attributo**|Consente di visualizzare il nome dell'attributo.|  
|**Tabella della dimensione**|Consente di visualizzare il nome della tabella della dimensione su cui è basato l'attributo.|  
  
 **Relazione**  
 Consente di visualizzare una griglia di relazioni tra le colonne della tabella delle dimensioni per l'attributo selezionato e le colonne della tabella dei fatti per il gruppo di misure selezionato nonché l'opzione di elaborazione dei valori Null relativa alla relazione. La griglia include le colonne seguenti:  
  
|Opzione|Definizione|  
|------------|----------------|  
|**Colonne dimensione**|Consente di visualizzare le colonne della tabella delle dimensioni su cui è basato l'attributo selezionato in **Attributi** .|  
|**Colonne gruppo di misure**|Consente di selezionare **Ereditate dalla dimensione** per utilizzare la relazione del gruppo di misure ereditata dalla dimensione oppure selezionare una colonna della tabella dei fatti su cui è basato il gruppo di misure per definire in modo esplicito una relazione.|  
|**Elaborazione valori Null**|Consente di selezionare un'opzione di elaborazione dei valori Null per l'attributo. Per altre informazioni sulle opzioni di elaborazione dei valori Null, vedere [Elemento NullProcessing &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl).|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Definisci relazione &#40;Analysis Services-Dati multidimensionali&#41;](define-relationship-dialog-box-analysis-services-multidimensional-data.md)   
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
