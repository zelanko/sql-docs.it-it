---
title: Definire una relazione di tipo fatti e delle relative proprietà | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2341335d1d9c4904e1832e0a8087c0fa8198fd58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178842"
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>Definire una relazione di tipo Fatti e le relative proprietà
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando si definisce un nuovo gruppo di misure o una nuova dimensione del cubo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] prova a rilevare la presenza di una relazione tra dimensioni dei fatti e quindi imposta l'utilizzo delle dimensioni su **Fatti**. È possibile visualizzare o modificare una relazione di tipo Fatti nella scheda **Utilizzo dimensioni** di Progettazione cubi. La relazione di tipo Fatti tra una dimensione e un gruppo di misure presenta i vincoli seguenti:  
  
-   Una dimensione del cubo può avere un'unica relazione di tipo Fatti con un particolare gruppo di misure.  
  
-   Una dimensione del cubo può avere diverse relazioni di tipo Fatti con più gruppi di misure.  
  
-   L'attributo di granularità per la relazione deve essere l'attributo chiave, ad esempio il numero di transazione, della dimensione. Viene così creata una relazione uno-a-uno tra la dimensione e i fatti della tabella dei fatti.  
  
  
