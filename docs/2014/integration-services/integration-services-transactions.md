---
title: Transazioni di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0359ca10e7279f4a80bec082a8e049f4641c9b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767633"
---
# <a name="integration-services-transactions"></a>Transazioni di Integration Services
  Nei pacchetti vengono utilizzate transazioni per l'associazione di azioni del database eseguite dalle attività in unità atomiche in modo da mantenere l'integrità dei dati. Tutti [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] i tipi di contenitori, ovvero pacchetti, ciclo for, ciclo foreach, contenitori sequenza e gli host attività che incapsulano ogni attività, possono essere configurati per l'utilizzo di transazioni. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]in sono disponibili tre opzioni per la configurazione delle transazioni: **NotSupported**, **supported**e **required**.  
  
-   **Required** indica che il contenitore avvia una transazione, a meno che non ne sia già stata avviata una dal contenitore padre. In questo caso, il contenitore parteciperà alla transazione in corso. Si supponga, ad esempio, che un pacchetto includa un contenitore Sequenza con l'opzione **Required**. Se il pacchetto non è stato configurato per il supporto di transazioni, il contenitore avvierà la propria transazione. Se per il pacchetto è stata impostata l'opzione **Required**, il contenitore Sequenza parteciperà alla transazione del pacchetto.  
  
-   **Supportato** indica che il contenitore non avvia una transazione, ma unisce qualsiasi transazione avviata dal contenitore padre. Si supponga, ad esempio, che un pacchetto includa quattro attività Esegui SQL con l'opzione **Supported** e che il pacchetto avvii una transazione. In questo caso, se una delle attività Esegui SQL ha esito negativo viene eseguito il rollback degli aggiornamenti del database eseguiti dalle attività. Nel caso di un pacchetto che non avvia una transazione, le quattro attività Esegui SQL risultano non associate ad alcuna transazione. Di conseguenza viene eseguito il rollback solo degli aggiornamenti del database eseguiti dall'attività che ha esito negativo.  
  
-   **NotSupported** indica che il contenitore non avvia una transazione né partecipa a una transazione esistente. Una transazione avviata da un contenitore padre non ha alcun effetto sui contenitori figlio non configurati per il supporto di transazioni. Si supponga, ad esempio, che un pacchetto sia configurato per l'avvio di una transazione e che per un contenitore Ciclo For del pacchetto sia impostata l'opzione **NotSupported**. In questo caso, se le attività del Ciclo For hanno esito negativo non è possibile eseguire il rollback di nessuna attività.  
  
 Per configurare le transazioni, è necessario impostare la proprietà TransactionOption del contenitore. È possibile eseguire questa operazione nella finestra **Proprietà** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] o a livello di codice.  
  
> [!NOTE]  
>  La proprietà `TransactionOption` può determinare se il valore della proprietà `IsolationLevel` richiesta da un contenitore viene applicato o meno. Per ulteriori informazioni, vedere la descrizione della `IsolationLevel` proprietà nell'argomento impostazione delle proprietà di un [pacchetto](set-package-properties.md).  
  
### <a name="to-configure-a-package-to-use-transactions"></a>Per configurare un pacchetto per l'utilizzo di transazioni  
  
-   [Configurazione di un pacchetto per l'utilizzo di transazioni](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Intervento nel blog [How to Use Transactions in SQL Server Integration Services SSIS](https://go.microsoft.com/fwlink/?LinkId=157783) sul sito Web all'indirizzo www.mssqltips.com  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni ereditate](../../2014/integration-services/inherited-transactions.md)   
 [Più transazioni](../../2014/integration-services/multiple-transactions.md)  
  
  
