---
title: SQLSetConnectOption (Driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071709"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Partial  
  
 Conformità di API ODBC: Livello 1  
  
 Imposta le opzioni che determinano gli aspetti delle connessioni. Questa funzione è supportata parzialmente: Il driver supporta tutti i valori per il *fOption* argomento, ma non supportano alcuni degli *vParam* valori per il *fOption* argomento SQL_TXN_ISOLATION.  
  
 Nella tabella seguente vengono descritte solo quegli argomenti con il comportamento specifico all'implementazione del Driver ODBC Visual FoxPro **SQLSetConnectOption**.  
  
|*fOption*|Note|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se si sceglie SQL_AUTOCOMMIT_OFF, l'applicazione deve esplicitamente eseguire il commit o il rollback delle transazioni con [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); il Driver ODBC Visual FoxPro non esegue automaticamente il commit un'istruzione transactable dopo il completamento. Il driver iniziare una transazione se l'istruzione è transactable.|  
|SQL_CURRENT_QUALIFIER|Può essere un nome completo [database](../../odbc/microsoft/visual-foxpro-terminology.md) nome o percorso completo alla directory contenente zero o più [libero tabelle](../../odbc/microsoft/visual-foxpro-terminology.md).|  
|SQL_LOGINTIMEOUT|Restituisce l'errore "Non è in grado di Driver".|  
|SQL_CURSORS|Restituisce l'errore "Non è in grado di Driver".|  
|SQL_PACKET_SIZE|Restituisce l'errore "Non è in grado di Driver".|  
|SQL_TXN_ISOLATION|Il driver consente solo SQL_TXN_READ_COMMITTED.<br /><br /> Quanto segue *vParam*s non sono supportate:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Per altre informazioni, vedere [SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md) nel *riferimento per programmatori ODBC*.
