---
title: Opzioni di convalida delle sottoscrizioni (sottoscrizioni transazionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a82e13202209121897a5e5878a141c8d53800a47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62745422"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>Opzioni di convalida delle sottoscrizioni (sottoscrizioni transazionali)
  Utilizzare la finestra di dialogo **Opzioni di convalida delle sottoscrizioni** per specificare se la convalida deve utilizzare solo un conteggio di righe o un conteggio di righe e un checksum binario.  
  
## <a name="options"></a>Opzioni  
 **Verificare che il Sottoscrittore abbia lo stesso numero di righe di dati replicati del server di pubblicazione**  
 Consente di selezionare il tipo di convalida del conteggio di righe da eseguire. Per le pubblicazioni Oracle, l'unica opzione disponibile è **Esegui il conteggio di righe effettivo tramite una query diretta nelle tabelle**.  
  
 **Confrontare i checksum per verificare i dati delle righe**  
 Oltre al conteggio delle righe nel server di pubblicazione e nel Sottoscrittore, viene calcolato un checksum di tutti i dati utilizzando l'algoritmo di checksum binario. In caso di esito negativo durante il conteggio delle righe il checksum non viene eseguito.  
  
 **Arresta il agente di distribuzione al termine della convalida**  
 Per impostazione predefinita, l'agente di distribuzione viene eseguito in modo continuativo. Selezionare questa opzione per arrestare l'agente dopo l'esecuzione della convalida. In tal modo è possibile controllare se la convalida è riuscita prima di continuare la replica dei dati nel Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalida dei dati nel Sottoscrittore](validate-data-at-the-subscriber.md)   
 [Convalidare i dati replicati](validate-data-at-the-subscriber.md)  
  
  
