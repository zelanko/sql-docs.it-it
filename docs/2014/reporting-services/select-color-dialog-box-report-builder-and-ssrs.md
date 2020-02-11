---
title: Finestra di dialogo Seleziona colore (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.selectcolor.f1
- "10090"
helpviewer_keywords:
- Select Color dialog box
ms.assetid: ac7089a3-5c7b-4f53-8348-180610e86da2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6bcbbe828da811ace5df4feea5cfdf888e1e6ca5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101375"
---
# <a name="select-color-dialog-box-report-builder-and-ssrs"></a>Finestra di dialogo Seleziona colore (Generatore report e SSRS)
  Utilizzare la finestra di dialogo **Seleziona colore** per specificare le opzioni relative al colore per lo sfondo di una o più celle in un'area dati o in una casella di testo oppure per un grafico.  
  
## <a name="options"></a>Opzioni  
 **Selettore colori**  
 Scegliere una delle tre opzioni disponibili per specificare la modalità di selezione dei colori:  
  
-   **Selezione-cerchio colori** Scegliere un colore utilizzando i valori dei colori HSB (Hue/Saturation/Brightness).  
  
-   **Selezione-quadrato colori** Scegliere un colore usando i valori di colore rosso/verde/blu (RGB).  
  
-   **Tavolozza-colori standard** Scegliere un colore da un elenco predefinito di valori dei colori.  
  
 **Cerchio colori**  
 Utilizzare questa opzione per i colori HSB perché il mapping dei valori HSB viene eseguito su un sistema di coordinate cilindrico. La tonalità corrisponde al colore effettivo, la saturazione alla purezza del colore, la luminosità alla luminosità o alla oscurità relativa.  
  
 Quando si effettua una scelta, il centro del cerchio determina il colore. Utilizzare il dispositivo di scorrimento del colore per cambiare la tonalità. Le coordinate x e y rappresentano rispettivamente i valori di saturazione e luminosità.  
  
 **Quadrato colori**  
 Utilizzare questa opzione per i colori RGB perché il mapping dei valori RGB viene eseguito su un sistema di coordinate cartesiano. R corrisponde al valore del rosso, G al valore del verde e B al valore del blu.  
  
 Quando si effettua una scelta, il centro del quadrato determina il colore. Utilizzare il dispositivo di scorrimento del colore per cambiare la gamma del colore scelto. Le coordinate x e y rappresentano gli altri due colori. Se ad esempio si sceglie il colore verde, il dispositivo di scorrimento visualizza la gamma di valori del verde, mentre le coordinate x e y rappresentano rispettivamente i valori del rosso e del blu.  
  
 **Tavolozza colori standard**  
 Utilizzare per i colori denominati dall' [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] `KnownColor` enumerazione.  
  
 **Sistema colori**  
 Specificare i colori RGB o HSB. Questa opzione consente di visualizzare i valori RGB o HSB, che vengono aggiornati in modo interattivo quando si utilizza un cerchio o un quadrato di colori per **Selettore colori**.  
  
 Il valore **Alfa** viene visualizzato per alcune proprietà quando un colore può includere un valore di trasparenza, ad esempio nel caso del riempimento della serie del grafico. Per le proprietà che non supportano la trasparenza, questo valore è disabilitato.  
  
 **Rosso**  
 Valore decimale relativo alla parte rossa del colore RGB. Utilizzare la casella di selezione per modificare il valore o digitare un valore compreso tra 0 e 255.  
  
 **Verde**  
 Valore decimale relativo alla parte verde del colore RGB. Utilizzare la casella di selezione per modificare il valore o digitare un valore compreso tra 0 e 255.  
  
 **Blu**  
 Valore decimale relativo alla parte blu del colore RGB. Utilizzare la casella di selezione per modificare il valore o digitare un valore compreso tra 0 e 255.  
  
 **Alfa**  
 Valore decimale relativo alla parte alfa o di trasparenza del colore. Quando questo valore è abilitato, è possibile utilizzare il dispositivo di scorrimento per regolare il grado di trasparenza desiderato.  
  
 **Hue**  
 Valore decimale relativo alla tonalità del colore HSB. Utilizzare la casella di selezione per modificare il valore o digitare un valore compreso tra 0 e 255.  
  
 **Saturazione**  
 Valore decimale relativo alla saturazione del colore HSB. Utilizzare la casella di selezione per modificare il valore o digitare un valore compreso tra 0 e 255.  
  
 **Brightness (Luminosità)**  
 Valore decimale relativo alla luminosità del colore HSB. Utilizzare la casella di selezione per modificare il valore o digitare un valore compreso tra 0 e 255.  
  
 **Esempio di colore**  
 Visualizza il colore corrente nella parte sinistra del riquadro e mostra in modo interattivo il nuovo colore scelto nella parte destra. Se non è presente un colore predefinito, la parte sinistra del riquadro è bianca. Per la maggior parte delle proprietà RDL non è disponibile alcun colore predefinito.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione degli elementi del report &#40;Generatore report e SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Formattazione di testo e segnaposto &#40;Generatore report e SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
