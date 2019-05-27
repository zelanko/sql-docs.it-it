---
title: Definire una relazione di tipo fatti e delle relative proprietà | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 471a65cb8f7560b409e6ddf8f73969d83d42a346
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075788"
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>Definire una relazione di tipo Fatti e le relative proprietà
  Quando si definisce un nuovo gruppo di misure o una nuova dimensione del cubo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di rilevare la presenza di una relazione di tipo Fatti per la dimensione e quindi imposta l'utilizzo della dimensione su `Fact`. È possibile visualizzare o modificare una relazione di tipo Fatti nella scheda **Utilizzo dimensioni** di Progettazione cubi. La relazione di tipo Fatti tra una dimensione e un gruppo di misure presenta i vincoli seguenti:  
  
-   Una dimensione del cubo può avere un'unica relazione di tipo Fatti con un particolare gruppo di misure.  
  
-   Una dimensione del cubo può avere diverse relazioni di tipo Fatti con più gruppi di misure.  
  
-   L'attributo di granularità per la relazione deve essere l'attributo chiave, ad esempio il numero di transazione, della dimensione. Viene così creata una relazione uno-a-uno tra la dimensione e i fatti della tabella dei fatti.  
  
  
