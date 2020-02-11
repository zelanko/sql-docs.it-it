---
title: Operatori unari nelle dimensioni padre-figlio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- UnaryOperatorColumn property
- attributes [Analysis Services], unary operators
- unary operators
ms.assetid: b8ef549c-5458-458a-bf1a-fd743a1417fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25c1acf7a1fadbc79b7781488143ce57881c81fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073450"
---
# <a name="unary-operators-in-parent-child-dimensions"></a>Operatori unari nelle dimensioni padre-figlio
  In una dimensione che contiene una relazione padre-figlio in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è necessario specificare una colonna dell'operatore unario (o rollup personalizzato) che determina il rollup personalizzato per tutti i membri non calcolati dell'attributo padre. L'operatore unario viene applicato ai membri ogni volta che i valori dei membri padre vengono valutati. La proprietà **UnaryOperatorColumn** in un attributo padre (**Usage**=Parent) specifica la colonna di una tabella nella vista origine dati contenente gli operatori unari. I valori per gli operatori di rollup personalizzato archiviati in questa colonna vengono applicati a ogni membro dell'attributo.  
  
 È possibile creare e specificare un calcolo denominato in una tabella della dimensione nella vista origine dati come colonna dell'operatore unario. L'espressione più semplice, ad esempio '+', restituisce lo stesso operatore per tutti i membri. È tuttavia possibile utilizzare qualsiasi espressione a condizione che restituisca un operatore per ogni membro.  
  
 È possibile modificare manualmente l'impostazione della proprietà **UnaryOperatorColumn** in un attributo padre oppure usare la funzionalità avanzata di definizione della funzione di aggregazione personalizzata disponibile in Configurazione guidata funzionalità di Business Intelligence per sostituire la funzione di aggregazione predefinita associata ai membri di una dimensione. Per altre informazioni sull'uso di Configurazione guidata funzionalità di Business Intelligence per eseguire questa configurazione, vedere [Aggiungere un'aggregazione personalizzata a una dimensione](bi-wizard-add-a-custom-aggregation-to-a-dimension.md).  
  
 L'impostazione predefinita della proprietà **UnaryOperatorColumn** in un attributo è (nessuna), ovvero gli operatori di rollup personalizzato sono disabilitati. Nella tabella seguente vengono elencati gli operatori unari e viene descritta la loro funzione quando vengono applicati a un livello.  
  
|Operatore unario|Descrizione|  
|--------------------|-----------------|  
|+ (segno di addizione)|Il valore del membro viene aggiunto al valore aggregato dei membri di pari livello precedenti. Si tratta dell'operatore predefinito se per un attributo non viene definita alcuna colonna dell'operatore unario.|  
|-(segno meno)|Il valore del membro viene sottratto dal valore aggregato dei membri di pari livello precedenti.|  
|* (asterisco)|Il valore del membro viene moltiplicato per il valore aggregato dei membri di pari livello precedenti.|  
|/ (barra)|Il valore del membro viene diviso per il valore aggregato dei membri di pari livello precedenti.|  
|~ (tilde)|Il valore del membro viene ignorato.|  
  
 I valori vuoti e qualsiasi altro valore non presente nella tabella vengono considerati come operatori unari (+). Poiché non esiste un ordine di precedenza tra gli operatori, l'ordine di valutazione è determinato dall'ordine dei membri archiviati nella colonna dell'operatore unario. Per modificare l'ordine di valutazione, creare un nuovo attributo, impostarne la proprietà **Type** su **Sequence**e quindi assegnare numeri di sequenza corrispondenti all'ordine di valutazione nella relativa proprietà **Source Column** . È inoltre necessario ordinare i membri dell'attributo in base a tale attributo. Per altre informazioni sull'uso di Configurazione guidata funzionalità di Business Intelligence per ordinare i membri di un attributo, vedere [Definire l'ordinamento di una dimensione](bi-wizard-define-the-ordering-for-a-dimension.md).  
  
 È possibile usare la proprietà **UnaryOperatorColumn** per specificare un calcolo denominato che restituisca un operatore unario come valore letterale per tutti i membri dell'attributo. È sufficiente digitare un carattere letterale quale `'*'` nel calcolo denominato. In questo modo l'operatore predefinito, ovvero il segno di addizione (+), viene sostituito dall'operatore di moltiplicazione, ovvero l'asterisco (*), per tutti i membri dell'attributo. Per ulteriori informazioni, vedere [definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
 Nella scheda **Esplorazione** di Progettazione dimensioni è possibile visualizzare gli operatori unari accanto a ogni membro di una gerarchia. È inoltre possibile modificare gli operatori unari in caso di utilizzo di una dimensione abilitata per la scrittura. Se la dimensione non è abilitata per la scrittura, è necessario utilizzare uno strumento per modificare direttamente l'origine dei dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alle proprietà degli attributi delle dimensioni](dimension-attribute-properties-reference.md)   
 [Operatori di rollup personalizzati nelle dimensioni padre-figlio](parent-child-dimension-attributes-custom-rollup-operators.md)   
 [Avviare la Configurazione guidata funzionalità di Business Intelligence in Progettazione dimensioni](database-dimensions-bi-wizard-in-dimension-designer.md)  
  
  
