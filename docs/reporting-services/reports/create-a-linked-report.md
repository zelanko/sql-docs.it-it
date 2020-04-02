---
title: Creare un report collegato | Microsoft Docs
description: Informazioni su come creare un report collegato in modo da poter creare versioni aggiuntive di un report esistente.
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cb362f699e8bf87e0f386c3ec726869f67aec934
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79510162"
---
# <a name="create-a-linked-report"></a>Creare un report collegato
  Un report collegato è un elemento del server di report che fornisce un punto di accesso a un report esistente. Tale elemento è concettualmente simile al collegamento a un programma utilizzato per l'esecuzione di un programma o per l'apertura di un file.  
  
 Un report collegato viene derivato da un report esistente e mantiene la definizione del report originale. Un report collegato, inoltre, eredita sempre il layout del report e le proprietà dell'origine dati del report originale. Tutte le altre proprietà e impostazioni, ad esempio sicurezza, parametri, percorso, sottoscrizioni e pianificazioni, possono essere diverse da quelle del report originale.  
  
 È possibile creare un report collegato quando si desidera creare versioni aggiuntive di un report esistente. Un singolo report delle vendite regionali può essere utilizzato, ad esempio, per creare report specifici di una regione per tutti i territori di vendita.  
  
 I report collegati sono in genere basati su report con parametri, sebbene questa condizione non costituisca un requisito. È possibile creare report collegati ogni volta che si desidera distribuire un report esistente con impostazioni diverse.  
  
## <a name="to-create-a-linked-report"></a>Per creare un report collegato  
  
1. Nel portale Web passare al report desiderato, fare clic con il pulsante destro del mouse su di esso e scegliere **Gestisci** dal menu a discesa.

2. Nella pagina **Gestisci <reportname>** selezionare **Crea report collegato**.  
  
3. Immettere un nome per il nuovo report collegato. Immettere facoltativamente una descrizione.  
  
4. Per selezionare una cartella diversa per il report, selezionare pulsante con i puntini di sospensione (...) a destra di ***Percorso***.  Passare alla nuova cartella per il report e selezionare **Seleziona**. Se non è stata selezionata una cartella diversa, il report collegato viene creato nella cartella corrente.  
  
5. Selezionare **Create** (Crea). Verrà creato il report collegato.  

6. In **Avanzate** selezionare un valore **Timeout report** diverso, se desiderato, e selezionare **Applica** per salvare le modifiche.
  
     L'icona di un report collegato è diversa da quella di altri elementi gestiti da un server di report. L'icona seguente indica un report collegato:  
  
     ![Icona di report collegato](../../reporting-services/report-server/media/hlp-16linked.gif "Icona di report collegato")  
  
## <a name="see-also"></a>Vedere anche  

 [Concetti relativi a Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)  
 [Portale Web di un server di report (modalità nativa SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)
  
