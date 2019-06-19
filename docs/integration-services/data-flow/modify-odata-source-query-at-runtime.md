---
title: Fornire una query di origine OData in fase di esecuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4a29245c790f97d92529ff2bf1e100675b3c9530
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726691"
---
# <a name="provide-an-odata-source-query-at-runtime"></a>Fornire una query di origine OData in fase di esecuzione

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 È possibile modificare la query di origine OData in fase di esecuzione aggiungendo un'*espressione* alla proprietà **[Origine OData].[Query]** dell'attività Flusso di dati.  
  
 Le colonne restituite devono essere le stesse restituite in fase di progettazione. In caso contrario, al momento dell'esecuzione del pacchetto si verifica un errore. Assicurarsi di specificare le stesse colonne (nello stesso ordine) quando si utilizza l'opzione query $select. Un'alternativa più sicura all'uso dell'opzione $select consiste nel deselezionare le colonne non desiderate direttamente dall'interfaccia utente del componente di origine.  
  
 Sono disponibili alcune modalità differenti per impostare dinamicamente il valore di query in fase di esecuzione. Ecco alcuni dei metodi più comuni.  
  
## <a name="provide-the-query-as-a-parameter"></a>Specificare la query come parametro  
 La procedura seguente mostra come esporre la query usata da un componente di origine OData come parametro del pacchetto.  
  
1.  Fare clic con il pulsante destro del mouse sull'**attività Flusso di dati** e selezionare l'opzione **Imposta parametri**.  
  
2.  Nella finestra di dialogo **Imposta parametri** selezionare **[\<< nome del componente di origine OData].[Query]** per **Proprietà**.  
  
3.  Scegliere se **creare un nuovo parametro** o **usare un parametro esistente**.  
  
4.  Se si seleziona **Crea nuovo parametro**:  
  
    1.  Immettere un **nome** e una **descrizione** per il parametro.  
  
    2.  Specificare il **valore** predefinito per il parametro.  
  
    3.  Specificare l' **ambito** (**pacchetto** o **progetto**) per il parametro.  
  
    4.  Specificare se il parametro è **obbligatorio** o meno.  
  
5.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
## <a name="provide-the-query-with-an-expression"></a>Specificare la query con un'espressione
 Questo metodo è utile quando si vuole creare dinamicamente la stringa di query in fase di esecuzione.
  
1.  Selezionare l' **attività Flusso di dati** che contiene l' **Origine OData**.  
  
2.  Nella finestra **Proprietà** selezionare la proprietà **Espressioni** .  
  
3.  Fare clic sul pulsante con i puntini di sospensione (...) per visualizzare **Editor espressioni di proprietà**.  
  
4.  Selezionare la proprietà **[Origine OData].[Query]** .  
  
5.  Fare clic sul pulsante con i puntini di sospensione (...) per **Espressione**.  
  
6.  Immettere l' **espressione**.  
  
7.  Fare clic su **OK**.  
  
> [!NOTE]  
> Quando si segue questo approccio, è necessario assicurarsi che i valori impostati siano correttamente codificati in URL. Alla ricezione di valori dall'input utente, ad esempio l'impostazione di singoli valori di opzioni query da un parametro, è necessario assicurarsi che i valori siano convalidati per evitare potenziali attacchi SQL injection.  
  
  
