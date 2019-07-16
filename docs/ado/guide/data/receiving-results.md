---
title: Ricezione dei risultati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b861553e9a71ce56377f8d87bba0f9e26e929c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924528"
---
# <a name="receiving-results"></a>Ricezione dei risultati
In ADO la maggior parte dei comandi generare alcune informazioni restituite al chiamante. Per i comandi di restituzione di set di righe, i risultati vengono ricevuti un **Recordset** oggetto, che è probabilmente più utilizzato l'oggetto ADO.  
  
 Esistono diversi modi per ricevere i dati in un **Recordset** oggetti da un'origine dati, tra cui la chiamata seguente:  
  
-   [Metodo Connection. Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command. Execute (metodo)](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Metodo Open](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 Ricezione di dati in un **Recordset** oggetto conclude il processo di recupero di dati, con la partecipazione di un **connessione** oggetto e un **comando** dell'oggetto, in modo implicito o in modo esplicito. In un sistema di applicazioni client/server tipico, l'intero processo di recupero dei dati è necessario un round trip in rete per ogni riempito **Recordset**.  
  
 Per ricevere più di un set di risultati significa che è necessario per rendere più round trip in rete, uno per ogni set di dati, incapsulate in un **Recordset** oggetto. Per le reti lente o sovraccarica, riducendo il numero di round trip possa contribuire a migliorare le prestazioni dell'applicazione. Di conseguenza, alcuni provider di servizi offre il supporto per la ricezione di più **Recordset**s in un unico round trip. Questo argomento viene illustrato nel seguente argomento:  
  
-   [Ricezione di più recordset](../../../ado/guide/data/receiving-multiple-recordsets.md)
