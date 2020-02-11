---
title: Imposta punti di interruzione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.setbreakpoints.f1
helpviewer_keywords:
- Set Breakpoints dialog box
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0c2c543343bd602be75d600a489edfd84663790b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62911403"
---
# <a name="set-breakpoints"></a>Imposta punti di interruzione
  Utilizzare la finestra di dialogo **Imposta punti di interruzione** per specificare gli eventi su cui abilitare i punti di interruzione e per controllarne il funzionamento.  
  
## <a name="options"></a>Opzioni  
 **Enabled**  
 Consente di abilitare un punto di interruzione su un evento.  
  
 **Condizione di interruzioni**  
 Consente di visualizzare un elenco di eventi disponibili sui quali è possibile impostare i punti di interruzione.  
  
 **Tipo di passaggi**  
 Consente di specificare quando il punto di interruzione diventa effettivo.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Sempre**|L'esecuzione viene sempre sospesa al rilevamento di un punto di interruzione.|  
|**Numero di passaggi uguale a**|L'esecuzione viene sospesa quando il punto di interruzione viene rilevato per un numero di volte uguale al numero di passaggi specificato.|  
|**Hit maggiore o uguale a**|L'esecuzione viene sospesa quando il punto di interruzione viene rilevato per un numero di volte maggiore o uguale al numero di passaggi specificato.|  
|**Numero di passaggi multiplo di**|L'esecuzione viene sospesa quando il punto di interruzione viene rilevato per un numero di volte multiplo del numero di passaggi specificato. Se ad esempio questa opzione è impostata su 5, l'esecuzione verrà sospesa ogni cinque volte.|  
  
 **Numero di passaggi**  
 Consente di specificare il numero di passaggi al raggiungimento del quale attivare un'interruzione. Questa opzione non è disponibile se il punto di interruzione è sempre attivo.  
  
## <a name="see-also"></a>Vedere anche  
 [Debug del flusso di controllo](../../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  
