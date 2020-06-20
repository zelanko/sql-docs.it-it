---
title: Opzioni attributi fissi e modificabili (Configurazione guidata dimensioni a modifica lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9e9e18d251335ea10721fa1d159d63530d973581
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939522"
---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>Opzioni attributi fissi e modificabili (Configurazione guidata dimensioni a modifica lenta)
  Utilizzare la finestra di dialogo **Opzioni attributi fissi e modificabili** per specificare le modalità di risposta alle modifiche degli attributi fissi e modificabili.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Attributi fissi**  
 Per gli attributi fissi, consente di indicare se l'attività deve essere interrotta in caso venga rilevata una modifica a un attributo fisso.  
  
 **Attributi modificabili**  
 Per gli attributi modificabili, consente di indicare se l'attività deve modificare i record obsoleti o scaduti oltre ai record correnti, in caso venga rilevata una modifica a un attributo modificabile. Per record scaduto si intende un record che è stato sostituito con un record più recente mediante una modifica in un attributo cronologico (una modifica di tipo 2). Se si seleziona questa opzione, è possibile che vengano imposti ulteriori requisiti di elaborazione in un oggetto multidimensionale costruito sul data warehouse relazionale.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli output tramite Configurazione guidata dimensioni a modifica lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
