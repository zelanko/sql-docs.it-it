---
title: Inizializzare una sottoscrizione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66ba96a96f95f91974f0a948db34c34ca0391f1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721117"
---
# <a name="initialize-a-subscription"></a>Inizializzazione di una sottoscrizione
  I Sottoscrittori in una topologia di replica devono essere inizializzati in modo da disporre di una copia dello schema di ogni articolo della pubblicazione per cui è stata effettuata la sottoscrizione e di tutti gli oggetti di replica necessari, quali stored procedure, trigger e tabelle di metadati. Il Sottoscrittore, inoltre, riceve in genere un set di dati iniziale. Con il metodo di inizializzazione predefinito è possibile utilizzare uno snapshot completo in cui sono inclusi lo schema, gli oggetti di replica e i dati. È tuttavia possibile inizializzare le pubblicazioni senza uno snapshot completo.  
  
 Per ulteriori informazioni, vedere [Initialize a Subscription with a Snapshot](initialize-a-subscription-with-a-snapshot.md) e [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
