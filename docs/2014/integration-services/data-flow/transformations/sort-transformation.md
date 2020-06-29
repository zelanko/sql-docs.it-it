---
title: Trasformazione Ordinamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sorttrans.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7039d02b6cc55355c3b27e5694474df4666570ef
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430128"
---
# <a name="sort-transformation"></a>Ordinamento - trasformazione
  La trasformazione Ordinamento consente di disporre i dati di input in ordine crescente o decrescente e di copiare i dati ordinati nell'output della trasformazione. A uno stesso input è possibile applicare più ordinamenti, ognuno dei quali è identificato da un numero che ne determina il tipo. La colonna con il numero più basso viene ordinata per prima, quindi viene ordinata quella con il secondo numero più basso e così via. Se ad esempio la colonna di nome **CountryRegion** ha come tipo di ordinamento 1 e la colonna di nome **City** ha come tipo di ordinamento 2, l'output verrà ordinato prima per country/region, quindi per city. Un numero positivo indica che l'ordinamento è crescente, mentre un numero negativo indica che è decrescente. Le colonne che non sono ordinate hanno un tipo di ordinamento 0. Le colonne non selezionate per l'ordinamento vengono copiate automaticamente nell'output della trasformazione insieme alle colonne ordinate.  
  
 La trasformazione Ordinamento include un set di opzioni di confronto che consentono di definire la modalità di gestione dei dati stringa in una colonna. Per altre informazioni, vedere [Comparing String Data](../comparing-string-data.md).  
  
> [!NOTE]  
>  La trasformazione Ordinamento non dispone i GUID nello stesso ordine della clausola ORDER BY in Transact-SQL. La trasformazione Ordinamento dispone i GUID che iniziano con 0-9 prima di quelli che iniziano con A-F, mentre la clausola ORDER BY li ordina in modo diverso, come implementato in [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]. Per altre informazioni, vedere [Clausola ORDER BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql).  
  
 La trasformazione Ordinamento è inoltre in grado di rimuovere le righe duplicate nell'ambito dell'operazione di ordinamento. Sono considerate duplicate le righe che hanno valori di chiave di ordinamento identici. Il valore della chiave di ordinamento viene generato in base alle opzioni utilizzate per il confronto delle stringhe e questo significa che stringhe letterali diverse possono avere gli stessi valori di chiave di ordinamento. La trasformazione identifica come duplicate le righe delle colonne di input che hanno valori di chiave di ordinamento identici, anche se i valori effettivi sono diversi.  
  
 La trasformazione Ordinamento include la proprietà personalizzata `MaximumThreads`, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md).  
  
 Questa trasformazione include un input e un output. Non supporta output degli errori.  
  
## <a name="configuration-of-the-sort-transformation"></a>Configurazione della trasformazione Ordinamento  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Ordinamento** , vedere [Editor trasformazione Ordinamento](../../sort-transformation-editor.md).  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [proprietà personalizzate della trasformazione](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni su come impostare le proprietà del componente, vedere [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 Esempio relativo al [componente SSIS personalizzato SortDeDuplicateDelimitedString](https://go.microsoft.com/fwlink/?LinkId=220821)su codeplex.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../data-flow.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
