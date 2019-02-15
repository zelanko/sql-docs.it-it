---
title: Eseguire il mapping di finestra di dialogo delle regole colore, generale | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10541"
- sql12.rtp.rptdesigner.shared.mapcolorrulesgeneral.f1
ms.assetid: 14ff5fc1-4cf8-4a45-9d98-47a1bf1c52c4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7c21f95a8ace66b502de7128711acc1d840c4147
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289669"
---
# <a name="map-color-rules-dialog-box-general"></a>Finestra di dialogo Proprietà regole colori mappa, Generale
  Selezionare **Generale** nella finestra di dialogo **Proprietà regole colori mappa** per definire le opzioni relative ai colori per gli elementi mappa di questo livello. Gli elementi della mappa includono poligoni, linee e punti. Le regole colore possono essere applicate quando è stata creata una relazione tra gli elementi della mappa in base ai dati spaziali e analitici di un campo del set di dati o di un campo dell'origine dati spaziali.  
  
 Per visualizzare tutti gli elementi della mappa su un livello specificando una sfumatura decorativa con colori primari e secondari diversi, utilizzare la pagina **Riempimento** della finestra di dialogo Proprietà poligono mappa. Le regole colore hanno la precedenza sulle proprietà di visualizzazione per un livello. Per altre informazioni, vedere [Personalizzare i dati e la visualizzazione di una mappa o di un livello mappa &#40;Generatore report e SSRS&#41;](report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opzioni  
 **Applica stile modello**  
 Selezionare questa opzione per utilizzare i colori in base al tema scelto nella procedura guidata o impostato nelle proprietà dei livelli Poligono, Linea o Punto. Un tema consente di impostare le opzioni predefinite per colore, carattere e bordi della mappa. Per questa opzione, non viene applicata nessuna regola per assegnare colori a ogni elemento della mappa.  
  
 **Visualizza dati tramite tavolozza dei colori**  
 Selezionare questa opzione per visualizzare i dati analitici tramite i colori di una specifica tavolozza.  
  
 **Visualizza dati tramite intervalli colori**  
 Selezionare questa opzione per visualizzare i dati analitici tramite un intervallo di colori per ogni elemento della mappa. Ad esempio se si specifica il rosso come colore iniziale, il giallo come colore intermedio e il verde come colore finale, i valori dell'intervallo inferiore sono rossi, i valori dell'intervallo intermedio sono gialli e i valori dell'intervallo superiore sono verdi.  
  
 **Visualizza dati tramite colori personalizzati**  
 Selezionare questa opzione per visualizzare i dati analitici specificando il proprio elenco di colori.  
  
 **Campo dati**  
 Questa opzione viene visualizzata quando si seleziona una delle **visualizzare i dati** opzioni.  
  
 Selezionare il campo dei dati analitici da utilizzare dall'elenco a discesa. A seconda dell'origine dati spaziali, l'elenco visualizza i campi dall'origine dati spaziali e da un set di dati del report che dispone di una relazione tra i dati spaziali e quelli analitici. Per creare tale relazione, impostare le opzioni dei dati nella pagina Dati analitici per il livello mappa selezionato.  
  
 **Tavolozza**  
 Digitare o selezionare il nome della tavolozza colori.  
  
 **Colore iniziale**  
 Specificare il colore da utilizzare per i dati nella parte inferiore dell'intervallo di dati.  
  
 **Colore intermedio**  
 Specificare il colore da utilizzare per i dati nella parte intermedia dell'intervallo di dati. Selezionare **Nessun colore** per rimuovere questo intervallo.  
  
 **Colore finale**  
 Specificare il colore da utilizzare per i dati nella parte superiore dell'intervallo di dati.  
  
 **Aggiungi**  
 Fare clic su **Add** per specificare i colori per la regola colore.  
  
## <a name="see-also"></a>Vedere anche  
 [Mappe &#40;Generatore report e SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)   
 [Modificare legende della mappa, scala dei colori e regole associate &#40;Generatore report e SSRS&#41;](report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)  
  
  
