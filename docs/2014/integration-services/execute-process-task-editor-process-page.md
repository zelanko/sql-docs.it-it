---
title: Editor attività Esegui processo (pagina processo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process Task Editor
ms.assetid: 0fc22406-e79b-47a4-a7e4-108d4ce6202f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 543ab9724f44e5db1f4532eeadcce79b36de52b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769587"
---
# <a name="execute-process-task-editor-process-page"></a>Execute Process Task Editor (Process Page)
  Utilizzare la pagina **Processo** della finestra di dialogo **Editor attività Esegui processo** per configurare le opzioni di esecuzione del processo. Tali opzioni includono il file eseguibile da avviare, il relativo percorso, gli argomenti del prompt dei comandi, nonché le variabili per la generazione dell'input e l'acquisizione dell'output.  
  
 Per ulteriori informazioni su questa attività, vedere [Execute Process Task](control-flow/execute-process-task.md).  
  
## <a name="options"></a>Opzioni  
 **RequireFullFileName**  
 Consente di indicare se l'attività deve avere esito negativo nel caso in cui il file eseguibile non venga trovato nel percorso specificato.  
  
 **File eseguibile**  
 Consente di digitare il nome del file eseguibile da avviare.  
  
 **Argomenti**  
 Consente di specificare gli argomenti del prompt dei comandi.  
  
 **WorkingDirectory**  
 Digitare il percorso della cartella contenente il file eseguibile oppure fare clic sul pulsante sfoglia **(...)** per individuare la cartella.  
  
 **StandardInputVariable**  
 Selezionare una variabile per l'invio dell'input al processo oppure fare clic su \<**Nuova variabile...**> per crearne una nuova:  
  
 **Argomenti correlati:**  [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
 **StandardOutputVariable**  
 Selezionare una variabile per l'acquisizione dell'output del processo oppure fare clic su \<**Nuova variabile...**> per crearne una nuova.  
  
 **StandardErrorVariable**  
 Selezionare una variabile per l'acquisizione dell'output di errore del processore oppure fare clic su \<**Nuova variabile...**> per crearne una nuova.  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 Consente di indicare se l'attività deve avere esito negativo nel caso in cui il codice di uscita del processo non corrisponda al valore specificato in **SuccessValue**.  
  
 **SuccessValue**  
 Consente di specificare il valore restituito dal file eseguibile per segnalare l'esito positivo. Per impostazione predefinita, questo valore è impostato su **0**.  
  
 **TimeOut**  
 Consente di specificare il numero di secondi di esecuzione del processo. Il valore **0** indica che non è previsto alcun timeout e il processo viene eseguito fino al completamento o finché non si verifica un errore.  
  
 **TerminateProcessAfterTimeOut**  
 Consente di indicare se il processo deve essere terminato allo scadere del periodo di timeout specificato nell'opzione **TimeOut** . Questa opzione è disponibile solo se **TimeOut** non è impostata su **0**.  
  
 **WindowStyle**  
 Consente di specificare lo stile della finestra in cui viene eseguito il processo.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Pagina Espressioni](expressions/expressions-page.md)  
  
  
