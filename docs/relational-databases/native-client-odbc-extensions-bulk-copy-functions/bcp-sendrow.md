---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5bc7b03405d6e43a6b19cc2903875685177942e1
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707529"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Invia una riga di dati dalle variabili di programma a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 La funzione **bcp_sendrow** compila una riga dalle variabili di programma e la invia a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Prima di chiamare **bcp_sendrow**, è necessario effettuare chiamate a [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) per specificare le variabili di programma contenenti i dati delle righe.  
  
 Se **bcp_bind** viene chiamato specificando un tipo di dati Long a lunghezza variabile, ad esempio un parametro *EDATATYPE* di SQLTEXT e un parametro *pData* non null, **bcp_sendrow** invia l'intero valore dei dati, così come accade per qualsiasi altro dato. tipo. Se, tuttavia, **bcp_bind** ha un parametro *pData* null, **bcp_sendrow** restituisce il controllo all'applicazione immediatamente dopo l'invio di tutte le colonne con dati specificati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'applicazione può quindi chiamare [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) ripetutamente per inviare i dati Long a lunghezza variabile a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un blocco alla volta. Per ulteriori informazioni, vedere [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md).  
  
 Quando **bcp_sendrow** viene utilizzato per eseguire la copia bulk delle righe dalle variabili di programma in tabelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], viene eseguito il commit delle righe solo quando l'utente chiama [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) o [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md). L'utente può scegliere di chiamare **bcp_batch** una volta ogni *n* righe o quando si verifica una pausa tra i periodi di dati in arrivo. Se **bcp_batch** non viene mai chiamato, viene eseguito il commit delle righe quando viene chiamato **bcp_done** .  
  
 Per informazioni sulle modifiche di rilievo apportate alla copia bulk a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], vedere [esecuzione &#40;di&#41;operazioni di copia bulk ODBC](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
