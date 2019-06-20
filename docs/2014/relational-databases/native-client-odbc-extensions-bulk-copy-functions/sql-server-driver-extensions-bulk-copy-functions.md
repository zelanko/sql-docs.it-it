---
title: Funzioni di copia bulk | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2888f34c1e4c4103845d07e569a0dbabeb2e4caa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225545"
---
# <a name="bulk-copy-functions"></a>Funzioni di copia bulk
  L'estensione API della copia bulk specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client consente alle applicazioni client di aggiungere o di estrarre rapidamente righe di dati in una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando si utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, è possibile fare riferimento alle funzioni di copia bulk (BCP) in SQLNCLI11.LIB e SQLNCLI.H.  
  
 Un'applicazione in cui vengono utilizzate le chiamate alla funzione API BCP dovrebbe essere collegata alla libreria (con estensione lib) fornita con il driver (con estensione dll) utilizzato dall'applicazione. Un'applicazione BCP non dovrebbe essere collegata a più di una libreria del driver.  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [bcp_batch](bcp-batch.md)  
  
-   [bcp_bind](bcp-bind.md)  
  
-   [bcp_colfmt](bcp-colfmt.md)  
  
-   [bcp_collen](bcp-collen.md)  
  
-   [bcp_colptr](bcp-colptr.md)  
  
-   [bcp_columns](bcp-columns.md)  
  
-   [bcp_control](bcp-control.md)  
  
-   [bcp_done](bcp-done.md)  
  
-   [bcp_exec](bcp-exec.md)  
  
-   [bcp_getcolfmt](bcp-getcolfmt.md)  
  
-   [bcp_gettypename](bcp-gettypename.md)  
  
-   [bcp_init](bcp-init.md)  
  
-   [bcp_moretext](bcp-moretext.md)  
  
-   [bcp_readfmt](bcp-readfmt.md)  
  
-   [bcp_sendrow](bcp-sendrow.md)  
  
-   [bcp_setbulkmode](bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](bcp-setcolfmt.md)  
  
-   [bcp_writefmt](bcp-writefmt.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni del Driver SQL Server](../../database-engine/dev-guide/sql-server-driver-extensions.md)   
 [Esecuzione di operazioni di copia Bulk &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
