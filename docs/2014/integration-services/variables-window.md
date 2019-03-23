---
title: Finestra Variabili | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.variables.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 62dd9af9ea66678c2cc69a016b83e907025a4294
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392999"
---
# <a name="variables-window"></a>Finestra Variabili
  Usare la finestra **Variabili** per creare e modificare variabili definite dall'utente e visualizzare quelle di sistema.  
  
 Per impostazione predefinita la finestra **Variabili** si trova sotto l'area **Gestioni connessioni** in Progettazione SSIS, in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Se non viene visualizzata la finestra **Variabili**, fare clic su **Variabili** nel menu **SSIS** per visualizzare la finestra.  
  
 Facoltativamente, è possibile visualizzare la finestra **Variabili** eseguendo il mapping del comando View.Variables a una combinazione di tasti scelta dall'utente nella pagina **Tastiera** della finestra di dialogo **Opzioni** .  
  
> [!NOTE]
>  I valori delle proprietà `Name` e `Namespace` devono iniziare con una delle lettere dell'alfabeto definite dallo standard Unicode 2.0 oppure con un carattere di sottolineatura (_). I caratteri successivi possono includere lettere o numeri, come definito dallo standard Unicode 2.0, o il carattere di sottolineatura (\_).  
  
## <a name="options"></a>Opzioni  
 **Aggiungi variabile**  
 Consente di aggiungere una variabile definita dall'utente.  
  
 **Sposta variabile**  
 Fare clic su una variabile nell'elenco e quindi fare clic su **Sposta variabile** per modificare l'ambito della variabile. Nella finestra di dialogo **Seleziona nuovo ambito** selezionare il pacchetto oppure un contenitore, un'attività o un gestore eventi del pacchetto per modificare l'ambito della variabile.  
  
 Per altre informazioni sull'ambito delle variabili, vedere [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md).  
  
 **Elimina variabile**  
 Selezionare una variabile dall'elenco e quindi fare clic su **Elimina variabile**.  
  
 **Opzioni griglia**  
 Fare clic su questo pulsante per aprire la finestra di dialogo **Opzioni griglia variabili** , in cui è possibile modificare la selezione delle colonne e applicare i filtri alla finestra **Variabili** . Per altre informazioni, vedere [Opzioni griglia variabili](../../2014/integration-services/variable-grid-options.md).  
  
 `Name`  
 Consente di visualizzare il nome della variabile. È possibile aggiornare il nome delle variabili definite dall'utente.  
  
 **Ambito**  
 Consente di visualizzare l'ambito della variabile, che può essere costituito dall'intero pacchetto oppure da un contenitore o da un'attività. L'ambito della variabile deve essere sufficiente affinché la variabile sia visibile per qualsiasi altro componente o attività che necessita di leggerne o impostarne il valore.  
  
 È possibile modificare l'ambito facendo clic sulla variabile e quindi selezionando **Sposta variabile** nella finestra **Variabili** .  
  
 **Tipo di dati**  
 Consente di visualizzare il tipo di dati della variabile. È possibile selezionare un tipo di dati dall'elenco per le variabili definite dall'utente.  
  
> [!NOTE]  
>  Se si assegna un'espressione alla variabile, non è possibile modificare il tipo di dati.  
  
 **Valore**  
 Consente di visualizzare il valore della variabile. È possibile aggiornare il valore per le variabili definite dall'utente. Questo valore può essere letterale, un'espressione e una stringa su più righe. Per assegnare un'espressione alla variabile, fare clic sul pulsante con i puntini di sospensione accanto alla colonna **Espressione** nella finestra **Variabili** .  
  
 `Namespace`  
 Consente di visualizzare il nome dello spazio dei nomi. Variabili definite dall'utente vengono inizialmente create nel **utente** dello spazio dei nomi, ma è possibile modificare il nome dello spazio dei nomi nel `Namespace` campo. Per visualizzare questa colonna, fare clic su **Opzioni griglia**.  
  
 **Raise Change Event**  
 Consente di indicare se generare l'evento `OnVariableValueChanged` alla modifica di un valore. È possibile aggiornare il valore per le variabili definite dall'utente e le variabili di sistema. Per impostazione predefinita, questa colonna non viene visualizzata nella finestra **Variabili** . Per visualizzare questa colonna, fare clic su **Opzioni griglia**.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione della variabile. È possibile modificare la descrizione per le variabili definite dall'utente. Per impostazione predefinita, questa colonna non viene visualizzata nella finestra **Variabili** . Per visualizzare questa colonna, fare clic su **Opzioni griglia**.  
  
 **Espressione**  
 Consente di visualizzare l'espressione assegnata alla variabile. Per assegnare un'espressione, fare clic sul pulsante con i puntini di sospensione.  
  
 Se si assegna un'espressione a una variabile, accanto a quest'ultima viene visualizzato un marcatore icona speciale. Tale marcatore icona speciale viene visualizzato anche accanto alle gestioni connessioni e alle attività in cui sono impostate espressioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)   
 [Utilizzo di variabili nei pacchetti](../../2014/integration-services/use-variables-in-packages.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md)   
 [Generazione di file di dump per l'esecuzione del pacchetto](troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
