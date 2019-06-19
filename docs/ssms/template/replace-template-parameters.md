---
title: Sostituire i parametri del modello | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.templates.replaceparameters.f1
helpviewer_keywords:
- template parameters [Template Explorer]
- templates [Transact-SQL], replacing parameters
- Replace (Query) Template Parameters dialog box
- replacing template parameters
ms.assetid: 1234aa14-3464-4a3e-922a-5cfb8fb23627
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7f81fcd7ad4f1ff8b99eccdaa2d3f1b0a0179e2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65102651"
---
# <a name="replace-template-parameters"></a>Sostituisci parametri modello
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
I modelli contengono parametri che possono essere sostituiti da valori specifici dell'implementazione ogni volta che il modello è utilizzato. Dopo avere aperto un modello in un editor di codice, è possibile sostituire i parametri con i valori attinenti all'implementazione.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
La finestra di dialogo **Imposta valori per parametri modello** è una griglia con tre colonne. Le colonne **Parametro** e **Tipo** sono di sola lettura e non possono essere modificate. Rivedere il contenuto della colonna **Valore** e modificare i valori predefiniti in base all'implementazione.  
  
Per usare questa finestra di dialogo, è necessario che i parametri nello script siano racchiusi tra parentesi angolari (`< >`) nel formato `<`*parameter_name*`,` *data_type*`,` *default_value*`>`.  
  
## <a name="replace-template-parameters"></a>Sostituisci parametri modello  
Dopo avere aperto il modello in una finestra dell'editor di codice:  
  
1.  Scegliere **Imposta valori per parametri modello** dal menu **Query**.  
  
2.  Nella finestra di dialogo **Imposta valori per parametri modello** la colonna **Valori** contiene un valore suggerito per ogni parametro. Accettare il valore o sostituirlo con uno nuovo.  
  
3.  Fare clic su **OK** per chiudere la finestra di dialogo **Replace Template Parameters** (Sostituisci parametri modello) e modificare lo script nell'editor di query.  
  
## <a name="see-also"></a>Vedere anche  
[Esplora modelli](../../ssms/template/template-explorer.md)  
[Aprire un modello](../../ssms/template/open-a-template.md)  
  
