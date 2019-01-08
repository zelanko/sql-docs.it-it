---
title: Trasformazione Unione input multipli | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unionalltrans.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 127af76434b3c2d32b9bfd5d7ba69b80b69a4b84
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754863"
---
# <a name="union-all-transformation"></a>Unione input multipli - trasformazione
  La trasformazione Unione input multipli consente di combinare più input in un unico output. È ad esempio possibile utilizzare gli output di cinque diverse origini file flat come input per la trasformazione Unione input multipli e combinarli in un singolo output.  
  
## <a name="inputs-and-outputs"></a>Input e output  
 Gli input della trasformazione vengono aggiunti all'output della trasformazione uno dopo l'altro, senza riordinare le righe. Se il pacchetto richiede un output ordinato, sarà necessario utilizzare la trasformazione Unione anziché la trasformazione Unione input multipli.  
  
 L'output della trasformazione Unione input multipli viene creato a partire dal primo input connesso alla trasformazione. Sulle colonne negli input connessi successivamente alla trasformazione viene eseguito il mapping a quelle dell'output della trasformazione.  
  
 Per unire gli input è necessario eseguire il mapping delle relative colonne alle colonne nell'output. È necessario eseguire il mapping di almeno una colonna di input a ogni colonna di output. Il mapping tra due colonne può essere eseguito solo se i relativi metadati corrispondono. Le colonne sulle quali viene eseguito il mapping devono ad esempio avere lo stesso tipo di dati.  
  
 Se le colonne sulle quali viene eseguito il mapping contengono dati stringa e la lunghezza della colonna di output è inferiore a quella della colonna di input, la lunghezza della colonna di output verrà aumentata automaticamente in modo che possa contenere la colonna di input. Le colonne di input sulle quali non viene eseguito il mapping a colonne di output vengono impostate su valori Null nelle colonne di output.  
  
 Questa trasformazione include più input e un output. Non supporta un output degli errori.  
  
## <a name="configuration-of-the-union-all-transformation"></a>Configurazione della trasformazione Unione input multipli  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Unione** , vedere [Editor trasformazione Unione input multipli](../../union-all-transformation-editor.md).  
  
 Per altre informazioni sulle proprietà che è possibile impostare a livello di codice, vedere [Proprietà comuni](../../common-properties.md).  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostare le proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Unione di dati tramite la trasformazione Unione input multipli](union-all-transformation.md)  
  
  
