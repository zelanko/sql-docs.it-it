---
title: Editor trasformazione campionamento (pagina campionamento) di riga | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql12.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- Row Sampling Transformation Editor
ms.assetid: 544c7709-6de0-4c08-bda3-759985be9a05
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 30163b4d65ac6a732efb3f7c67a018f433a42ac0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056450"
---
# <a name="row-sampling-transformation-editor-sampling-page"></a>Editor trasformazione Campionamento righe (pagina Campionamento)
  Utilizzare la finestra di dialogo **Editor trasformazione Campionamento righe** per dividere parte di un input in un campione utilizzando il numero di righe specificato. La trasformazione divide l'input in due output separati.  
  
 Per ulteriori informazioni sulla trasformazione Campionamento righe, vedere [Row Sampling Transformation](data-flow/transformations/row-sampling-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Numero di righe**  
 Consente di specificare il numero di righe dell'input da utilizzare come campione.  
  
 È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.  
  
 **Nome output campione**  
 Consente di specificare un nome univoco per l'output che includerà le righe campionate. Il nome specificato verrà visualizzato in Progettazione SSIS.  
  
 **Nome output non selezionato**  
 Consente di specificare un nome univoco per l'output che conterrà le righe escluse dal campionamento. Il nome specificato verrà visualizzato in Progettazione SSIS.  
  
 **Usa il valore di inizializzazione casuale seguente**  
 Consente di specificare il valore di inizializzazione del campionamento per il generatore di numeri casuali utilizzato dalla trasformazione per creare un campione. È consigliato solo a scopo di sviluppo e test. Se non viene specificato alcun valore di inizializzazione casuale, la trasformazione utilizza il conteggio tick di Microsoft Windows come valore di inizializzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Trasformazione Campionamento percentuale](data-flow/transformations/percentage-sampling-transformation.md)  
  
  
