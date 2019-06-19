---
title: Finestra di dialogo Controllo immediato | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c653130f1b2d3cfee447a3c7dec5790d14c9641f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65821707"
---
# <a name="transact-sql-debugger---quickwatch-dialog-box"></a>Debugger Transact-SQL - Finestra di dialogo Controllo immediato
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Utilizzare la finestra di dialogo **Controllo immediato** per visualizzare rapidamente il tipo di dati e il valore di un'espressione [!INCLUDE[tsql](../../includes/tsql-md.md)] , ad esempio una variabile o un parametro, quando si esegue il debug di codice [!INCLUDE[tsql](../../includes/tsql-md.md)] . Per controllare più espressioni, è anche possibile aggiungere l'espressione a una finestra **Espressione di controllo** .  
  
## <a name="task-list"></a>Elenco attività  
 **Per accedere alla finestra di dialogo Controllo immediato**  
  
-   Scegliere **Controllo immediato** dal menu **Debug**.  
  
 **Per visualizzare le informazioni relative a un'espressione**  
  
1.  Nella casella di riepilogo **Espressione** digitare o selezionare l'espressione desiderata. Sono supportate le espressioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti:  
  
    -   Variabili.  
  
    -   Parametri.  
  
    -   Funzioni di sistema il cui nome inizia con @@.  
  
    -   Espressioni compilate applicando operatori a uno o più parametri, variabili o funzioni di sistema, ad esempio @@IntegerCounter + 1 o FirstName + LastName.  
  
    -   Istruzioni Transact-SQL che restituiscono un singolo valore, come ad esempio: SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
2.  Fare clic su **Rivaluta**.  
  
 **Per aggiungere un'espressione di controllo immediato a una finestra Espressione di controllo**  
  
-   Fare clic su **Aggiungi espressione di controllo**.  
  
 **Per modificare il valore di un'espressione di controllo immediato**  
  
-   Fare clic con il pulsante destro del mouse sull'espressione, quindi scegliere **Modifica valore**.  
  
## <a name="options"></a>Opzioni  
 **Elenco di espressioni**  
 Consente di visualizzare l'espressione selezionata. L'elenco a discesa contiene un set di espressioni che è possibile selezionare per visualizzarle. Le espressioni incluse nell'elenco sono quelle disponibili nell'ambito del frame dello stack corrente selezionato nella finestra **Stack di chiamate** . Per visualizzare un'espressione diversa, immettere l'espressione o selezionarla nell'elenco. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta le espressioni seguenti: variabili, parametri e le funzioni di sistema i cui nomi iniziano con @@.  
  
 **Griglia Valore**  
 Consente di visualizzare le proprietà dell'espressione attualmente controllata.  
  
 **Nome**  
 Espressione [!INCLUDE[tsql](../../includes/tsql-md.md)] controllata.  
  
 **Value**  
 Consente di visualizzare il valore assegnato all'espressione. Quando l'espressione non è associata ad alcun valore, viene visualizzato uno spazio vuoto.  
  
 Se la lunghezza di un'espressione è maggiore della larghezza della colonna **Valore** , il valore completo verrà visualizzato in una descrizione comandi quando si sposta il puntatore sulla cella **Valore** per l'espressione.  
  
 Un'icona di lente di ingrandimento in una cella **Valore** indica che è disponibile il visualizzatore del debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] . Nell'elenco è possibile specificare **Visualizzatore testo**, **Visualizzatore XML**o **Visualizzatore HTML**. Per avviare un visualizzatore del debugger, fare clic sull'icona di lente di ingrandimento. Tramite il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] viene visualizzata una finestra di dialogo contenente dati in un formato appropriato per il tipo di dati.  
  
 **Tipo**  
 Consente di visualizzare il tipo di dati dell'espressione.  
  
## <a name="see-also"></a>Vedere anche  
 [Debugger Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Informazioni del debugger Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [finestra Espressioni di controllo](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [finestra Variabili locali](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [Finestra Stack di chiamate](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Espressioni &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
