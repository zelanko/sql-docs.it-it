---
title: Trasformazione Unione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergetrans.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 741ea39f6a60d7c9f52fb901a1b038a352e948b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770419"
---
# <a name="merge-transformation"></a>Unione - trasformazione
  La trasformazione Unione consente di combinare due set di dati ordinati in un singolo set di dati. Le righe di ogni set di dati vengono inserite nell'output in base ai valori delle relative colonne chiave.  
  
 Includendo la trasformazione Unione in un flusso di dati, è possibile eseguire le attività seguenti:  
  
-   Unire dati da due origini dei dati, ad esempio tabelle e file.  
  
-   Creare set di dati complessi, nidificando più trasformazioni Unione.  
  
-   Unire di nuovo le righe dopo aver corretto gli errori nei dati.  
  
 La trasformazione Unione è simile alle trasformazioni Unione input multipli. Utilizzare la trasformazione Unione input multipli anziché la trasformazione Unione nelle situazioni seguenti:  
  
-   Gli input della trasformazione non sono ordinati.  
  
-   Non è necessario che l'output combinato sia ordinato.  
  
-   La trasformazione include più di due input.  
  
## <a name="input-requirements"></a>Requisiti relativi all'input  
 Per eseguire la trasformazione Unione, è necessario che i relativi dati di input siano ordinati. Per altre informazioni su questo requisito importante, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 La trasformazione Unione richiede inoltre che le colonne da unire nei relativi input abbiano metadati corrispondenti. Non è ad esempio possibile unire una colonna con tipo di dati numeric a una colonna con tipo di dati character. Se i dati sono di tipo string, la lunghezza della colonna nel secondo input dovrà essere minore o uguale a quella della colonna nel primo input, alla quale verrà unita.  
  
 In Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] l'interfaccia utente della trasformazione Unione mappa automaticamente le colonne con gli stessi metadati. È quindi possibile eseguire il mapping manualmente altre colonne con tipi di dati compatibili.  
  
 Questa trasformazione include due input e un output. Non supporta un output degli errori.  
  
## <a name="configuration-of-the-merge-transformation"></a>Configurazione della trasformazione Unione  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Unione** , vedere [Editor trasformazione Unione](../../merge-transformation-editor.md).  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni dettagliate sull'impostazione delle proprietà, vedere i seguenti argomenti:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinamento dei dati per le trasformazioni Unione e Merge Join](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Merge join](merge-join-transformation.md)   
 [Trasformazione Unione input multipli](union-all-transformation.md)   
 [Flusso di dati](../data-flow.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
