---
title: Impostare un intervallo di blocco su un misuratore (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0ece7297-6e2f-47fb-835d-b9e9cce53fe2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e2a35e4d6fefb6830774ffd7b2c3bc13a5e097c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101370"
---
# <a name="set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs"></a>Impostazione di un intervallo di blocco su un misuratore (Generatore report e SSRS)
  Un intervallo di blocco definisce il multiplo in base al quale arrotondare i valori. Per impostazione predefinita, il misuratore punterà al valore esatto del campo specificato nel riquadro dei dati. È tuttavia possibile arrotondare il valore esatto per eccesso o per difetto in modo da bloccare l'indicatore di misura su un intervallo predefinito. Se, ad esempio, il valore sul misuratore è 34,2 e si specifica un intervallo di blocco pari a 5, l'indicatore di misura del misuratore punterà al valore 35. Se invece il valore sul misuratore è 31,2 e si specifica un intervallo di blocco pari a 5, l'indicatore di misura del misuratore punterà al valore 30.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-snapping-interval-on-a-gauge"></a>Per impostare un intervallo di blocco su un misuratore  
  
1.  Fare clic in un punto qualsiasi dei numeri del misuratore per evidenziare la scala.  
  
2.  Aprire il riquadro Proprietà.  
  
    > [!NOTE]  
    >  Se il riquadro proprietà non è visualizzato, fare clic sulla scheda **Visualizza** , quindi selezionare la casella di controllo **Proprietà** .  
  
3.  Nella proprietà **puntatori** fare clic sul pulsante (...). Verrà aperto l'editor di raccolta indicatori di misura.  
  
4.  Impostare la proprietà **SnappingEnabled** su `True`.  
  
5.  Impostare **SnappingInterval** su un valore che rappresenta l'intervallo di blocco. L'indicatore di misura verrà bloccato sul multiplo di arrotondamento più vicino al valore specificato.  
  
## <a name="see-also"></a>Vedi anche  
 [Formattazione di scale su un misuratore &#40;Generatore report e SSRS&#41;](report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formattazione di puntatori su un misuratore &#40;Generatore report e SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
