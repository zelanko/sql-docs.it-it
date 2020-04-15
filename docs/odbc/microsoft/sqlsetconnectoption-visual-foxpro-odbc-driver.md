---
title: SQLSetConnectOption (driver ODBC di Visual FoxPro) . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2af208663f1e91250faad0ca9538b76bcec43b06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301502"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Parziale  
  
 Conformità API ODBC: livello 1ODBC API Conformance: Level 1  
  
 Imposta le opzioni che regolano gli aspetti delle connessioni. Questa funzione è parzialmente supportata: il driver supporta tutti i valori per il *fOption* argomento ma non supporta alcuni dei valori *vParam* per il *fOption* argomento SQL_TXN_ISOLATION.  
  
 Nella tabella riportata di seguito vengono descritti solo gli argomenti con comportamento specifico dell'implementazione del driver ODBC di Visual FoxPro di **SQLSetConnectOption**.  
  
|*fOpzione*|Osservazioni|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se si sceglie SQL_AUTOCOMMIT_OFF, l'applicazione deve eseguire in modo esplicito il commit o il rollback delle transazioni con [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); il driver ODBC di Visual FoxPro non esegue automaticamente il commit di un'istruzione transazionale al completamento. Il driver inizia una transazione se l'istruzione è transazionale.|  
|SQL_CURRENT_QUALIFIER|Può essere un nome di [database](../../odbc/microsoft/visual-foxpro-terminology.md) completo o un percorso completo di una directory contenente zero o più [tabelle libere.](../../odbc/microsoft/visual-foxpro-terminology.md)|  
|SQL_LOGINTIMEOUT|Restituisce l'errore "Driver non in grado".|  
|SQL_CURSORS|Restituisce l'errore "Driver non in grado".|  
|SQL_PACKET_SIZE|Restituisce l'errore "Driver non in grado".|  
|SQL_TXN_ISOLATION|Il conducente consente solo SQL_TXN_READ_COMMITTED.<br /><br /> I seguenti *vParam*s non sono supportati:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Per ulteriori informazioni, vedere [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) in *ODBC Programmer's Reference*.
