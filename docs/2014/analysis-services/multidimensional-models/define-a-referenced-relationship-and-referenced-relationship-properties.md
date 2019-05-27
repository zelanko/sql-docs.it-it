---
title: Definire una relazione di riferimento e le relative proprietà | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- referenced dimension relationship
- relationships [Analysis Services], referenced dimensions
ms.assetid: 5bb44b41-635b-4398-8fe9-0bfbb142553e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00305d00bb3a11cc4237e005a057c70d4c5f3397
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075756"
---
# <a name="define-a-referenced-relationship-and-referenced-relationship-properties"></a>Definire una relazione di tipo Riferimento e le relative proprietà
  È possibile definire una relazione di tipo Riferimento per la dimensione tramite la scheda **Utilizzo dimensioni** di Progettazione cubi. La relazione di tipo Riferimento viene definita specificando gli elementi seguenti:  
  
-   La dimensione intermedia con cui eseguire l'unione in join. A tale scopo, è possibile specificare una dimensione regolare o un'altra dimensione di riferimento.  
  
-   Un attributo della dimensione di riferimento che definisce il livello più basso in cui la dimensione è disponibile per l'aggregazione in relazione al gruppo di misure.  
  
-   L'attributo (chiave esterna) nella dimensione intermedia corrispondente all'attributo della dimensione di riferimento.  
  
 Si noti che la colonna che collega la dimensione di riferimento alla tabella dei fatti, che corrisponde in genere all'attributo chiave nella dimensione di riferimento, deve essere inoltre definita come attributo nella dimensione intermedia. Quando si crea una catena di dimensioni di riferimento, creare innanzitutto la relazione di tipo Regolare tra la prima dimensione nella catena e il gruppo di misure. Creare quindi ogni ulteriore relazione di tipo Riferimento nell'ordine corretto. È possibile creare una relazione di tipo Riferimento solo con una dimensione per la quale esiste una relazione con il gruppo di misure.  
  
 Quando si crea una relazione di tipo Riferimento, il collegamento dell'attributo della dimensione viene materializzato per impostazione predefinita. La materializzazione di un collegamento dell'attributo della dimensione determina la materializzazione o l'archiviazione del valore del collegamento tra la tabella dei fatti e la dimensione di riferimento per ogni riga nella struttura MOLAP della dimensione durante l'elaborazione. Ciò influisce in modo poco significativo sulle prestazioni di elaborazione e sui requisiti di archiviazione, ma determina un miglioramento delle prestazioni di esecuzione delle query.  
  
 In una dimensione di riferimento, la granularità viene specificata identificando l'attributo che definisce la relazione tra una dimensione di riferimento e il gruppo di misure corrispondente alla tabella principale della dimensione. Quando più dimensioni di riferimento sono concatenate, i riferimenti definiscono la relazione dalla dimensione più esterna al gruppo di misure.  
  
  
