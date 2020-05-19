---
title: bcp_colptr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colptr
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 38e4b2590bebd09da764e6249e59d32b0c28d356
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705305"
---
# <a name="bcp_colptr"></a>bcp_colptr
  Imposta l'indirizzo dei dati della variabile di programma per la copia corrente su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_colptr (  
HDBC   
hdbc  
,  
LPCBYTE   
pData  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *pData*  
 Puntatore ai dati da copiare. Se il tipo di dati associato è un tipo di valore di grandi dimensioni, ad esempio SQLTEXT o SQLIMAGE, *pData* può essere null. Un valore NULL *pData* indica che i valori di dati Long verranno inviati a SQL Server in blocchi utilizzando [bcp_moretext](bcp-moretext.md).  
  
 Se *pData* è impostato su null e la colonna corrispondente al campo associato non è un tipo di valore di grandi dimensioni, **bcp_colptr** ha esito negativo.  
  
 Per ulteriori informazioni sui tipi di valore di grandi dimensioni, vedere [bcp_bind](bcp-bind.md)**.**  
  
 *idxServerCol*  
 Posizione ordinale della colonna nella tabella di database in cui vengono copiati i dati. La prima colonna di una tabella è la colonna 1. La posizione ordinale di una colonna viene segnalata da [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Restituisce  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **bcp_colptr** consente di modificare l'indirizzo dei dati di origine per una determinata colonna durante la copia dei dati in SQL Server con [bcp_sendrow](bcp-sendrow.md).  
  
 Inizialmente, il puntatore ai dati utente viene impostato da una chiamata a **bcp_bind**. Se l'indirizzo dei dati della variabile di programma cambia tra le chiamate a **bcp_sendrow**, è possibile chiamare **bcp_colptr** per reimpostare il puntatore ai dati. La chiamata successiva a **bcp_sendrow** invia i dati indirizzati dalla chiamata al **bcp_colptr**.  
  
 Deve essere presente una chiamata di **bcp_colptr** separata per ogni colonna della tabella di cui si desidera modificare l'indirizzo dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
