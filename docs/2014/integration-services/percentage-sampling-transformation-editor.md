---
title: Editor trasformazione Campionamento percentuale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- Percentage Sampling Transformation Editor
ms.assetid: 2c40d804-26a3-4d35-809b-bc923d83d451
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0366ecb08281a28d43bc98639bf4b11e60aea402
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056715"
---
# <a name="percentage-sampling-transformation-editor"></a>Editor trasformazione Campionamento percentuale
  Utilizzare la finestra di dialogo **Editor trasformazione Campionamento percentuale** per dividere parte di un input in un campione utilizzando la percentuale di righe specificata. La trasformazione divide l'input in due output separati.  
  
 Per ulteriori informazioni sulla trasformazione Campionamento percentuale, vedere [Percentage Sampling Transformation](data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Percentuale di righe**  
 Consente di specificare la percentuale di righe dell'input da utilizzare come campione.  
  
 È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.  
  
 **Nome output campione**  
 Consente di specificare un nome univoco per l'output che includerà le righe campionate. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Nome output non selezionato**  
 Consente di specificare un nome univoco per l'output che conterrà le righe escluse dal campionamento. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Usa il valore di inizializzazione casuale seguente**  
 Consente di specificare il valore di inizializzazione del campionamento per il generatore di numeri casuali utilizzato dalla trasformazione per creare un campione. È consigliato solo a scopo di sviluppo e test. Se non viene specificato alcun valore di inizializzazione casuale, la trasformazione utilizza il conteggio tick di Microsoft Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Campionamento righe - trasformazione](data-flow/transformations/row-sampling-transformation.md)  
  
  
