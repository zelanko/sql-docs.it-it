---
title: Suddivisione condizionale - trasformazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittrans.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dcfbbac9eacc96384a723088cf8f20cc939bdc48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900825"
---
# <a name="conditional-split-transformation"></a>Suddivisione condizionale - trasformazione
  La trasformazione Suddivisione condizionale consente di indirizzare righe di dati verso output diversi a seconda del contenuto dei dati. L'implementazione della trasformazione Suddivisione condizionale è simile a una struttura decisionale CASE in un linguaggio di programmazione. La trasformazione valuta una o più espressioni e, in base ai risultati, dirige la riga di dati verso l'output specificato. Questa trasformazione prevede inoltre un output predefinito, verso il quale vengono indirizzate le righe che non corrispondono ad alcuna espressione.  
  
## <a name="configuration-of-the-conditional-split-transformation"></a>Configurazione della trasformazione Suddivisione condizionale  
 Per configurare la trasformazione Suddivisione condizionale, procedere nel modo seguente:  
  
-   Specificare un'espressione che restituisce un valore booleano per ogni condizione che dovrà essere verificata dalla trasformazione.  
  
-   Specificare l'ordine in cui devono essere valutate le condizioni. L'ordine è estremamente importante, perché ogni riga viene inviata all'output corrispondente alla prima condizione che restituisce True.  
  
-   Specificare l'output predefinito per la trasformazione. La trasformazione richiede che venga specificato un output predefinito.  
  
 Ogni riga di input può essere inviata a un solo output, ovvero quello corrispondente alla prima condizione che restituisce True. Le condizioni seguenti, ad esempio, dirigono tutte le righe della colonna **FirstName** che iniziano con la lettera *A* a un determinato output, a un altro output le righe che iniziano con la lettera *B* e tutte le altre righe all'output predefinito.  
  
 Output 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 Output 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include funzioni e operatori che è possibile usare per creare le espressioni che valutano i dati di input e dirigono i dati di output. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md).  
  
 La trasformazione Suddivisione condizionale include la proprietà personalizzata `FriendlyExpression`, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](../../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md).  
  
 Questa trasformazione include un input, uno o più output e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Suddivisione condizionale** , vedere [Editor trasformazione Suddivisione condizionale](../../conditional-split-transformation-editor.md).  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Dividere un set di dati tramite la trasformazione Suddivisione condizionale](conditional-split-transformation.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Divisione di un set di dati tramite la trasformazione Suddivisione condizionale](conditional-split-transformation.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../data-flow.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
