---
title: In generale i comandi di forma | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f44063e4f1994e01f3685fdb2c7c47a5c41d4998
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704901"
---
# <a name="shape-commands-in-general"></a>Comandi Shape in generale
Il data shaping definisce le colonne di una data shaping **Recordset**, le relazioni tra le entità rappresentate dalle colonne e il modo in cui le **Recordset** viene popolato con i dati.  
  
 Una data shaping **Recordset** può contenere i seguenti tipi di colonne.  
  
|Tipo di colonna|Descrizione|  
|-----------------|-----------------|  
|data|I campi da un **Recordset** restituita da un comando di query per un provider di dati, di tabella o la forma precedentemente **Recordset**.|  
|Capitolo|Un riferimento a un'altra **Recordset**, definita come una *capitolo*. Le colonne a capitoli consentono di definire un *padre-figlio* relazione in cui le *padre* è la **Recordset** che contiene la colonna a capitoli e il *figlio* è il **Recordset** rappresentato dal capitolo.|  
|aggregazione|Il valore della colonna è derivato per l'esecuzione di un' *funzione di aggregazione* su tutte le righe o una colonna di tutte le righe di un elemento figlio **Recordset**. (Vedere le funzioni di aggregazione nell'argomento seguente [funzioni di aggregazione, funzione CALC e parola chiave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|espressione calcolata|Il valore della colonna è derivato calcolando un'espressione di applicazioni nelle colonne della stessa riga di Visual Basic il **Recordset**. L'espressione è l'argomento della funzione CALC. (Vedere espressione calcolata nell'argomento seguente [funzioni di aggregazione, funzione CALC e la nuova parola chiave](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) e nella [funzioni di applicazioni Visual Basic](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|nuovo|Campi vuoti, creati, che possono essere popolati con i dati in un secondo momento. La colonna viene definita con la parola chiave NEW. (Vedere nuova parola chiave nell'argomento seguente [funzioni di aggregazione, funzione CALC e parola chiave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Un comando shape può contenere una clausola che specifica un comando di query per un provider di dati sottostante verrà restituito un **Recordset** oggetto. La sintassi della query dipende dai requisiti del provider di dati sottostante. In genere è SQL, anche se ADO non richiede l'uso di qualsiasi linguaggio di query specifico.  
  
 I comandi di forma possono essere emesso da **Recordset** oggetti oppure impostando il [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) proprietà del [comando](../../../ado/reference/ado-api/command-object-ado.md) e quindi chiamando il [Execute ](../../../ado/reference/ado-api/execute-method-ado-command.md) (metodo).  
  
 È possibile usare una clausola SQL JOIN per correlare due tabelle. Tuttavia, un modello gerarchico **Recordset** possono rappresentare le informazioni in modo più efficiente. Ogni riga di una **Recordset** creato da informazioni a ripetizioni JOIN in modo ridondante da una delle tabelle. Un modello gerarchico **Recordset** ha un solo padre **Recordset** per ogni figlio più **Recordset** oggetti.  
  
 Comandi Shape possono essere annidati. Ovvero il *comando padre* oppure *comando figlio* stesso potrebbe essere un altro comando shape.  
  
 Il provider shape restituisce sempre un cursore del client, anche quando l'utente specifica una posizione del cursore **adUseServer**.  
  
 È possibile accedere la **Recordset** componenti del data shaping **Recordset** a livello di codice o tramite un controllo visuale appropriato.  
  
 Microsoft fornisce uno strumento visivo che genera i comandi di forma (vedere la [ambiente Data Designer](https://go.microsoft.com/fwlink/?LinkId=5689) nella documentazione di Visual Basic 6) e un altro che consente di visualizzare gerarchica dei cursori (vedere "utilizzo di Microsoft gerarchici Controllo FlexGrid"nella documentazione di Visual Basic 6).  
  
 Per informazioni sulla navigazione gerarchico **Recordset**, vedere [accesso alle righe in un Recordset gerarchico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 Per informazioni dettagliate sui comandi di forma sintatticamente corretto, vedere [grammatica formale forma](../../../ado/guide/data/formal-shape-grammar.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Funzioni di aggregazione, funzione CALC e parola chiave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [Invio di comandi al provider di dati sottostante](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
