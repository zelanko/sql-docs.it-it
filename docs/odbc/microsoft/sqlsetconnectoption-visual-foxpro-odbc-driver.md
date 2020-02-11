---
title: SQLSetConnectOption (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48a4c8666ab7aa7e210289564210d99c947e5631
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071709"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: parziale  
  
 Conformità API ODBC: livello 1  
  
 Imposta le opzioni che determinano gli aspetti delle connessioni. Questa funzione è parzialmente supportata: il driver supporta tutti i valori per l'argomento *fOption* , ma non supporta alcuni valori *parametro vParam* per l'argomento *fOption* SQL_TXN_ISOLATION.  
  
 Nella tabella seguente vengono descritti solo gli argomenti con comportamento specifico dell'implementazione del driver ODBC Visual FoxPro di **SQLSetConnectOption**.  
  
|*fOption*|Osservazioni|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se si sceglie SQL_AUTOCOMMIT_OFF, l'applicazione deve eseguire il commit o il rollback delle transazioni in modo esplicito con [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); al termine, il driver ODBC Visual FoxPro non esegue automaticamente il commit di un'istruzione transazionale. Il driver inizia una transazione se l'istruzione è transazionale.|  
|SQL_CURRENT_QUALIFIER|Può essere un nome di [database](../../odbc/microsoft/visual-foxpro-terminology.md) completo o un percorso completo di una directory che contiene zero o più [tabelle gratuite](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Restituisce l'errore "driver non in grado".|  
|SQL_CURSORS|Restituisce l'errore "driver non in grado".|  
|SQL_PACKET_SIZE|Restituisce l'errore "driver non in grado".|  
|SQL_TXN_ISOLATION|Il driver consente solo SQL_TXN_READ_COMMITTED.<br /><br /> Gli *parametro vParam*seguenti non sono supportati:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Per ulteriori informazioni, vedere [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) in *ODBC Programmer ' s Reference*.
