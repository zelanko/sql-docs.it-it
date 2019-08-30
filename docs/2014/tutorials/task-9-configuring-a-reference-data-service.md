---
title: 'Attività 9: Configurazione di un servizio dati di riferimento | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e4c756463c43ede8c6dae0cda0a184f0ec7f9956
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154936"
---
# <a name="task-9-configuring-a-reference-data-service"></a>Attività 9: Configurazione di un servizio dati di riferimento
  In questa attività viene configurato DQS per l'utilizzo di un servizio dati di riferimento in Azure Marketplace. Nell'attività successiva verrà configurato il dominio di **convalida degli indirizzi** per l'utilizzo di questo servizio. In fase di esecuzione, durante l'attività di pulizia, DQS passa i valori dei domini nel dominio di **convalida degli indirizzi** al servizio per la pulizia. Per altri dettagli, vedere [configurare DQS per l'uso dei dati di riferimento](https://msdn.microsoft.com/library/hh213070.aspx) .  
  
1.  Nella pagina principale del **client DQS**, nel riquadro **Amministrazione** , fare clic su **configurazione**.  
  
2.  Verificare che la scheda **dati di riferimento** sia attiva.  
  
3.  Nell'area **impostazioni di rete** Digitare i valori appropriati nei campi **server proxy** e **porta** se è necessario usare un server proxy per la connessione a Internet.  
  
4.  Digitare la **chiave dell'account di Azure Marketplace** per il campo **ID account DataMarket** .  
  
     ![Account del servizio dati di riferimento di Azure Data Market](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Account del servizio dati di riferimento di Azure Data Market")  
  
5.  Fare clic sul pulsante **convalida** accanto alla casella di testo per convalidare l'ID account.  
  
6.  Fare clic su **OK** nella finestra di messaggio.  
  
7.  Fare clic su **Chiudi** nella parte inferiore della pagina per passare alla pagina principale del client DQS.  
  
## <a name="next-task"></a>Attività successiva  
 [Attività 10: Configurazione del dominio composito per l'utilizzo del servizio dati di riferimento](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
