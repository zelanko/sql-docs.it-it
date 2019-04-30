---
title: Convalida tutte le sottoscrizioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.allsubscriptions.f1
helpviewer_keywords:
- Validate All Subscriptions dialog box
ms.assetid: 32e31469-36e4-42d9-a57a-12388bfd229d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b33cfe47cebba4c24c90ad41ce1b218192d128f4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63255331"
---
# <a name="validate-all-subscriptions"></a>Convalida tutte le sottoscrizioni
  Utilizzare la finestra di dialogo **Convalida tutte le sottoscrizioni** per specificare che tutte le sottoscrizioni di una pubblicazione di tipo merge devono essere convalidate all'esecuzione successiva dell'agente di merge per ogni sottoscrizione. I risultati della convalida vengono visualizzati in Monitoraggio replica. Per altre informazioni, vedere [Validate Data at the Subscriber](validate-data-at-the-subscriber.md).  
  
 È inoltre possibile convalidare una singola sottoscrizione facendo clic con il pulsante destro del mouse su una sottoscrizione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , quindi scegliendo **Convalida sottoscrizione**.  
  
## <a name="options"></a>Opzioni  
 **Verifica solo il conteggio delle righe**  
 Consente di verificare che la tabella nel Sottoscrittore abbia lo stesso numero di righe della tabella nel server di pubblicazione. Questa opzione non convalida la corrispondenza del contenuto delle righe. La convalida del conteggio delle righe è un controllo non approfondito che consente comunque di evidenziare eventuali problemi dei dati.  
  
 **Verifica il conteggio delle righe e confronta i valori di checksum per la verifica dei dati delle righe**  
 Oltre al conteggio delle righe nel server di pubblicazione e nel Sottoscrittore, viene calcolato un checksum di tutti i dati utilizzando l'algoritmo di checksum binario. In caso di esito negativo durante il conteggio delle righe il checksum non viene eseguito. Questa opzione non è valida per [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare i dati replicati](validate-data-at-the-subscriber.md)  
  
  
