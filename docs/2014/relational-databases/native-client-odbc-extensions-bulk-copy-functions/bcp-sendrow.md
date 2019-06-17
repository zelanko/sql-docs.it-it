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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688834"
---
# <a name="bcpsendrow"></a>bcp_sendrow
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
  
## <a name="remarks"></a>Note  
 Il **bcp_sendrow** funzione compila una riga dalle variabili di programma e lo invia a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Prima di chiamare **bcp_sendrow**, è necessario effettuare chiamate al [bcp_bind](bcp-bind.md) per specificare le variabili di programma che contiene i dati di riga.  
  
 Se **bcp_bind** viene chiamato specificando un tipo di dati long a lunghezza variabile, ad esempio, un *eDataType* parametro di SQLTEXT e un valore diverso da null *pData* ,parametro**bcp_sendrow** invia il valore entiredata come avviene per qualsiasi altro tipo di dati. Se, tuttavia **bcp_bind** ha un valore NULL *pData* parametro **bcp_sendrow** restituisce il controllo all'applicazione subito dopo tutte le colonne con i dati specificati vengono inviate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'applicazione può quindi chiamare [bcp_moretext](bcp-moretext.md) ripetutamente per inviare i dati long a lunghezza variabile per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un blocco alla volta. Per altre informazioni, vedere [bcp_moretext](bcp-moretext.md).  
  
 Quando **bcp_sendrow** consente di copia bulk di righe dalle variabili di programma in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle, delle righe viene eseguito solo quando l'utente chiama [bcp_batch](bcp-batch.md) oppure [bcp_done](bcp-done.md) . L'utente può scegliere di chiamare **bcp_batch** una volta ogni *n* righe o quando è presente una pausa nei periodi di dati in ingresso. Se **bcp_batch** viene mai chiamato, le righe vengono eseguito quando **bcp_done** viene chiamato.  
  
 Per informazioni su una sostanziale modifica inizio la copia di massa in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], vedere [esecuzione di operazioni di copia di massa &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
