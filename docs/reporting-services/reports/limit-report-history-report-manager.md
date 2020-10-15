---
title: Limitare la cronologia dei report - Reporting Services | Microsoft Docs
description: Informazioni su come configurare la cronologia del report per un server di report. Scoprire anche come configurare la cronologia per un report specifico.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
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
ms.openlocfilehash: 809d11c82a9b09a23590592ec3f7b433e3c9ca43
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986657"
---
# <a name="limit-report-history---reporting-services"></a>Limitare la cronologia dei report - Reporting Services
  La cronologia di un report è una raccolta di snapshot del report creati nel tempo. È possibile creare la cronologia del report su richiesta o pianificare la frequenza di creazione di uno snapshot e della relativa aggiunta alla cronologia.  
  
 La cronologia del report viene archiviata nel database del server di report. Se gli snapshot del report contengono una quantità di dati elevata, è possibile limitare la cronologia del report per ridurre al minimo l'impatto della conservazione degli snapshot sulle dimensioni del database.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-history-for-a-report-server"></a>Per configurare la cronologia del report per un server di report  
  
1.  In Gestione report fare clic su **Impostazioni sito** sulla barra degli strumenti principale.  
  
2.  Selezionare **Nessun limite per il numero di snapshot archiviabili nella cronologia** se si desidera mantenere tutta la cronologia del report per un periodo illimitato. In alternativa, selezionare **Numero massimo di copie della cronologia** per specificare il numero massimo di snapshot che è possibile mantenere per qualsiasi report.  
  
3.  Fare clic su **Applica**.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>Per configurare la cronologia per un report specifico  
  
1.  In Gestione report passare al report per il quale si desidera configurare la cronologia e quindi fare clic su di esso per aprirlo.  
  
2.  Fare clic sulla scheda **Proprietà**.  
  
3.  Fare clic sulla scheda **Cronologia** .  
  
4.  Selezionare le opzioni per il report e fare clic su **Applica**. Per informazioni dettagliate su ogni opzione, vedere [Pagina delle proprietà Opzioni snapshot &#40;Gestione report&#41;](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130)).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere uno snapshot alla cronologia del report &#40;Gestione report&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../web-portal-ssrs-native-mode.md)  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="to-configure-report-history-for-a-report-server"></a>Per configurare la cronologia del report per un server di report  
  
1.  Nel portale Web fare clic su **Impostazioni sito** nella barra degli strumenti globale.  
  
2.  Selezionare **Nessun limite per il numero di snapshot archiviabili nella cronologia** se si desidera mantenere tutta la cronologia del report per un periodo illimitato. In alternativa, selezionare **Numero massimo di copie della cronologia** per specificare il numero massimo di snapshot che è possibile mantenere per qualsiasi report.  
  
3.  Fare clic su **Applica**.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>Per configurare la cronologia per un report specifico  
  
1.  Nel portale Web passare al report per il quale si vuole configurare la cronologia, quindi farci clic sopra per aprirlo.  
  
2.  Fare clic sulla scheda **Proprietà**.  
  
3.  Fare clic sulla scheda **Cronologia** .  
  
4.  Selezionare le opzioni per il report e fare clic su **Applica**. Per informazioni dettagliate su ogni opzione, vedere [Pagina delle proprietà Opzioni snapshot](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130)).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere uno snapshot alla cronologia del report](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   

::: moniker-end
