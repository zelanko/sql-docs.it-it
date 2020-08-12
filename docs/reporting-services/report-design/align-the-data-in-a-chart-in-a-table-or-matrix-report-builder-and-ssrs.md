---
title: Allineare i dati in un grafico in una tabella o matrice (Generatore report) | Microsoft Docs
description: Informazioni sull'uso dei grafici sparkline e delle barre dei dati in Generatore report. Questi piccoli, semplici grafici comunicano numerose informazioni con la quantità minima di dettagli.
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 30b2c4ad2bb1c4c4a6254d5563ab547b11c3f52c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84994571"
---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>Allineare i dati in un grafico di una tabella o matrice (Generatore report e SSRS)
  I grafici sparkline e le barre dei dati sono grafici semplici, di piccole dimensioni, contenenti numerose informazioni poco dettagliate. In un report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , quando si seleziona questa opzione, i valori presenti nei grafici sparkline e nelle barre dei dati vengono allineati nelle diverse celle della tabella o della matrice, anche se mancano dei valori nei dati su cui si basano.  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 In questa immagine, nell'istogramma vengono mostrate le vendite giornaliere per ogni dipendente. Nei giorni in cui il dipendente non ha effettuato vendite, nel grafico viene lasciato uno spazio vuoto, mentre i giorni successivi vengono allineati orizzontalmente. I grafici vengono inoltre allineati verticalmente mettendone in relazione le diverse dimensioni. Per altre informazioni, vedere [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="align-the-data-in-a-sparkline-or-data-bar"></a>Allineare i dati in un grafico sparkline o in una barra dei dati  
  
1.  [Aggiungere grafici sparkline o barre dei dati](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) a una tabella o a una matrice.  
  
2. Fare clic nel grafico sparkline o barra dei dati, quindi selezionare **Proprietà asse orizzontale** o **Proprietà asse verticale**.  
  
2.  Nella scheda **Opzioni asse** selezionare la casella **Align axes in** (Allinea assi in), quindi nella casella a discesa selezionare il gruppo sul quale allineare l'asse.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Aggiungere grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
