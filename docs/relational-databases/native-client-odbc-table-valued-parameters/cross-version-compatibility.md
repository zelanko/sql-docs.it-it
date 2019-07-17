---
title: Compatibilità tra versioni | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ce057a2ea0985243bc9c42e6384dfe805e56ff4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030278"
---
# <a name="cross-version-compatibility"></a>Compatibilità tra versioni
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Possono verificarsi conflitti tra versioni quando è previsto che istanze client o server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] elaborino parametri con valori di tabella.  
  
 In generale, la funzionalità dei parametri con valori di tabella è disponibile solo per i client [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] che utilizzano SQL Server Native Client 10.0 o versione successiva e che sono connessi a server [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versione successiva. Nuove colonne in set di risultati di funzioni di catalogo saranno presenti solo quando si è connessi a un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versione successiva) server.  
  
 Se un'applicazione client compilata con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client esegue istruzioni per le quali sono previsti parametri con valori di tabella, il server rileva questa condizione mediante un errore di conversione dei dati e ODBC restituisce l'errore SQLSTATE 07006 e il messaggio "Violazione dell'attributo del tipo di dati".  
  
 Se un'applicazione client che è stata compilata con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 o versioni successive cerca di usare parametri con valori di tabella quando si è connessi a un'istanza del server precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rileverà la situazione, SQLBindCol e SQLBindParameter e SQLSetDescFields SQLSetDescRec chiamate avrà esito negativo con SQLSTATE 07006 e il messaggio "Violazione dell'attributo tipo di dati (la versione di SQL Server per questa connessione non supporta i parametri con valori di tabella) Restricted".  
  
## <a name="see-also"></a>Vedere anche  
 [I parametri con valori di tabella &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
