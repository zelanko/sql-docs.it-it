---
title: Attivare e disattivare la finestra di dialogo di Writeback (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitiondesigner.writebackenabledisable.f1
ms.assetid: 2d254393-3f0d-4b70-8b98-87159f9f3639
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 498d1af6f96791b9ee3912c09a3667e139f30ff0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081291"
---
# <a name="enable-disable-writeback-dialog-box-analysis-services---multidimensional-data"></a>Attivare e disattivare la finestra di dialogo di Writeback (Analysis Services - dati multidimensionali)
  La finestra di dialogo **Enable/Disable Writeback** (Abilita/Disabilita writeback) attiva o disabilita il writeback per un gruppo di misure in un cubo. L'attivazione del writeback su un gruppo di misure definisce una partizione writeback e crea una tabella writeback per tale gruppo di misure. La disabilitazione del writeback su un gruppo di misure elimina la partizione writeback ma non la tabella writeback, per evitare una perdita imprevista di dati. La finestra di dialogo **Enable/Disable Writeback** (Abilita/Disabilita writeback) può essere visualizzata nei modi seguenti:  
  
-   Facendo clic su **Impostazioni writeback** nel riquadro **Gruppi di misure** della scheda **Partizioni** in Progettazione cubi.  
  
-   Facendo clic con il pulsante destro del mouse su una partizione nella griglia **Partizioni** nel riquadro **Gruppi di misure** della scheda **Partizioni** in Progettazione cubi e scegliendo **Impostazioni writeback** dal menu di scelta rapida.  
  
## <a name="options"></a>Opzioni  
 **Nome tabella**  
 Consente di digitare il nome della tabella writeback da creare per la partizione selezionata. La tabella di writeback archivia le modifiche apportate al gruppo di misure da un’applicazione client.  
  
> [!NOTE]  
>  Se il writeback non è abilitato questa opzione non è disponibile.  
  
 **Origine dati**  
 Consente di selezionare l'origine dei dati che deve contenere la tabella writeback.  
  
> [!NOTE]  
>  Se il writeback non è abilitato questa opzione non è disponibile.  
  
 **Nuova**  
 Fare clic su questo pulsante per visualizzare la finestra di dialogo **Gestione connessione** e definire una nuova origine dei dati che deve contenere la tabella writeback.  
  
> [!NOTE]  
>  Se il writeback non è abilitato questa opzione non è disponibile.  
  
  
