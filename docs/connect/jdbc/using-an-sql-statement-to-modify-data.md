---
title: Uso di un'istruzione SQL per modificare i dati | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a9de31bad8ef2980e7322b529a6a2b68a12355c2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026749"
---
# <a name="using-an-sql-statement-to-modify-data"></a>Uso di un'istruzione SQL per modificare i dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per modificare i dati contenuti in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando un'istruzione SQL, è possibile usare il metodo [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Con il metodo executeUpdate l'istruzione SQL viene passata al database per l'elaborazione e viene restituito un valore che indica il numero di righe modificate.

A tale scopo, è necessario innanzitutto creare un oggetto SQLServerStatement usando il metodo [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

Nell'esempio seguente, viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], viene costruita un'istruzione SQL che aggiunge nuovi dati alla tabella, viene eseguita l'istruzione e viene visualizzato il valore restituito.

[!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]

> [!NOTE]  
> Per usare un'istruzione SQL contenente dei parametri per la modifica dei dati contenuti in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è consigliabile usare il metodo [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) della classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).
>
> Se nella colonna in cui si desidera inserire i dati sono presenti caratteri speciali, quali, ad esempio, gli spazi, è necessario fornire i valori da inserire, anche se si tratta dei valori predefiniti. In caso contrario, l'operazione di inserimento non verrà eseguita correttamente.
>
> Se si desidera che il driver JDBC restituisca tutti i conteggi degli aggiornamenti, inclusi i conteggi degli aggiornamenti restituiti dai trigger eventualmente attivati, impostare la proprietà della stringa di connessione lastUpdateCount su "false". Per altre informazioni sulla proprietà lastUpdateCount, vedere [Impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).

## <a name="see-also"></a>Vedere anche

[Uso di istruzioni SQL](../../connect/jdbc/using-statements-with-sql.md)
