---
title: Modificare la query di origine OData in fase di esecuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2c355c95c5e6c686a063c4c32081aa0740f8e2fd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915211"
---
# <a name="modify-odata-source-query-at-runtime"></a>Modificare la query di origine OData in fase di esecuzione
  È possibile modificare la query di origine OData in fase di esecuzione aggiungendo un'espressione alla proprietà **[Origine OData].[Query]** dell'attività Flusso di dati.  
  
 Si noti che le colonne devono essere le stesse di quelle utilizzate in fase di progettazione; in caso contrario, verrà visualizzato un errore al momento dell'esecuzione del pacchetto. Assicurarsi di specificare le stesse colonne (nello stesso ordine) quando si utilizza l'opzione query $select. Un'alternativa più sicura all'uso dell'opzione $select consiste nel deselezionare le colonne non desiderate direttamente dall'interfaccia utente del componente di origine.  
  
 Sono disponibili alcune modalità differenti per impostare dinamicamente il valore di query in fase di esecuzione. Di seguito sono riportati alcuni dei metodi più comuni.  
  
## <a name="exposing-the-query-as-a-parameter"></a>Esposizione della query come parametro  
 Nella procedura seguente sono riportati i passaggi per esporre la query utilizzata da un componente di origine OData come parametro nel pacchetto.  
  
1.  Fare clic con il pulsante destro del mouse sull'**attività Flusso di dati** e selezionare l'opzione **Imposta parametri**.  
  
2.  Nella finestra di dialogo imposta **parametri** selezionare **[ \<Name of the OData Source Component> ]. [ Query]** per la **Proprietà**.  
  
3.  Scegliere se **creare un nuovo parametro** o **usare un parametro esistente**.  
  
4.  Se si seleziona **Crea nuovo parametro**, eseguire le operazioni seguenti:  
  
    1.  Immettere un **nome** e una **descrizione** per il parametro.  
  
    2.  Specificare il **valore** predefinito per il parametro.  
  
    3.  Specificare l' **ambito** (**pacchetto** o **progetto**) per il parametro.  
  
    4.  Specificare se il parametro è **obbligatorio** o meno.  
  
5.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
## <a name="using-an-expression"></a>Utilizzo di un'espressione  
 Questo metodo è utile quando si desidera creare dinamicamente la stringa di query in fase di esecuzione. In questo esempio, la variabile MaxRows verrà impostata in altro modo (script, parametro e così via).  
  
1.  Selezionare l' **attività Flusso di dati** contenente l' **Origine OData**.  
  
2.  Nella finestra **Proprietà** selezionare la proprietà **Espressioni** .  
  
3.  Fare clic su... pulsante (ellissi) per visualizzare l' **Editor espressioni di proprietà**.  
  
4.  Selezionare la proprietà **[Origine OData].[Query]** .  
  
5.  Fare clic su... pulsante (ellissi) per **espressione**.  
  
6.  Immettere l' **espressione**.  
  
7.  Fare clic su **OK**.  
  
> [!WARNING]  
>  Si noti che quando si utilizza questo approccio, è necessario assicurarsi che i valori impostati siano URL correttamente codificati. Alla ricezione di valori dall'input utente, ad esempio l'impostazione di singoli valori di opzioni query da un parametro, è necessario assicurarsi che i valori siano convalidati per evitare potenziali attacchi SQL injection.  
  
  
