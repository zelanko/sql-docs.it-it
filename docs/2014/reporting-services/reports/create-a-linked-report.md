---
title: Creare un report collegato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 27667eececc3905b927b7e888e692a8261d14d30
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177060"
---
# <a name="create-a-linked-report"></a>Creare un report collegato
  Un report collegato è un elemento del server di report che fornisce un punto di accesso a un report esistente. Tale elemento è concettualmente simile al collegamento a un programma utilizzato per l'esecuzione di un programma o per l'apertura di un file.

 Un report collegato viene derivato da un report esistente e mantiene la definizione del report originale. Un report collegato, inoltre, eredita sempre il layout del report e le proprietà dell'origine dati del report originale. Tutte le altre proprietà e impostazioni, ad esempio sicurezza, parametri, percorso, sottoscrizioni e pianificazioni, possono essere diverse da quelle del report originale.

 È possibile creare un report collegato quando si desidera creare versioni aggiuntive di un report esistente. Un singolo report delle vendite regionali può essere utilizzato, ad esempio, per creare report specifici di una regione per tutti i territori di vendita.

 I report collegati sono in genere basati su report con parametri, sebbene questa condizione non costituisca un requisito. È possibile creare report collegati ogni volta che si desidera distribuire un report esistente con impostazioni diverse.

### <a name="to-create-a-linked-report"></a>Per creare un report collegato

1.  In Gestione report, passare alla cartella che contiene il report per il quale si vuole creare un collegamento, quindi aprire il menu delle opzioni e fare clic su **Crea report collegato**.

2.  Digitare un nome per il nuovo report collegato. Se lo si desidera, digitare una descrizione.

3.  Per selezionare una cartella diversa per il report, fare clic su **Cambia percorso**. Selezionare la cartella che si vuole usare o digitare il nome della cartella nella casella **Percorso** . 
  [!INCLUDE[clickOK](../../../includes/clickok-md.md)] Se non è stata selezionata una cartella diversa, il report collegato viene creato nella cartella corrente (dove è archiviato il report su cui si basa).

4.  
  [!INCLUDE[clickOK](../../../includes/clickok-md.md)] Verrà aperto il report collegato.

     L'icona di un report collegato è diversa da quella di altri elementi gestiti da un server di report. L'icona seguente indica un report collegato:

     ![Icona di report collegato](../media/hlp-16linked.gif "Icona di report collegato")

## <a name="see-also"></a>Vedere anche
 [Aprire e chiudere un report &#40;Gestione report&#41;](../reports/open-and-close-a-report-report-manager.md) [pagina nuovo report collegato &#40;Gestione report&#41;](../new-linked-report-page-report-manager.md) [scegliere la pagina percorso elemento &#40;](../choose-item-location-page-report-manager.md) Gestione report&#41;[pagina delle proprietà generale, report &#40;](../general-properties-page-reports-report-manager.md) Gestione report&#41;Reporting Services [concetti &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md) Gestione report &#40;[modalità nativa SSRS](../report-manager-ssrs-native-mode.md)&#41;


