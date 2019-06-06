---
title: Preparazione ed esecuzione di comandi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6bf2120468a00de2150f6105f4d79ec5a2ed4278
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700452"
---
# <a name="preparing-and-executing-commands"></a>Preparazione ed esecuzione di comandi
I comandi sono istruzioni emesso a un provider di eseguire alcune operazioni per l'origine dati sottostante. Un'istruzione SQL, ad esempio, è un comando per il Provider di dati di Microsoft SQL. In ADO, i comandi sono in genere rappresentati dal **comandi** oggetti, anche se semplici comandi possono essere generati anche tramite **connessione** oppure **Recordset** oggetti.  
  
 È possibile usare la **comando** oggetto richiedere qualsiasi tipo di operazione supportato dal provider, presupponendo che il provider può interpretare correttamente la stringa di comando. È un'operazione comune per i provider di dati per eseguire query su un database e restituire i record in una **Recordset** oggetto, che può essere considerato un contenitore per contenere il risultato e uno strumento per visualizzare il risultato. Come con molti oggetti ADO, alcuni **comando** raccolte di oggetti, metodi o proprietà possono generare errori quando viene fatto riferimento, a seconda della funzionalità del provider.  
  
 Oltre a usare **comandi** oggetti, è possibile utilizzare il **Execute** metodo sul **connessione** oggetto o il **Open** metodo sul  **Recordset** oggetto per emettere un comando e consentire l'esecuzione. Tuttavia, è consigliabile usare un **comando** dell'oggetto se è necessario riutilizzare un comando nel codice o se è necessario passare informazioni dettagliate sui parametri con il comando. Questi scenari sono illustrati in dettaglio più avanti in questa sezione.  
  
> [!NOTE]
>  Determinati **comandi**s può restituire un risultato impostato come flusso binario o come un unico **Record** anziché come una **Recordset**, se supportato dal provider. Inoltre, alcuni **comando**s non sono progettati per restituire qualsiasi set di risultati affatto (ad esempio, una query SQL Update). Questa sezione illustra lo scenario più comune, tuttavia: l'esecuzione **comandi**che restituiscono i risultati come una **Recordset** oggetto. Per altre informazioni sulla restituzione di risultati in **Record**s oppure **Stream**s, vedere [record e flussi](../../../ado/guide/data/records-and-streams.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Panoramica dell'oggetto Command](../../../ado/guide/data/command-object-overview.md)  
  
-   [Creazione ed esecuzione di un comando semplice](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Parametri dell'oggetto Command](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Chiamata di una stored procedure con Command](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [Chiama una Stored Procedure come metodo in un oggetto di connessione](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [Comandi con nome](../../../ado/guide/data/named-commands.md)  
  
-   [Passaggio di parametri a un comando con nome](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
