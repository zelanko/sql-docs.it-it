---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_sendrow
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e8ef7aa7a4354f5a3fbc334504512b2ee8d131b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62688834"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
  Invia una riga di dati dalle variabili di programma a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **bcp_sendrow** compila una riga dalle variabili di programma e la invia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a.  
  
 Prima di chiamare **bcp_sendrow**, è necessario effettuare chiamate a [bcp_bind](bcp-bind.md) per specificare le variabili di programma contenenti i dati delle righe.  
  
 Se **bcp_bind** viene chiamato specificando un tipo di dati Long a lunghezza variabile, ad esempio un parametro *EDATATYPE* di SQLTEXT e un parametro *pData* non null, **bcp_sendrow** invierà il valore entiredata, proprio come per qualsiasi altro tipo di dati. Se, tuttavia, **bcp_bind** dispone di un parametro *pData* null, **bcp_sendrow** restituisce il controllo all'applicazione immediatamente dopo l'invio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tutte le colonne con i dati specificati. L'applicazione può quindi chiamare ripetutamente [bcp_moretext](bcp-moretext.md) per inviare i dati Long a lunghezza variabile a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un blocco alla volta. Per ulteriori informazioni, vedere [bcp_moretext](bcp-moretext.md).  
  
 Quando **bcp_sendrow** viene utilizzata per eseguire la copia bulk delle righe dalle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] variabili di programma alle tabelle, viene eseguito il commit delle righe solo quando l'utente chiama [bcp_batch](bcp-batch.md) o [bcp_done](bcp-done.md). L'utente può scegliere di chiamare **bcp_batch** una volta ogni *n* righe o quando si verifica una pausa tra i periodi di dati in arrivo. Se **bcp_batch** non viene mai chiamato, viene eseguito il commit delle righe quando viene chiamato **bcp_done** .  
  
 Per informazioni sulle modifiche di rilievo apportate alla copia bulk [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]a partire da, vedere [esecuzione di operazioni di copia bulk &#40;&#41;ODBC ](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
