---
title: Uso di un'istruzione SQL per modificare gli oggetti di database | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de8e357328c151e3762f324dcbeba2525df53530
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026557"
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>Uso di un'istruzione SQL per modificare gli oggetti di database

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per modificare gli oggetti di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un'istruzione SQL, è possibile usare il metodo [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) della classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Il metodo executeUpdate passerà l'istruzione SQL al database per l'elaborazione e quindi restituirà un valore pari a 0 poiché non sono presenti righe interessate dall'operazione.

A tale scopo, è necessario innanzitutto creare un oggetto SQLServerStatement usando il metodo [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

> [!NOTE]  
> Le istruzioni SQL che modificano gli oggetti presenti in un database vengono definite istruzioni DDL (Data Definition Language) e Sono incluse istruzioni come `CREATE TABLE`, `DROP TABLE`, `CREATE INDEX` e `DROP INDEX`. Per altre informazioni sui tipi di istruzioni DDL supportati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la documentazione in linea di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], viene costruita un'istruzione SQL che creerà l'oggetto semplice TestTable nel database e quindi viene eseguita l'istruzione e visualizzato il valore restituito.

[!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]

## <a name="see-also"></a>Vedere anche

[Uso di istruzioni SQL](../../connect/jdbc/using-statements-with-sql.md)
