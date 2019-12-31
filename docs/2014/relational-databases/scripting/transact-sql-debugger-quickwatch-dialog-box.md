---
title: Finestra di dialogo Controllo immediato
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d41aab8066b4ce1ee4e45fa9c363e60479868a5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243036"
---
# <a name="quickwatch-dialog-box"></a>Finestra di dialogo Controllo immediato
  Utilizzare la finestra di dialogo controllo **immediato** per visualizzare rapidamente il tipo di dati e [!INCLUDE[tsql](../../includes/tsql-md.md)] il valore di un'espressione, ad esempio una variabile o un parametro [!INCLUDE[tsql](../../includes/tsql-md.md)] , quando si esegue il debug del codice. Per controllare più espressioni, è anche possibile aggiungere l'espressione a una finestra **Espressione di controllo** .  
  
## <a name="task-list"></a>Elenco attività  
 **Per accedere alla finestra di dialogo controllo immediato**  
  
-   Scegliere **Controllo immediato** dal menu **Debug**.  
  
 **Per visualizzare le informazioni su un'espressione**  
  
1.  Nella casella di riepilogo **Espressione** digitare o selezionare l'espressione desiderata. Sono supportate le espressioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti:  
  
    -   Variabili.  
  
    -   Parametri.  
  
    -   Funzioni di sistema il cui nome inizia con @@.  
  
    -   Espressioni compilate applicando operatori a uno o più parametri, variabili o funzioni di sistema, ad esempio @@IntegerCounter + 1 o FirstName + LastName.  
  
    -   Istruzioni Transact-SQL tramite cui viene restituito un solo valore, ad esempio SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
2.  Fare clic su **Rivaluta**.  
  
 **Per aggiungere l'espressione controllo immediato a un finestra Espressioni di controllo**  
  
-   Fare clic su **Aggiungi espressione di controllo**.  
  
 **Per modificare il valore dell'espressione controllo immediato**  
  
-   Fare clic con il pulsante destro del mouse sull'espressione, quindi scegliere **Modifica valore**.  
  
## <a name="options"></a>Options  
 **Elenco di espressioni**  
 Consente di visualizzare l'espressione selezionata. L'elenco a discesa contiene un set di espressioni che è possibile selezionare per visualizzarle. Le espressioni incluse nell'elenco sono quelle disponibili nell'ambito del frame dello stack corrente selezionato nella finestra **Stack di chiamate** . Per visualizzare un'espressione diversa, immettere l'espressione o selezionarla nell'elenco. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta le espressioni seguenti: variabili, parametri e le funzioni di sistema i cui nomi iniziano con @@.  
  
 **Griglia valore**  
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
 [Debugger Transact-SQL](transact-sql-debugger.md)   
 [Informazioni del debugger Transact-SQL](transact-sql-debugger-information.md)   
 [Finestra espressioni di controllo](transact-sql-debugger-watch-window.md)   
 [Finestra variabili locali](transact-sql-debugger-locals-window.md)   
 [Finestra stack di chiamate](transact-sql-debugger-call-stack-window.md)   
 [Espressioni &#40;&#41;Transact-SQL](/sql/t-sql/language-elements/expressions-transact-sql)  
  
  
