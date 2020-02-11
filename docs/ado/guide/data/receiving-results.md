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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924528"
---
# <a name="receiving-results"></a>Ricezione dei risultati
In ADO la maggior parte dei comandi genera alcune informazioni restituite al chiamante. Per i comandi che restituiscono un set di righe, i risultati vengono ricevuti in un oggetto **Recordset** , che è probabilmente il più utilizzato degli oggetti ADO.  
  
 Esistono diversi modi per ricevere dati in un oggetto **Recordset** da un'origine dati, inclusa la chiamata a quanto segue:  
  
-   [Metodo Connection. Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command. Execute (metodo)](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset. Open (metodo)](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection. NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection. StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 La ricezione di dati in un oggetto **Recordset** conclude il processo di recupero dei dati, con la partecipazione di un oggetto **Connection** e di un oggetto **Command** , in modo implicito o esplicito. In un tipico sistema di applicazioni client/server, l'intero processo di recupero dei dati richiede un round trip sulla rete per ogni **Recordset**compilato.  
  
 Per ricevere più set di risultati significa che è necessario eseguire diversi round trip in rete, uno per ogni set di dati incapsulato in un oggetto **Recordset** . Per le reti lente o congestionate, la riduzione del numero di round trip può contribuire a migliorare le prestazioni dell'applicazione. Alcuni provider offrono pertanto supporto per la ricezione di più **Recordset**in un'unica round trip. Questo argomento viene illustrato nell'argomento seguente:  
  
-   [Ricezione di più recordset](../../../ado/guide/data/receiving-multiple-recordsets.md)
