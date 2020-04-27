---
title: Collegare un report a un modello come report click-through | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- customizing clickthrough reports
- clickthrough reports, customizing
- clickthrough reports, templates
ms.assetid: 3af42de3-67ef-41c2-bc8a-7045baec6f63
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 45b7695a9cd259d10155036ce1f9367a71e2fe72
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108364"
---
# <a name="link-a-report-to-a-model-as-a-clickthrough-report"></a>Collegare un report a un modello come report click-through
  Invece di utilizzare i modelli di report click-through predefiniti, è possibile creare un report con Generatore report e quindi collegarlo a un'entità specifica nel modello di report. Quando l'utente che visualizza il report fa clic sui dati interattivi nel report principale, questo report viene visualizzato come report click-through. Per collegare un report a un'entità, utilizzare Gestione report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  L'entità primaria, o di base, che viene utilizzata nel report deve coincidere con quella a cui il report è collegato.  
  
### <a name="to-start-report-manager-from-a-browser"></a>Per avviare Gestione report da un browser  
  
1.  Aprire [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 6.0 o versione successiva.  
  
2.  Nella barra degli indirizzi del browser digitare l'URL di Gestione report. Per impostazione predefinita, l'URL è\<http://*nomecomputer*>/Reports.  
  
### <a name="to-create-a-customized-clickthrough-report"></a>Per creare un report click-through personalizzato  
  
1.  Passare al modello di report al quale si desidera aggiungere il report click-through personalizzato.  
  
2.  Fare doppio clic sul modello di report.  
  
3.  Fare clic su **Click-through**.  
  
4.  Selezionare l'entità a cui associare il report click-through personalizzato.  
  
    > [!NOTE]  
    >  Questa entità deve corrispondere all'entità di base del report click-through personalizzato.  
  
5.  Per visualizzare il report personalizzato quando viene selezionata una singola istanza dell'entità scelta, fare clic sul pulsante **Sfoglia** del report a istanza singola.  
  
     -oppure-  
  
     Per visualizzare il report personalizzato quando vengono selezionate più istanze dell'entità scelta, fare clic sul pulsante **Sfoglia** del report a più istanze.  
  
6.  Selezionare il report, quindi fare clic su **OK**.  
  
7.  Fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedi anche  
 [Report click-through &#40;&#41;SSRS](reports/clickthrough-reports-ssrs.md)  
  
  
