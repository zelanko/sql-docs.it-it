---
title: Recupero di un valore singolo da un database
description: Informazioni su come restituire un singolo valore in ADO.NET. Questo codice di esempio restituisce il valore della colonna Identity per un record inserito.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: b38526cd-a62a-48cb-822a-e91dfa68e02d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: c4815d048e5648e2c89c2cc32b8f159cc515f2b5
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428230"
---
# <a name="obtaining-a-single-value-from-a-database"></a>Recupero di un valore singolo da un database

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Può essere necessario restituire informazioni del database costituite semplicemente da un singolo valore anziché da una tabella o da un flusso di dati. È possibile restituire il risultato di una funzione di aggregazione, ad esempio COUNT(\*), SUM(Price) o AVG(Quantity). L'oggetto **Command** consente di restituire singoli valori usando il metodo **ExecuteScalar**. Il metodo **ExecuteScalar** restituisce come valore scalare il valore della prima colonna della prima riga del set di risultati.

## <a name="example"></a>Esempio

Nell'esempio di codice seguente viene inserito un nuovo valore nel database usando un <xref:Microsoft.Data.SqlClient.SqlCommand>. Per restituire il valore della colonna Identity per il record inserito, viene usato il metodo <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteScalar%2A>.

[!code-csharp[DataWorks SqlCommand.ExecuteScalar#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteScalar_Return_Id.cs#1)]

## <a name="see-also"></a>Vedere anche

- [Comandi e parametri](commands-parameters.md)
- [Esecuzione di un comando](execute-command.md)
