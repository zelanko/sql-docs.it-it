---
title: Impostazione informazioni origine (Creazione guidata partizione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifydsvandfacttables.f1
ms.assetid: b6c13587-c690-45d9-af90-b3d652afc55b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aca14c9462d847d91ae2b51dfdf179650ee06732
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068164"
---
# <a name="specify-source-information-partition-wizard"></a>Impostazione informazioni origine (Creazione guidata partizione)
  Utilizzare la pagina **Impostazione informazioni origine** per selezionare il gruppo di misure in cui creare la partizione, nonché la vista origine dati e le tabelle di filtro per la partizione.  
  
> [!CAUTION]  
>  Se in **Tabelle disponibili** si seleziona una tabella usata da un'altra partizione, sarà necessario specificare una query nella pagina **Limitazione righe** per evitare il rischio di duplicazioni di dati nel cubo.  
  
## <a name="options"></a>Opzioni  
 **Gruppo di misure**  
 Consente di selezionare un gruppo di misure per la partizione.  
  
 **Look in**  
 Consente di selezionare l'origine dei dati o la vista origine dati contenente le tabelle di origine per la partizione. Per impostazione predefinita, è selezionata la vista origine dati utilizzata dal gruppo di misure.  
  
 **Tabelle dei filtri**  
 Digitare la stringa usata per limitare le tabelle visualizzate in **Tabelle disponibili**per nome tabella.  
  
 **Trovare le tabelle**  
 Selezionare questa opzione per aggiornare l'elenco delle tabelle in **Tabelle disponibili**e per ridurre ulteriormente l'elenco, se in **Filtro tabelle**è stata specificata una stringa.  
  
 **Tabelle disponibili**  
 Consente di selezionare le tabelle da utilizzare come tabelle di origine per le partizioni. La **Creazione guidata partizione** crea una partizione per ogni tabella selezionata in **Tabelle disponibili**.  
  
 Se in **Filtro tabelle**non è indicato alcun filtro, questa opzione consentirà di visualizzare l'elenco di tutte le tabelle nell'origine dati o nella vista origine dati specificata in **Cerca in** , simili per struttura alla tabella dei fatti utilizzata dal gruppo di misure selezionato in **Gruppo di misure**.  
  
 Se in **Filtro tabelle**è specificato un filtro, l'elenco verrà ulteriormente ridotto tramite un confronto del filtro con i nomi di tabella che soddisfano i criteri precedenti. Verranno visualizzate solo le tabelle che contengono la stringa specificata in **Filtro tabelle** .  
  
> [!NOTE]  
>  Se sono selezionate più tabelle, non sarà possibile visualizzare la pagina **Limitazione righe** , né ridurre le righe per le partizioni create dalle tabelle specificate. Per limitare le righe per ogni partizione, eseguire la Creazione guidata partizione una volta per ogni tabella da cui deve essere creata la partizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni &#40;Analysis Services - Dati multidimensionali&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
