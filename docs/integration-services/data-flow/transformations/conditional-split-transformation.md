---
description: Suddivisione condizionale - trasformazione
title: Suddivisione condizionale - trasformazione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.conditionalsplittrans.f1
- sql13.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2f70d8f963a6f26131099e6cd7d09d5019f9c6bc
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194669"
---
# <a name="conditional-split-transformation"></a>Suddivisione condizionale - trasformazione

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  La trasformazione Suddivisione condizionale consente di indirizzare righe di dati verso output diversi a seconda del contenuto dei dati. L'implementazione della trasformazione Suddivisione condizionale è simile a una struttura decisionale CASE in un linguaggio di programmazione. La trasformazione valuta una o più espressioni e, in base ai risultati, dirige la riga di dati verso l'output specificato. Questa trasformazione prevede inoltre un output predefinito, in modo che se una riga non corrisponde ad alcuna espressione venga indirizzata all'output predefinito.  
  
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
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include funzioni e operatori che è possibile usare per creare le espressioni che valutano i dati di input e dirigono i dati di output. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 La trasformazione Suddivisione condizionale include la proprietà personalizzata **FriendlyExpression**, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Questa trasformazione include un input, uno o più output e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Divisione di un set di dati tramite la trasformazione Suddivisione condizionale](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Divisione di un set di dati tramite la trasformazione Suddivisione condizionale](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
## <a name="conditional-split-transformation-editor"></a>Editor trasformazione Suddivisione condizionale
  Utilizzare la finestra di dialogo **Editor trasformazione Suddivisione condizionale** per creare espressioni e impostare l'ordine in cui vengono valutate, nonché per assegnare un nome agli output di una suddivisione condizionale. In questa finestra di dialogo sono inclusi funzioni e operatori matematici, di data/ora e per i valori stringa che possono essere utilizzati per la compilazione di espressioni. La prima condizione che restituisce true determina l'output a cui è indirizzata una riga.  
  
> [!NOTE]  
>  La trasformazione Suddivisione condizionale indirizza ogni riga di input a un unico output. Se si immettono più condizioni, la trasformazione invierà ogni riga al primo output per cui la condizione è verificata e ignorerà le successive condizioni per tale riga. Per valutare più condizioni consecutivamente, potrebbe essere necessario concatenare più trasformazioni Suddivisione condizionale nel flusso di dati.  
  
### <a name="options"></a>Opzioni  
 **Ordine**  
 Selezionare una riga e utilizzare i tasti di direzione a destra per modificare l'ordine in base a cui valutare le espressioni.  
  
 **Nome output**  
 Consente di specificare un nome per l'output. Per impostazione predefinita viene suggerito un elenco numerato di casi. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Condition**  
 Consente di digitare un'espressione o di compilarne una eseguendo un'operazione di trascinamento dall'elenco di operatori, funzioni, variabili e colonne disponibili.  
  
 È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.  
  
 **Argomenti correlati:**  [Espressioni di Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Operatori &#40;espressione SSIS&#41;](../../../integration-services/expressions/operators-ssis-expression.md) e [Funzioni &#40;espressione SSIS&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **Nome output predefinito**  
 Consente di immettere un nome per la trasformazione. In alternativa, utilizzare quello predefinito.  
  
 **Configura output errori**  
 Consente di indicare come gestire gli errori tramite la finestra di dialogo [Configura output errori](../error-handling-in-data.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
