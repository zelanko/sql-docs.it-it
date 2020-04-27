---
title: Configurare l'accesso in memoria o DirectQuery per un database modello tabulare | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55a1a296e6a7b2a2155dea590be9321b22e73451
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66067188"
---
# <a name="configure-in-memory-or-directquery-access-for-a-tabular-model-database"></a>Configurare l'accesso in memoria o DirectQuery per un database di modello tabulare
  In questo argomento viene illustrato come modificare le proprietà di connessione di un modello tabulare che è già stato distribuito, per consentire l'utilizzo del modello in modalità DirectQuery.  
  
 Per altre informazioni su queste proprietà e sulla configurazione per gli scenari più comuni, vedere [scenari di distribuzione DirectQuery &#40;SSAS tabulare&#41;](../directquery-deployment-scenarios-ssas-tabular.md).  
  
## <a name="requirements"></a>Requisiti  
 L'abilitazione dell'utilizzo della modalità DirectQuery su un modello tabulare è un processo a più passaggi. È necessario:  
  
1.  Verificare che il modello non disponga di funzionalità che potrebbero provocare errori di convalida in modalità DirectQuery.  
  
2.  Modificare la modalità di archiviazione del modello per supportare DirectQuery.  
  
3.  Distribuire il modello in una modalità che supporti le query in modalità DirectQuery pura o ibrida.  
  
4.  Modificare la stringa di connessione nel database distribuito per supportare la modalità DirectQuery.  
  
 In questo argomento si presuppone che sia stato creato e convalidato il modello e che occorra soltanto abilitare l'accesso DirectQuery da un client quale [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
## <a name="procedure"></a>Procedura  
  
#### <a name="change-the-connection-string-properties-of-the-model"></a>Modificare le proprietà della stringa di connessione del modello  
  
1.  In SQL Server Management Studio aprire l'istanza in cui distribuire il modello.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nome del database modello e scegliere **Proprietà**.  
  
3.  Individuare la proprietà **DirectQueryMode**. Per abilitare l'utilizzo dell'origine dati relazionale, è necessario impostare questa proprietà su uno dei valori seguenti:  
  
    -   **DirectQuery**  
  
    -   **InMemoryWithDirectQuery**  
  
    -   **DirectQueryWithInMemory**  
  
  
