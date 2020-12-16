---
description: Inizializzazione di una sottoscrizione
title: Inizializzare una sottoscrizione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: aafcf9b2e19fbf515fcd0df7bc6981f828a26502
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479902"
---
# <a name="initialize-a-subscription"></a>Inizializzazione di una sottoscrizione
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  I Sottoscrittori in una topologia di replica devono essere inizializzati in modo da disporre di una copia dello schema di ogni articolo della pubblicazione per cui è stata effettuata la sottoscrizione e di tutti gli oggetti di replica necessari, quali stored procedure, trigger e tabelle di metadati. Il Sottoscrittore, inoltre, riceve in genere un set di dati iniziale. Con il metodo di inizializzazione predefinito è possibile utilizzare uno snapshot completo in cui sono inclusi lo schema, gli oggetti di replica e i dati. È tuttavia possibile inizializzare le pubblicazioni senza uno snapshot completo.  
  
 Per ulteriori informazioni, vedere [Initialize a Subscription with a Snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) e [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
