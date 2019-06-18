---
title: SQLGetConnectOption (Driver ODBC Visual FoxPro) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 62f1033abeaa32499602534f7f43b17fefe55ce9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313183"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Partial  
  
 Conformità di API ODBC: Livello 1  
  
 Restituisce l'impostazione corrente dell'opzione di connessione. Questa funzione è supportata parzialmente: Il driver supporta tutti i valori per il *fOption* argomento, ma non supportano alcuni degli *vParam* valori per il *fOption* argomento SQL_TXN_ISOLATION.  
  
 Nella tabella seguente vengono descritte solo quegli argomenti con il comportamento specifico all'implementazione del Driver ODBC Visual FoxPro **SQLGetConnectOption**.  
  
|*fOption*|Note|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|Se si sceglie SQL_AUTOCOMMIT_OFF, l'applicazione deve esplicitamente eseguire il commit o il rollback delle transazioni con [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md); il Driver ODBC Visual FoxPro non esegue automaticamente il commit un'istruzione transactable dopo il completamento. Il driver iniziare una transazione se l'istruzione è transactable.|  
|SQL_CURRENT_QUALIFIER|Può essere un nome completo del database (file DBC) o il percorso completo di una directory che contiene zero o più tabelle (file con estensione dbf).|  
|SQL_LOGINTIMEOUT|Restituisce l'errore "Driver non è in grado".|  
|SQL_CURSORS|Restituisce l'errore "Driver non è in grado".|  
|SQL_PACKET_SIZE|Restituisce l'errore "Driver non è in grado".|  
|SQL_TXN_ISOLATION|Il driver consente solo SQL_TXN_READ_COMMITTED.<br /><br /> Quanto segue *vParam*s non sono supportate:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 Per altre informazioni, vedere [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) nel *riferimento per programmatori ODBC*.
