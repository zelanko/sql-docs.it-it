---
title: Trasformazione UnPivot | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 98a8476ef317a0ddfa6f7fc27c0c9572ed12817a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770192"
---
# <a name="unpivot-transformation"></a>UnPivot - trasformazione
  La trasformazione tramite UnPivot consente di trasformare un set di dati non normalizzato in una versione più normalizzata, espandendo valori di più colonne contenuti in un singolo record in più record con gli stessi valori in un'unica colonna. Si consideri ad esempio un set di dati che elenca i nomi dei clienti e include una riga per ogni cliente, ognuna contenente colonne in cui sono indicati i prodotti e le quantità acquistati. Dopo la normalizzazione del set di dati tramite la trasformazione UnPivot, il set di dati conterrà una riga per ogni prodotto acquistato dal cliente.  
  
 Nella figura seguente viene illustrato un set di dati prima della trasformazione tramite UnPivot in base alla colonna Product.  
  
 ![Set di dati dopo la trasformazione tramite UnPivot](../../media/mw-dts-18.gif "Set di dati dopo la trasformazione tramite UnPivot")  
  
 Nella figura seguente viene illustrato un set di dati dopo la trasformazione tramite UnPivot in base alla colonna Product.  
  
 ![Set di dati prima della trasformazione tramite UnPivot](../../media/mw-dts-17.gif "Set di dati prima della trasformazione tramite UnPivot")  
  
 In alcuni casi, i risultati della trasformazione tramite UnPivot possono contenere righe con valori imprevisti. Se i dati di esempio da trasformare tramite UnPivot illustrati nel diagramma contenessero valori Null in tutte le colonne Qty per Fred, l'output conterrebbe solo una riga per Fred e non cinque. La colonna Qty conterrebbe valori Null oppure zero, in base al tipo di dati della colonna.  
  
## <a name="configuration-of-the-unpivot-transformation"></a>Configurazione della trasformazione UnPivot  
 La trasformazione UnPivot include la proprietà personalizzata `PivotKeyValue`, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md).  
  
 Questa trasformazione include un input e un output. Non include alcun output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione UnPivot** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor trasformazione UnPivot](../../unpivot-transformation-editor.md)  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md).  
  
  
