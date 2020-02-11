---
title: SQLGetConnectOption (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c17cd473d3c96032817c2b183bf65fe360cf3cdc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053681"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: parziale  
  
 Conformità API ODBC: livello 1  
  
 Restituisce l'impostazione corrente di un'opzione di connessione. Questa funzione è parzialmente supportata: il driver supporta tutti i valori per l'argomento *fOption* , ma non supporta alcuni valori *parametro vParam* per l'argomento *fOption* SQL_TXN_ISOLATION.  
  
 Nella tabella seguente vengono descritti solo gli argomenti con comportamento specifico dell'implementazione del driver ODBC Visual FoxPro di **SQLGetConnectOption**.  
  
|*fOption*|Osservazioni|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se si sceglie SQL_AUTOCOMMIT_OFF, l'applicazione deve eseguire il commit o il rollback delle transazioni in modo esplicito con [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); al termine, il driver ODBC Visual FoxPro non esegue automaticamente il commit di un'istruzione transazionale. Il driver inizia una transazione se l'istruzione è transazionale.|  
|SQL_CURRENT_QUALIFIER|Può essere un nome di database completo (file con estensione DBC) o un percorso completo di una directory che contiene zero o più tabelle (file con estensione dbf).|  
|SQL_LOGINTIMEOUT|Restituisce l'errore "driver non in grado".|  
|SQL_CURSORS|Restituisce l'errore "driver non in grado".|  
|SQL_PACKET_SIZE|Restituisce l'errore "driver non in grado".|  
|SQL_TXN_ISOLATION|Il driver consente solo SQL_TXN_READ_COMMITTED.<br /><br /> Gli *parametro vParam*seguenti non sono supportati:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Per ulteriori informazioni, vedere [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) in *ODBC Programmer ' s Reference*.
