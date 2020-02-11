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
ms.openlocfilehash: 6b1de2f2147357f9e2ed4f71657b9298c4a13684
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910429"
---
# <a name="environment-transitions"></a>Transizioni di ambiente
Negli ambienti ODBC sono disponibili i tre stati seguenti.  
  
|State|Descrizione|  
|-----------|-----------------|  
|E0|Ambiente non allocato|  
|E1|Ambiente allocato, connessione non allocata|  
|E2|Ambiente allocato, connessione allocata|  
  
 Nelle tabelle seguenti viene illustrato il modo in cui ogni funzione ODBC influiscono sullo stato dell'ambiente.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|IH 2|E2 [5]<br />HY010 6|--[4]|  
|IH 3|IH|--[4]|  
  
 [1] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] la chiamata a **SQLAllocHandle** con *OutputHandlePtr* che punta a un handle valido sovrascrive tale handle. Potrebbe trattarsi di un errore di programmazione dell'applicazione.  
  
 [5] l'attributo dell'ambiente SQL_ATTR_ODBC_VERSION è stato impostato sull'ambiente.  
  
 [6] l'attributo SQL_ATTR_ODBC_VERSION Environment non è stato impostato sull'ambiente.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|E0<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|IH|--[1]<br />HY010 2|--[1]<br />HY010 2|  
  
 [1] l'attributo dell'ambiente SQL_ATTR_ODBC_VERSION è stato impostato sull'ambiente.  
  
 [2] l'attributo SQL_ATTR_ODBC_VERSION Environment non è stato impostato sull'ambiente.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|IH 1|--[3]<br />HY010 4|--[3]<br />HY010 4|  
|IH 2|IH|--|  
  
 [1] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] l'attributo dell'ambiente SQL_ATTR_ODBC_VERSION è stato impostato sull'ambiente.  
  
 [4] l'attributo SQL_ATTR_ODBC_VERSION Environment non è stato impostato sull'ambiente.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|IH 1|E0|HY010|  
|IH 2|IH|--[4]<br />E1 [5]|  
|IH 3|IH|--|  
  
 [1] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] sono presenti altri handle di connessione allocati.  
  
 [5] l'handle di connessione specificato nell' *handle* è l'unico handle di connessione allocato.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|E0<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|IH 1|--|--|  
|IH 2|IH|--|  
  
 [1] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga Mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|IH|--[1]<br />HY010 2|--|  
  
 [1] l'attributo dell'ambiente SQL_ATTR_ODBC_VERSION è stato impostato sull'ambiente.  
  
 [2] l'attributo SQL_ATTR_ODBC_VERSION Environment non è stato impostato sull'ambiente.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|IH|--[1]<br />HY010 2|Hy011|  
  
 [1] l'attributo dell'ambiente SQL_ATTR_ODBC_VERSION è stato impostato sull'ambiente.  
  
 [2] l'argomento dell' *attributo* non è stato SQL_ATTR_ODBC_VERSION e l'attributo dell'ambiente SQL_ATTR_ODBC_VERSION non è stato impostato sull'ambiente.  
  
## <a name="all-other-odbc-functions"></a>Tutte le altre funzioni ODBC  
  
|E0<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|IH|IH|--|
