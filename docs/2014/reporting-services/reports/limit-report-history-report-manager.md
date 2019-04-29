---
title: Limitare la cronologia dei report (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe038f264a1bf748414715b0f51a32c5f14531bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63012249"
---
# <a name="limit-report-history-report-manager"></a>Limitare la cronologia dei report (Gestione report)
  La cronologia di un report è una raccolta di snapshot del report creati nel tempo. È possibile creare la cronologia del report su richiesta o pianificare la frequenza di creazione di uno snapshot e della relativa aggiunta alla cronologia.  
  
 La cronologia del report viene archiviata nel database del server di report. Se gli snapshot del report contengono una quantità di dati elevata, è possibile limitare la cronologia del report per minimizzare l'impatto della memorizzazione degli snapshot sulle dimensione del database.  
  
### <a name="to-configure-report-history-for-a-report-server"></a>Per configurare la cronologia del report per un server di report  
  
1.  In Gestione report fare clic su **Impostazioni sito** sulla barra degli strumenti principale.  
  
2.  Selezionare **Nessun limite per il numero di snapshot archiviabili nella cronologia** se si desidera mantenere tutta la cronologia del report per un periodo illimitato. In alternativa, selezionare **Numero massimo di copie della cronologia** per specificare il numero massimo di snapshot che è possibile mantenere per qualsiasi report.  
  
3.  Fare clic su **Applica**.  
  
### <a name="to-configure-report-history-for-a-specific-report"></a>Per configurare la cronologia per un report specifico  
  
1.  In Gestione report passare al report per il quale si desidera configurare la cronologia e quindi fare clic su di esso per aprirlo.  
  
2.  Fare clic sulla scheda **Proprietà** .  
  
3.  Fare clic sulla scheda **Cronologia** .  
  
4.  Selezionare le opzioni per il report e fare clic su **Applica**. Per informazioni dettagliate su ogni opzione, vedere [Pagina delle proprietà Opzioni snapshot &#40;Gestione report&#41;](../snapshot-options-properties-page-report-manager.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere uno snapshot alla cronologia del report &#40;Gestione report&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)  
  
  
