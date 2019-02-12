---
title: 'Attività 6: Impostazione di sinonimi | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a81a538e2cd15dd38a6c32993395cac20079b6f2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022276"
---
# <a name="task-6-setting-synonyms"></a>Attività 6: Impostazione di sinonimi
  In questa attività si definiscono due valori di dominio, **negli Stati Uniti** e **Stati Uniti**, del **Country** dominio come sinonimi con **United States** come il valore iniziale. Poiché il **utilizza valori iniziali** è stata selezionata l'opzione quando si crea il **paese** dominio, qualsiasi **negli Stati Uniti** valori per il **paese** dominio verranno restituiti come **Stati Uniti** (quanto United States è il valore iniziale). Visualizzare [Change Domain Values](https://msdn.microsoft.com/library/hh510408.aspx) per altri dettagli.  
  
1.  Selezionare **paese** dall'elenco di domini.  
  
2.  Passare al **i valori di dominio** scheda.  
  
3.  Fare clic su **Aggiungi nuovo valore dominio** pulsante sulla barra degli strumenti.  
  
4.  Tipo di **Stati Uniti** per il valore e premere **invio**.  
  
5.  Selezione multipla **Stati Uniti** e **Stati Uniti** usando CTRL o MAIUSC, fare doppio clic sugli elementi selezionati e quindi fare clic su **impostati come sinonimi**. Tramite DQS questi valori vengono raggruppati e uno di essi viene definito come valore iniziale con cui vengono sostituiti gli altri valori.  
  
     ![Menu Imposta come sinonimi](../../2014/tutorials/media/et-settingsynonyms-01.jpg "Menu Imposta come sinonimi")  
  
6.  Si noti che **Stati Uniti** è impostato come valore iniziale. Se si desidera che USA come valore iniziale, è possibile fare clic su USA e selezionare **imposta come iniziale** opzione. Per questa esercitazione viene usato **Stati Uniti** come valore iniziale.  
  
     ![Stati Uniti e USA come sinonimi](../../2014/tutorials/media/et-settingsynonyms-02.jpg "negli Stati Uniti e USA come sinonimi")  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 7: Creazione di un dominio composito](../../2014/tutorials/task-7-creating-a-composite-domain.md)  
  
  
