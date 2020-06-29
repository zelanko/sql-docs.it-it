---
title: Editor attività Esegui SQL (pagina set di risultati) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: d27000c8-8d91-4e1c-b45e-bca9a3c12f6d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 027f3c77e84b47958e9fb6567acdb308c14eb1e7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437358"
---
# <a name="execute-sql-task-editor-result-set-page"></a>Editor attività Esegui SQL (pagina Set dei risultati)
  La pagina **Set dei risultati** della finestra di dialogo **Editor attività Esegui SQL** consente di eseguire il mapping dei risultati dell'istruzione SQL a variabili nuove o esistenti. Le opzioni disponibili in questa finestra di dialogo sono disabilitate se **ResultSet** è impostato su **None**nella pagina Generale.  
  
 Per altre informazioni su questa attività vedere [Attività Esegui SQL](control-flow/execute-sql-task.md) e [Set di risultati nell'attività Esegui SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md).  
  
## <a name="options"></a>Opzioni  
 **Nome risultato**  
 Dopo aver aggiunto un set di mapping del set di risultati facendo clic su **Aggiungi**, specificare un nome per il risultato. A seconda del tipo di set di risultati, è necessario utilizzare nomi specifici per i risultati.  
  
 Se il set di risultati è di tipo **Riga singola**, è possibile utilizzare o il nome di una colonna restituita dalla query o il numero che rappresenta la posizione di una colonna nell'elenco di colonne di una colonna restituita dalla query.  
  
 Se il set di risultati è di tipo **Set dei risultati completo** o **XML**, sarà necessario usare 0 come nome del set di risultati.  
  
 **Argomenti correlati**: [Set di risultati nell'attività Esegui SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
 **Nome variabile**  
 Eseguire il mapping del set di risultati a una variabile selezionando una variabile o facendo clic \<**New variable...**> per aggiungere una nuova variabile tramite la finestra di dialogo **Aggiungi variabile** .  
  
 **Aggiungere**  
 Fare clic su questo pulsante per aggiungere un mapping del set di risultati.  
  
 **Rimuovi**  
 Selezionare un mapping del set di risultati e quindi fare clic su **Rimuovi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Esegui SQL &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor attività Esegui SQL &#40;pagina Mapping parametri&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference)  
  
  
