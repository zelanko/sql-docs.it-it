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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1edcb27ac2be97919fb3d494b35afc1fab25c204
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756743"
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
 [Configurazione degli output tramite Configurazione guidata dimensioni a modifica lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
