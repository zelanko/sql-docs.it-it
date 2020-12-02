---
description: Finestra Variabili
title: Finestra Variabili | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.variables.f1
- sql13.dts.designer.variableoptionswindow.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa326be8b57eed58f0aa52876d0d32b889320c58
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "92193741"
---
# <a name="variables-window"></a>Finestra Variabili

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  Usare la finestra **Variabili** per creare e modificare variabili definite dall'utente e visualizzare quelle di sistema.  
  
 Per impostazione predefinita la finestra **Variabili** si trova sotto l'area **Gestioni connessioni** in Progettazione SSIS, in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Se non viene visualizzata la finestra **Variabili**, fare clic su **Variabili** nel menu **SSIS** per visualizzare la finestra.  
  
 Facoltativamente, è possibile visualizzare la finestra **Variabili** eseguendo il mapping del comando View.Variables a una combinazione di tasti scelta dall'utente nella pagina **Tastiera** della finestra di dialogo **Opzioni** .  
  
> [!NOTE]
>  I valori delle proprietà **Name** e **Namespace** devono iniziare con una delle lettere dell'alfabeto definite dallo standard Unicode 2.0 oppure con un carattere di sottolineatura (_). I caratteri successivi possono includere lettere o numeri, come definito dallo standard Unicode 2.0, o il carattere di sottolineatura (\_).  
  
## <a name="options"></a>Opzioni  
 **Aggiungi variabile**  
 Consente di aggiungere una variabile definita dall'utente.  
  
 **Sposta variabile**  
 Fare clic su una variabile nell'elenco e quindi fare clic su **Sposta variabile** per modificare l'ambito della variabile. Nella finestra di dialogo **Seleziona nuovo ambito** selezionare il pacchetto oppure un contenitore, un'attività o un gestore eventi del pacchetto per modificare l'ambito della variabile.  
  
 Per altre informazioni sull'ambito delle variabili, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md).  
  
 **Elimina variabile**  
 Selezionare una variabile dall'elenco e quindi fare clic su **Elimina variabile**.  
  
 **Opzioni griglia**  
 Fare clic su questo pulsante per aprire la finestra di dialogo **Opzioni griglia variabili** , in cui è possibile modificare la selezione delle colonne e applicare i filtri alla finestra **Variabili** . Per altre informazioni, vedere [Opzioni griglia variabili]().  
  
 **Nome**  
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
  
 **Spazio dei nomi**  
 Consente di visualizzare il nome dello spazio dei nomi. Le variabili definite dall'utente vengono inizialmente create nello spazio dei nomi **User** , ma è possibile modificare il nome dello spazio dei nomi nel campo **Spazio dei nomi** . Per visualizzare questa colonna, fare clic su **Opzioni griglia**.  
  
 **Raise Change Event**  
 Consente di indicare se generare l'evento **OnVariableValueChanged** alla modifica di un valore. È possibile aggiornare il valore per le variabili definite dall'utente e le variabili di sistema. Per impostazione predefinita, questa colonna non viene visualizzata nella finestra **Variabili** . Per visualizzare questa colonna, fare clic su **Opzioni griglia**.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione della variabile. È possibile modificare la descrizione per le variabili definite dall'utente. Per impostazione predefinita, questa colonna non viene visualizzata nella finestra **Variabili** . Per visualizzare questa colonna, fare clic su **Opzioni griglia**.  
  
 **Espressione**  
 Consente di visualizzare l'espressione assegnata alla variabile. Per assegnare un'espressione, fare clic sul pulsante con i puntini di sospensione.  
  
 Se si assegna un'espressione a una variabile, accanto a quest'ultima viene visualizzato un marcatore icona speciale. Tale marcatore icona speciale viene visualizzato anche accanto alle gestioni connessioni e alle attività in cui sono impostate espressioni.  

## <a name="variable-grid-options-dialog-box"></a>Finestra di dialogo Opzioni griglia variabili
 Utilizzare la finestra di dialogo **Opzioni griglia variabili** per selezionare le colonne che verranno visualizzate nella finestra **Variabili** e per selezionare i filtri da applicare all'elenco di variabili. Per altre informazioni sulle proprietà delle variabili corrispondenti, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md).  
  
### <a name="options-for-filter"></a>Opzioni per il filtro  
 **Mostra variabili di sistema**  
 Selezionare questa opzione per elencare le variabili di sistema nella finestra **Variabili** . Le variabili di sistema sono predefinite Non è possibile aggiungere né eliminare le variabili di sistema. È possibile modificare l'impostazione della proprietà **RaiseChangedEvent** .  
  
 L'elenco è codificato tramite colori: Le variabili di sistema vengono visualizzate in grigio, mentre quelle definite dall'utente in nero.  
  
 **Mostra variabili di tutti gli ambiti**  
 Selezionare questa opzione per visualizzare le variabili nell'ambito del pacchetto e nell'ambito di contenitori, attività e gestori eventi del pacchetto. Deselezionarla per visualizzare le variabili solo nell'ambito del pacchetto e nell'ambito di un contenitore, un'attività o un gestore eventi selezionato.  
  
 Per altre informazioni sull'ambito delle variabili, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md).  
  
### <a name="options-for-columns"></a>Opzioni per le colonne  
 Selezionare le colonne che si desidera visualizzare nella finestra **Variabili** .  
  
-   **Ambito**  
  
-   **Tipo di dati**  
  
-   **Valore**  
  
-   **Spazio dei nomi**  
  
-   **Genera evento alla modifica del valore della variabile**  
  
-   **Descrizione**  
  
-   **Espressione**  
  
## <a name="see-also"></a>Vedere anche  
 [Variabili di Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md)   
 [Utilizzo di variabili nei pacchetti](./integration-services-ssis-variables.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md)   
 [Generazione di file di dump per l'esecuzione dei pacchetti](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
