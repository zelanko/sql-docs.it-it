---
title: Opzioni schema database area di interesse (generazione guidata schema) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.schemagenwizard.subjectareaschemaopts.f1
ms.assetid: 4c109bb8-e19d-412b-908f-bfdd7f872439
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2173255654b9ef02c269ec34bd21f93f8bf629a3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067982"
---
# <a name="subject-area-database-schema-options-schema-generation-wizard-analysis-services---multidimensional-data"></a>Opzioni schema database area di interesse (Generazione guidata schema) (Analysis Services - Dati multidimensionali)
  Utilizzare la pagina **Opzioni schema database area di interesse** per controllare la generazione dello schema e definire la modalità di mantenimento dei dati.  
  
## <a name="options"></a>Opzioni  
 **Nome schema**  
 Consente di specificare il nome dello schema all'interno del nuovo database dell'area di interesse.  
  
 **Crea chiavi primarie nelle tabelle delle dimensioni**  
 Consente di creare chiavi primarie nelle tabelle delle dimensioni nello schema generato. Se non si seleziona questa opzione non viene generato alcun indice.  
  
> [!NOTE]  
>  Se non si seleziona questa opzione viene applicata l'integrità referenziale.  
  
 **Creare indici**  
 Consente di creare indici su colonne chiave esterna nello schema generato.  
  
 **Applica integrità referenziale**  
 Consente di applicare l'integrità referenziale all'interno dello schema generato. Se non si seleziona questa opzione le relazioni vengono create ma non applicate.  
  
 **Mantieni dati in caso di rigenerazione**  
 Consente di mantenere i dati nel database dell'area di interesse al termine della procedura guidata. Se non si seleziona questa opzione tutti i dati nel database dell'area di interesse possono essere cancellati senza notifica.  
  
 **Popola tabelle dei tempi**  
 Consente di specificare la modalità di popolamento delle tabelle dei tempi da parte della procedura guidata. Nella tabella seguente vengono descritti i valori possibili per questa opzione.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo se la Generazione guidata schema viene avviata da un progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] in modalità progetto.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Popola|Le tabelle dei tempi dell'area di interesse vengono popolate.|  
|Non popolare|Le tabelle dei tempi dell'area di interesse non vengono popolate.|  
|Popola solo se vuota|Le tabelle dei tempi dell'area di interesse vengono popolate solo se sono vuote.|  
  
## <a name="see-also"></a>Vedi anche  
 [Guida sensibile al contesto della generazione guidata schema &#40;Analysis Services-Dati multidimensionali&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)  
  
  
