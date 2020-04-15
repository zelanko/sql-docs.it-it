---
title: Transizioni dell'ambiente Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebfb5475d24d5fc70c4cb46a666b2573066565a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283301"
---
# <a name="environment-transitions"></a>Transizioni di ambiente
Gli ambienti ODBC hanno i seguenti tre stati.  
  
|State|Descrizione|  
|-----------|-----------------|  
|E0 (in questo stato del sistema|Ambiente non allocato|  
|E1|Ambiente allocato, connessione non allocata|  
|E2|Ambiente allocato, connessione allocata|  
  
 Nelle tabelle seguenti viene illustrato come ogni funzione ODBC influisce sullo stato dell'ambiente.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH) [2]|E2[5]<br />(HY010) [6]|--[4]|  
|(IH) [3]|(IH)|--[4]|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] La chiamata a **SQLAllocHandle** con *OutputHandlePtr* che punta a un handle valido sovrascrive tale handle. Potrebbe trattarsi di un errore di programmazione dell'applicazione.  
  
 [5] L'attributo SQL_ATTR_ODBC_VERSION'ambiente era stato impostato sull'ambiente.  
  
 [6] L'attributo SQL_ATTR_ODBC_VERSION'ambiente non era stato impostato sull'ambiente.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources e SQLDrivers  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--[1]<br />(HY010) [2]|  
  
 [1] L'attributo SQL_ATTR_ODBC_VERSION dell'ambiente era stato impostato sull'ambiente.  
  
 [2] L'attributo SQL_ATTR_ODBC_VERSION'ambiente non era stato impostato sull'ambiente.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--[3]<br />(HY010) [4]|--[3]<br />(HY010) [4]|  
|(IH) [2]|(IH)|--|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] L'attributo SQL_ATTR_ODBC_VERSION'ambiente era stato impostato sull'ambiente.  
  
 [4] L'attributo SQL_ATTR_ODBC_VERSION'ambiente non era stato impostato sull'ambiente.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|E0 (in questo stato del sistema|(HY010)|  
|(IH) [2]|(IH)|--[4]<br />E1[5]|  
|(IH) [3]|(IH)|--|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 [2] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC.  
  
 [3] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
 [4] C'erano altre maniglie di connessione allocate.  
  
 [5] L'handle di connessione specificato in *Handle* era l'unico handle di connessione allocato.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField e SQLGetDiagRec  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH) [1]|--|--|  
|(IH) [2]|(IH)|--|  
  
 [1] Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_ENV.  
  
 Questa riga mostra le transizioni quando *HandleType* è stato SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr (Informazioni in lingua inglese)  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|--|  
  
 [1] L'attributo SQL_ATTR_ODBC_VERSION dell'ambiente era stato impostato sull'ambiente.  
  
 [2] L'attributo SQL_ATTR_ODBC_VERSION'ambiente non era stato impostato sull'ambiente.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010) [2]|(HY011)|  
  
 [1] L'attributo SQL_ATTR_ODBC_VERSION dell'ambiente era stato impostato sull'ambiente.  
  
 [2] L'argomento *Attributo* non era SQL_ATTR_ODBC_VERSION e l'attributo SQL_ATTR_ODBC_VERSION dell'ambiente non era stato impostato nell'ambiente.  
  
## <a name="all-other-odbc-functions"></a>Tutte le altre funzioni ODBC  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
