---
title: Dialogo Definisci relazione (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.f1
helpviewer_keywords:
- Define Relationship dialog box
ms.assetid: 0fcee7f1-f138-4c2e-ae8c-245395ee0fe8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d80be1c4898ae00dfdbb88e22771c071636cf73c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082095"
---
# <a name="define-relationship-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Definisci relazione (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Definisci relazione** per definire una relazione tra una dimensione del cubo e un gruppo di misure in Progettazioni cubi. Per visualizzare la finestra di dialogo **Definisci relazione** , è possibile fare clic su **...** in una cella del riquadro **Griglia** della scheda **Utilizzo dimensioni** in Progettazione cubi.  
  
## <a name="options"></a>Opzioni  
 **Selezionare il tipo di relazione**  
 Consente di selezionare il tipo di relazione da creare tra la dimensione del cubo e il gruppo di misure. Quando si seleziona un tipo di relazione tra dimensioni, il contenuto del riquadro **Dettaglio** cambia di conseguenza.  
  
 Se si seleziona **Nessuna relazione** , non viene creata alcune relazione tra dimensioni.  
  
 **Detail**  
 Visualizza le opzioni disponibili per il tipo di relazione tra dimensioni selezionato in **Selezionare il tipo di relazione**.  
  
## <a name="detail-pane-options"></a>Opzioni del riquadro dei dettagli  
 A seconda del tipo di relazione specificato in **Selezionare il tipo di relazione** , nel riquadro **Dettaglio**vengono visualizzate le opzioni seguenti:  
  
|Tipo di relazione|Descrizione|Opzione|  
|-----------------------|-----------------|------------|  
|**Nessuna relazione**|Non viene definita alcuna relazione e pertanto nel riquadro **Dettaglio** non viene visualizzata alcuna opzione.||  
|**Regular**|Consente di impostare una relazione di tipo Regolare per la dimensione. Nel riquadro **Dettaglio** vengono visualizzate le opzioni seguenti:|**Attributo di granularità**: <br />                      Consente di selezionare l'attributo che definisce la granularità del gruppo di misure rispetto alla dimensione. Si tratta in genere di un attributo chiave della dimensione.|  
|||**Tabella della dimensione** : Consente di visualizzare la tabella principale della dimensione.|  
|||**Tabella del gruppo di misure** : Consente di visualizzare la tabella dei fatti relativa al gruppo di misure.|  
|||**Relazione**: Consente di visualizzare una griglia di colonne della dimensione e colonne di gruppo di misure in cui si basa la relazione. La griglia include le colonne seguenti:<br /><br /> **Colonne dimensione**: Visualizza le colonne associate all'attributo di granularità selezionato. Nota: Se la dimensione non è stata ancora generata, questa opzione è impostata su **genera**.<br />**Colonne gruppo di misure** :<br />                              Consente di selezionare le colonne nel gruppo di misure correlate alle colonne della dimensione.|  
|||**Avanzate**:<br />                      Fare clic su questo pulsante per visualizzare la finestra di dialogo **Associazioni gruppo di misure** e modificare le proprietà avanzate, ad esempio l'elaborazione di valori Null, relative alle relazioni tra attributi e colonne di gruppi di misure. Per altre informazioni sulla finestra di dialogo **Associazioni gruppo di misure**, vedere [Finestra di dialogo Associazioni gruppo di misure &#40;Analysis Services - Dati multidimensionali&#41;](measure-group-bindings-dialog-box-analysis-services-multidimensional-data.md).|  
|**Fact**|Consente di impostare una relazione di tipo Fatti per la dimensione. Nel riquadro **Dettaglio** vengono visualizzate le opzioni seguenti:|**Attributo di granularità**: Consente di selezionare l'attributo che definisce la granularità del gruppo di misure rispetto alla dimensione. Si tratta in genere di un attributo chiave della dimensione.|  
|||**Tabella delle dimensioni**: Consente di visualizzare la tabella della dimensione principale.|  
|||**Tabella del gruppo di misure**: <br />                      Consente di visualizzare la tabella su cui si basa il gruppo di misure.|  
|**Fa riferimento**|Consente di impostare una relazione di tipo Riferimento per la dimensione. Nel riquadro **Dettaglio** vengono visualizzate le opzioni seguenti:|**Dimensione di riferimento**: <br />                      Consente di visualizzare la dimensione selezionata.|  
|||**Dimensione intermedia**: <br />                      Consente di selezionare la dimensione intermedia.|  
|||**Attributo della dimensione di riferimento**: <br />                      Consente di selezionare l'attributo della dimensione di riferimento correlato all'attributo della dimensione intermedia specificato in **Attributo della dimensione intermedia**.|  
|||**Attributo della dimensione intermedia**: <br />                      Consente di selezionare l'attributo della dimensione intermedia correlato all'attributo della dimensione di riferimento specificato in **Dimensione di riferimento**.|  
|||**Materializza**: <br />                      Selezionare per memorizzare il membro dell'attributo nella dimensione intermedia che collega l'attributo nella dimensione di riferimento alla tabella dei fatti nella struttura MOLAP. La materializzazione della relazione è il comportamento predefinito per ottimizzare le prestazioni della query, a scapito di un aumento del tempo di elaborazione e dello spazio di archiviazione.|  
|**Molti-a-molti**|Consente di impostare una relazione di tipo molti-a-molti per la dimensione. Nel riquadro **Dettaglio** vengono visualizzate le opzioni seguenti:|**Dimensione** : Consente di visualizzare la dimensione selezionata.|  
|||**Gruppo di misure intermedio** : <br />                      Consente di selezionare il gruppo di misure intermedio associato.<br /><br /> Nota: Il gruppo di misure intermedio deve avere almeno una dimensione in comune con il gruppo di misure selezionato. La granularità della relazione tra il gruppo di misure intermedio e la dimensione comune deve essere inoltre maggiore o uguale alla granularità della relazione tra la dimensione comune e il gruppo di misure selezionato.|  
|**Data mining**|Consente di impostare una relazione di tipo Data mining per la dimensione. Nel riquadro **Dettaglio** vengono visualizzate le opzioni seguenti:|**Dimensione di destinazione**: Visualizza la dimensione di data mining.<br /><br /> Nota: È necessario selezionare una dimensione di data mining per creare una relazione tra dimensioni di data mining.|  
|||**Dimensione di origine**: Consente di selezionare la dimensione in base alla quale la dimensione di data mining elabora analisi predittive.|  
  
## <a name="see-also"></a>Vedere anche  
 [Relazioni tra dimensioni](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Utilizzo dimensioni &#40;Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
