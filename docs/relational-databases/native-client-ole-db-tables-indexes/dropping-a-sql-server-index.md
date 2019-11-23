---
title: Eliminazione di un indice SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2481c516714acd58ba243c614534b1079be6b0f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761583"
---
# <a name="dropping-a-sql-server-index"></a>Eliminazione di un indice di SQL Server

  Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client espone la funzione **IIndexDefinition::D ropindex** . Questo consente ai consumer di rimuovere una colonna da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Il provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client espone alcuni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vincoli PRIMARY KEY e UNIQUE come indici. Il proprietario della tabella, il proprietario del database e alcuni membri del ruolo amministrativo possono modificare una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eliminando un vincolo. Per impostazione predefinita, solo il proprietario della tabella può eliminare un indice. L'esito positivo o negativo di **DropIndex** dipende quindi non solo dai diritti di accesso dell'utente dell'applicazione, ma anche dal tipo di indice indicato.  
  
 I consumer specificano il nome della tabella come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel parametro *pTableID*. Il membro *eKind* di *pTableID* deve essere DBKIND_NAME.  
  
 I consumer specificano il nome dell'indice come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel parametro *pIndexID*. Il membro *eKind* di *pIndexID* deve essere DBKIND_NAME. Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client non supporta la funzionalità OLE DB di eliminazione di tutti gli indici in una tabella quando *pIndexID* è null. Se *pIndexID* è Null, viene restituito E_INVALIDARG.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e indici](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
