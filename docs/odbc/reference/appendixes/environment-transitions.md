---
title: Transizioni di ambiente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ed2bbf40ac333db34d3920b2ed2ec688c344bfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63189003"
---
# <a name="environment-transitions"></a>Transizioni di ambiente
ODBC presenta i seguenti tre stati.  
  
|State|Descrizione|  
|-----------|-----------------|  
|E0|Ambiente non allocato|  
|E1|Ambiente allocato, non allocato connessione|  
|E2|Ambiente di connessione allocato allocata|  
  
 Le tabelle seguenti mostrano come ogni funzione ODBC riguarda lo stato dell'ambiente.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH)[2]|E2[5]<br />(HY010)[6]|--[4]|  
|(IH)[3]|(IH)|--[4]|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] chiamante **SQLAllocHandle** con *OutputHandlePtr* che punta a un handle valido sovrascrive tale handle. Potrebbe trattarsi di un errore di programmazione dell'applicazione.  
  
 [5] l'attributo di ambiente SQL_ATTR_ODBC_VERSION era stata impostata nell'ambiente.  
  
 [6] l'attributo di ambiente SQL_ATTR_ODBC_VERSION non era stato impostato sull'ambiente.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [1] l'attributo di ambiente SQL_ATTR_ODBC_VERSION era stata impostata nell'ambiente.  
  
 [2] l'attributo di ambiente SQL_ATTR_ODBC_VERSION non era stato impostato sull'ambiente.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(IH)[2]|(IH)|--|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] l'attributo di ambiente SQL_ATTR_ODBC_VERSION era stato impostato sull'ambiente.  
  
 [4] attributo l'ambiente SQL_ATTR_ODBC_VERSION non era stato impostato sull'ambiente.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|E0|(HY010)|  
|(IH)[2]|(IH)|--[4]<br />E1[5]|  
|(IH)[3]|(IH)|--|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DBC.  
  
 [3] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] si sono verificati altri handle di connessione allocato.  
  
 [5] l'handle di connessione specificato nel *gestire* era l'handle di connessione allocato solo.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagRec e SQLGetDiagField  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--|--|  
|(IH)[2]|(IH)|--|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_ENV.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--|  
  
 [1] l'attributo di ambiente SQL_ATTR_ODBC_VERSION era stata impostata nell'ambiente.  
  
 [2] l'attributo di ambiente SQL_ATTR_ODBC_VERSION non era stato impostato sull'ambiente.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|(HY011)|  
  
 [1] l'attributo di ambiente SQL_ATTR_ODBC_VERSION era stata impostata nell'ambiente.  
  
 [2] il *attributo* argomento non era SQL_ATTR_ODBC_VERSION e l'attributo di ambiente SQL_ATTR_ODBC_VERSION non era stato impostato sull'ambiente.  
  
## <a name="all-other-odbc-functions"></a>Tutte le altre funzioni ODBC  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
