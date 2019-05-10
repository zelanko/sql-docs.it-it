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
ms.openlocfilehash: 08ead4185051ad90f53e904b55e541e9bb2edd2f
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489578"
---
# <a name="task-9-configuring-a-reference-data-service"></a>Attività 9: Configurazione di un servizio dati di riferimento
  In questa attività viene configurato DQS per l'utilizzo del servizio dati di riferimento in Windows Azure Marketplace. Nell'attività successiva, si configurerà il **Address Validation** dominio per usare questo servizio. In fase di esecuzione durante l'attività di pulizia, DQS passa i valori dei domini nel **Address Validation** dominio al servizio per la pulizia. Visualizzare [Configure DQS to Use Reference Data](https://msdn.microsoft.com/library/hh213070.aspx) per altri dettagli.  
  
1.  Nella pagina principale del **Client DQS**, nella **amministrazione** riquadro, fare clic su **configurazione**.  
  
2.  Assicurarsi che **i dati di riferimento** scheda è attiva.  
  
3.  Nel **le impostazioni di rete** area, digitare i valori appropriati nel **Server Proxy** e **porta** campi se è necessario usare un server proxy per connettersi a Internet.  
  
4.  Tipo di **chiave di Account di Windows Azure Marketplace** per il **ID Account DataMarket** campo.  
  
     ![Account del servizio dati riferimento dati Azure Market](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Account del servizio dati riferimento mercato dei dati di Azure")  
  
5.  Fare clic su **Validate** pulsante accanto alla casella di testo per convalidare l'ID dell'account.  
  
6.  Fare clic su **OK** nella finestra di messaggio.  
  
7.  Fare clic su **Chiudi** nella parte inferiore della pagina per passare alla pagina principale del Client DQS.  
  
## <a name="next-task"></a>Attività successiva  
 [Attività 10: Configurazione del dominio composito per utilizzare il servizio dati di riferimento](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
