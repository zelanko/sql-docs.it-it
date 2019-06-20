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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 269ab3c748557d1d2870195524310f2371b79c52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62689144"
---
# <a name="bcpcolptr"></a>bcp_colptr
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
 Puntatore ai dati da copiare. Se il tipo di dati associato è il tipo di valori di grandi dimensioni (ad esempio SQLTEXT o SQLIMAGE), *pData* può essere NULL. Un valore NULL *pData* indica i valori di dati long verranno inviati a SQL Server in blocchi mediante [bcp_moretext](bcp-moretext.md).  
  
 Se *pData* è impostata su NULL e la colonna corrispondente al campo associato, non è un tipo di valore elevato **bcp_colptr** ha esito negativo.  
  
 Per altre informazioni sui tipi di valori di grandi dimensioni, vedere [bcp_bind](bcp-bind.md)**.**  
  
 *idxServerCol*  
 Posizione ordinale della colonna nella tabella di database in cui vengono copiati i dati. La prima colonna di una tabella è la colonna 1. La posizione ordinale di una colonna viene indicata da [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 Il **bcp_colptr** funzione consente di modificare l'indirizzo dei dati di origine per una determinata colonna quando si copiano dati da SQL Server con [bcp_sendrow](bcp-sendrow.md).  
  
 Inizialmente, il puntatore ai dati dell'utente viene impostato da una chiamata a **bcp_bind**. Se l'indirizzo di dati della variabile di programma cambia tra le chiamate a **bcp_sendrow**, è possibile chiamare **bcp_colptr** per reimpostare il puntatore ai dati. La chiamata successiva a **bcp_sendrow** invia i dati indirizzati dalla chiamata al metodo **bcp_colptr**.  
  
 Deve essere presente un oggetto separato **bcp_colptr** chiamata per ogni colonna della tabella di indirizzi contenente i dati che si desidera modificare.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
