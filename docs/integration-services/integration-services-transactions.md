---
title: Transazioni di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 90855baaa61e242488a7fb6a91a52e34d77e5f48
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284406"
---
# <a name="integration-services-transactions"></a>Transazioni di Integration Services

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Nei pacchetti vengono utilizzate transazioni per l'associazione di azioni del database eseguite dalle attività in unità atomiche in modo da mantenere l'integrità dei dati. Tutti i tipi di contenitori di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], ovvero pacchetti, ciclo For, ciclo Foreach, contenitori Sequenza, nonché gli host di attività in cui è incapsulata ogni attività, possono essere configurati per l'uso delle transazioni. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include tre opzioni per la configurazione delle transazioni: **NotSupported**, **Supported** e **Required**.  
  
-   L'opzione**Required** indica che il contenitore avvia una transazione, a meno che il contenitore padre non abbia già avviato un'altra transazione. In questo caso, il contenitore parteciperà alla transazione in corso. Si supponga, ad esempio, che un pacchetto includa un contenitore Sequenza con l'opzione **Required** . Se il pacchetto non è stato configurato per il supporto di transazioni, il contenitore avvierà la propria transazione. Se per il pacchetto è stata impostata l'opzione **Required** , il contenitore Sequenza parteciperà alla transazione del pacchetto.  
  
-   L'opzione**Supported** indica che il contenitore non avvia una transazione, ma partecipa alla transazione avviata dal contenitore padre. Si supponga, ad esempio, che un pacchetto includa quattro attività Esegui SQL con l'opzione **Supported** e che il pacchetto avvii una transazione. In questo caso, se una delle attività Esegui SQL ha esito negativo viene eseguito il rollback degli aggiornamenti del database eseguiti dalle attività. Nel caso di un pacchetto che non avvia una transazione, le quattro attività Esegui SQL risultano non associate ad alcuna transazione. Di conseguenza viene eseguito il rollback solo degli aggiornamenti del database eseguiti dall'attività che ha esito negativo.  
  
-   L'opzione**NotSupported** indica che il contenitore non avvia una transazione e non partecipa ad una transazione in corso. Una transazione avviata da un contenitore padre non ha alcun effetto sui contenitori figlio non configurati per il supporto di transazioni. Si supponga, ad esempio, che un pacchetto sia configurato per l'avvio di una transazione e che per un contenitore Ciclo For del pacchetto sia impostata l'opzione **NotSupported** . In questo caso, se le attività del Ciclo For hanno esito negativo non è possibile eseguire il rollback di nessuna attività.  
  
 Per configurare le transazioni, è necessario impostare la proprietà TransactionOption del contenitore. È possibile eseguire questa operazione nella finestra **Proprietà** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]o a livello di codice.  
  
> [!NOTE]  
>  La proprietà **TransactionOption** può determinare se il valore della proprietà **IsolationLevel** richiesta da un contenitore viene applicato o meno. Per altre informazioni, vedere la descrizione della proprietà **IsolationLevel** nell'argomento [Impostazione delle proprietà di un pacchetto](../integration-services/set-package-properties.md).  
  
## <a name="configure-a-package-to-use-transactions"></a>Configurazione di un pacchetto per l'utilizzo di transazioni
Quando si configura un pacchetto per l'utilizzo di transazioni, sono disponibili due opzioni:  
  
-   Utilizzare una sola transazione per il pacchetto. In questo caso, è il pacchetto stesso che *inizializza* questa transazione, mentre le singole attività e i contenitori del pacchetto partecipano a questa unica transazione.  
  
-   Utilizzare più transazioni nel pacchetto. In questo caso, il pacchetto supporta le transazioni, ma sono le singole attività e i contenitori del pacchetto a inizializzare le transazioni.  
  
 Nelle procedure seguenti viene descritto come configurare entrambe le opzioni.  
  
### <a name="configure-a-package-to-use-a-single-transaction"></a>Configurare un pacchetto per l'uso di una transazione singola  
 In questo caso, il pacchetto stesso inizializza un'unica transazione. È necessario configurare il pacchetto in modo che inizializzi questa transazione impostando la proprietà TransactionOption del pacchetto su **Required**.  
  
 In questa unica transazione verranno quindi inserite le attività e i contenitori specifici. Per inserire un'attività o un contenitore in una transazione, è necessario impostare la proprietà TransactionOption dell'attività o del contenitore su **Supported**.  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto che si desidera configurare per l'utilizzo di una transazione.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di controllo, quindi scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** impostare la proprietà TransactionOption su **Required**.  
  
6.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse sull'attività o il contenitore che si vuole integrare nella transazione e quindi scegliere **Proprietà**.  
  
7.  Nella finestra **Proprietà** impostare la proprietà TransactionOption su **Supported**.  
  
    > [!NOTE]  
    >  Per integrare una connessione in una transazione, integrare nella transazione le attività che la utilizzano. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
8.  Ripetere i passaggi 6 e 7 per ogni attività e ogni contenitore che si desidera registrare nella transazione.  
  
### <a name="configure-a-package-to-use-multiple-transactions"></a>Per configurare un pacchetto per l'uso di più transazioni  
 In questo caso, il pacchetto supporta le transazioni ma non ne avvia alcuna. È necessario configurare il pacchetto in modo che supporti le transazioni impostando la proprietà TransactionOption del pacchetto su **Supported**.  
  
 Configurare quindi le attività e i contenitori desiderati all'interno del pacchetto in modo che inizializzino la transazione o vengano eseguiti con essa. Per configurare un'attività o un contenitore in modo che inizializzi una transazione, è necessario impostare la proprietà TransactionOption dell'attività o del contenitore su **Required**.   
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto che si desidera configurare per l'utilizzo delle transazioni.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di controllo e quindi scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** impostare la proprietà TransactionOption su **Supported**.  
  
    > [!NOTE]  
    >  Il pacchetto supporta le transazioni, ma le transazioni vengono avviate da attività o contenitori nel pacchetto.  
  
6.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse sull'attività o il contenitore del pacchetto per il quale si vuole avviare una transazione e quindi scegliere **Proprietà**.  
  
7.  Nella finestra **Proprietà** impostare la proprietà TransactionOption su **Required**.  
  
8.  Se la transazione viene avviata da un contenitore, fare clic con il pulsante destro del mouse sull'attività o il contenitore che si vuole includere nella transazione e quindi scegliere **Proprietà**.  
  
9. Nella finestra **Proprietà** impostare la proprietà TransactionOption su **Supported**.  
  
    > [!NOTE]  
    >  Per integrare una connessione in una transazione, integrare nella transazione le attività che la utilizzano. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
10. Ripetere i passaggi da 6 a 9 per ogni attività e ogni contenitore che avvierà una transazione.  

## <a name="multiple-transactions-in-a-package"></a>Più transazioni in un pacchetto
Un pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] potrebbe includere transazioni non correlate. Quando un contenitore all'interno di una gerarchia di contenitori nidificati non supporta le transazioni, i contenitori di livello superiore o inferiore nella gerarchia avviano transazioni distinte se sono configurati per il supporto di transazioni. Viene quindi eseguito il commit o il rollback delle transazioni a partire dall'attività più interna della gerarchia fino al livello del pacchetto. Dopo il commit della transazione più interna, tuttavia, viene eseguito il rollback solo in caso di interruzione di una transazione esterna.  
  
### <a name="example-of-multiple-transactions-in-a-package"></a>Esempio di più transazioni in un pacchetto 
 Si supponga, ad esempio, che un pacchetto includa un contenitore Sequenza con due contenitori Ciclo Foreach ognuno dei quali include due attività Esegui SQL. A differenza del contenitore Sequenza e delle attività Esegui SQL, i contenitori Ciclo Foreach non supportano transazioni. In questo esempio, ogni attività Esegui SQL avvia la propria transazione e non viene eseguito il rollback in caso di interruzione della transazione nell'attività Sequenza.  
  
 Le proprietà TransactionOption del contenitore Sequenza, del contenitore Ciclo Foreach e delle attività Esegui SQL vengono impostate nel modo seguente:  
  
-   La proprietà TransactionOption del contenitore Sequenza viene impostata su **Required**.  
  
-   La proprietà TransactionOption dei contenitori Ciclo Foreach viene impostata su **NotSupported**.  
  
-   La proprietà TransactionOption dell'attività Esegui SQL viene impostata su **Required**.  
  
 Nella figura seguente vengono illustrate le cinque transazioni non correlate del pacchetto. Una transazione viene avviata nel contenitore Sequenza e le altre quattro vengono avviate dalle attività Esegui SQL.  
  
 ![Implementazione di più transazioni](../integration-services/media/mw-dts-trans2.gif "Implementazione di più transazioni")  
 
## <a name="inherited-transactions"></a>Transazioni ereditate
 Un pacchetto può eseguire un altro pacchetto tramite l'attività Esegui pacchetto. Il pacchetto figlio, ovvero il pacchetto eseguito dall'attività Esegui pacchetto, può creare la propria transazione del pacchetto o ereditare quella del padre.  
  
 Un pacchetto figlio eredita la transazione del pacchetto padre se sono soddisfatte le due condizioni seguenti:  
  
-   Il pacchetto viene richiamato da un'attività Esegui pacchetto.  
  
-   Anche l'attività Esegui pacchetto che richiama il pacchetto partecipa alla transazione del pacchetto padre.  
  
 I contenitori e le attività del pacchetto figlio possono partecipare alla transazione del pacchetto padre solo se il pacchetto figlio partecipa alla transazione.  
  
### <a name="example-of-inherited-transactions"></a>Esempio di transazioni ereditate  
 Nella figura seguente sono illustrati tre pacchetti che utilizzano transazioni. Ogni pacchetto include più attività. Per evidenziare il comportamento delle transazioni, sono visualizzate solo le attività Esegui pacchetto. Il pacchetto A esegue i pacchetti B e C. Il pacchetto B esegue a sua volta i pacchetti D ed E e il pacchetto C esegue il pacchetto F.  
  
 Ai pacchetti e alle attività sono associati gli attributi di transazione seguenti:  
  
-   **TransactionOption** è impostata su **Required** per i pacchetti A e C  
  
-   **TransactionOption** è impostata su **Supported** per i pacchetti B e D e per le attività Esegui pacchetto B, Esegui pacchetto D e Esegui pacchetto F.  
  
-   **TransactionOption** è impostata su **NotSupported** per il pacchetto E e per le attività Esegui pacchetto C e Esegui pacchetto E.  
  
 ![Flusso di transazioni ereditate](../integration-services/media/mw-dts-executepack.gif "Flusso di transazioni ereditate")  
  
 Solo i pacchetti B, D e F possono ereditare transazioni dal pacchetto padre.  
  
 I pacchetti B e D ereditano la transazione avviata dal pacchetto A.  
  
 Il pacchetto F eredita la transazione avviata dal pacchetto C.  
  
 I pacchetti A e C controllano le proprie transazioni.  
  
 Il pacchetto E non utilizza transazioni.  
 
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Intervento nel blog [How to Use Transactions in SQL Server Integration Services SSIS](https://go.microsoft.com/fwlink/?LinkId=157783) sul sito Web all'indirizzo www.mssqltips.com  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni ereditate](https://msdn.microsoft.com/library/90db5564-d41e-4cfe-8c9e-4e68d41eff1c)   
 [Più transazioni](https://msdn.microsoft.com/library/c3664a94-be89-40c0-a3a0-84b74a7fedbe)  
  
  
