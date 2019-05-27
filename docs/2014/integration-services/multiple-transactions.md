---
title: Più transazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], multiple
- multiple transactions
ms.assetid: c3664a94-be89-40c0-a3a0-84b74a7fedbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da0f932acb2ab97204aeb27c9e077c7fae154987
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057403"
---
# <a name="multiple-transactions"></a>Più transazioni
  Un pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] potrebbe includere transazioni non correlate. Quando un contenitore all'interno di una gerarchia di contenitori nidificati non supporta le transazioni, i contenitori di livello superiore o inferiore nella gerarchia avviano transazioni distinte se sono configurati per il supporto di transazioni. Viene quindi eseguito il commit o il rollback delle transazioni a partire dall'attività più interna della gerarchia fino al livello del pacchetto. Dopo il commit della transazione più interna, tuttavia, viene eseguito il rollback solo in caso di interruzione di una transazione esterna.  
  
## <a name="illustration-of-multiple-transactions"></a>Illustrazione di più transazioni  
 Si supponga, ad esempio, che un pacchetto includa un contenitore Sequenza con due contenitori Ciclo Foreach ognuno dei quali include due attività Esegui SQL. A differenza del contenitore Sequenza e delle attività Esegui SQL, i contenitori Ciclo Foreach non supportano transazioni. In questo esempio, ogni attività Esegui SQL avvia la propria transazione e non viene eseguito il rollback in caso di interruzione della transazione nell'attività Sequenza.  
  
 Le proprietà TransactionOption del contenitore Sequenza, del contenitore Ciclo Foreach e delle attività Esegui SQL vengono impostate nel modo seguente:  
  
-   La proprietà TransactionOption del contenitore Sequenza viene impostata su **Required**.  
  
-   La proprietà TransactionOption dei contenitori Ciclo Foreach viene impostata su **NotSupported**.  
  
-   La proprietà TransactionOption dell'attività Esegui SQL viene impostata su **Required**.  
  
 Nella figura seguente vengono illustrate le cinque transazioni non correlate del pacchetto. Una transazione viene avviata nel contenitore Sequenza e le altre quattro vengono avviate dalle attività Esegui SQL.  
  
 ![Implementazione di più transazioni](media/mw-dts-trans2.gif "Implementazione di più transazioni")  
  
## <a name="related-tasks"></a>Attività correlate  
 [Configurazione di un pacchetto per l'utilizzo di transazioni](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
