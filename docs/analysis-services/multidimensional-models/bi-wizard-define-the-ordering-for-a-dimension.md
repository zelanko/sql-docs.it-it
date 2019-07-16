---
title: Definire l'ordinamento di una dimensione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f2e9dfce4abc66e9fa77a7d429c3cdd9a306c69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209144"
---
# <a name="bi-wizard---define-the-ordering-for-a-dimension"></a>Procedura guidata per BI - Definire l'ordinamento di una dimensione
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  L'aggiunta della funzionalità avanzata di ordinamento degli attributi a un cubo o una dimensione consente di specificare come verranno ordinati i membri di un attributo. I membri possono essere ordinati in base al nome o alla chiave dell'attributo oppure in base al nome o alla chiave di un altro attributo (tramite una relazione tra attributi). Per impostazione predefinita, i membri vengono ordinati in base al nome. Questa funzionalità avanzata modifica l'impostazione delle proprietà **OrderBy** e **OrderByAttributeID** degli attributi in una dimensione.  
  
 Per aggiungere la funzionalità di ordinamento degli attributi, usare Configurazione guidata funzionalità di Business Intelligence e quindi selezionare l'opzione **Impostazione ordinamento attributi** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi relativi alla selezione di una dimensione alla quale si desidera applicare l'ordinamento degli attributi e all'impostazione della modalità di ordinamento degli attributi per la dimensione selezionata.  
  
## <a name="selecting-a-dimension"></a>Selezione di una dimensione  
 Nella prima pagina **Impostazione ordinamento attributi** della procedura guidata specificare la dimensione alla quale si desidera applicare l'ordinamento degli attributi. L'aggiunta della funzionalità avanzata dell'ordinamento degli attributi alla dimensione selezionata implica modifiche alla dimensione. Tali modifiche verranno ereditate da tutti i cubi che includono la dimensione selezionata.  
  
## <a name="specifying-ordering"></a>Impostazione dell'ordinamento  
 Nella seconda pagina **Impostazione ordinamento attributi** della procedura guidata specificare la modalità di ordinamento di tutti gli attributi nella dimensione.  
  
 Nella colonna **Attributo di ordinamento** è possibile modificare l'attributo usato per l'ordinamento. Se l'attributo che si desidera utilizzare per ordinare i membri non è presente nell'elenco, scorrere verso il basso nell'elenco e quindi selezionare  **\<nuovo attributo... >** per aprire la **seleziona una colonna** della finestra di dialogo in cui è possibile Selezionare una colonna nella tabella della dimensione. La selezione di una colonna tramite la finestra di dialogo **Seleziona colonna** consente di creare un attributo aggiuntivo in base al quale ordinare i membri di un attributo.  
  
 Nella colonna **Criteri** è quindi possibile selezionare se ordinare i membri dell'attributo in base alla **chiave** oppure al **nome**.  
  
  
