---
title: Comando SET PATH Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e44093c3ea18bc995264a8974726f5af0abe3b3a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300821"
---
# <a name="set-path-command"></a>SET PATH (comando)
Specifica un percorso per le ricerche di file. Per informazioni specifiche del driver, vedere la pagina Osservazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argomenti  
 TO [ *Percorso*]  
 Specifica le directory in cui si desidera che Visual FoxPro eseda. Utilizzare virgole o punti e virgola per separare le directory.  
  
## <a name="remarks"></a>Osservazioni  
 SET PATH consente di specificare percorsi di ricerca per altri programmi Visual FoxPro che possono essere chiamati all'interno di stored procedure. SET PATH non modificherà il percorso dell'origine dati specificata per la connessione.  
  
 Problema SET PATH TO senza *Percorso* per ripristinare il percorso della directory o della cartella predefinita.  
  
## <a name="driver-remarks"></a>Osservazioni del conducente  
 Se si rilascia SET PATH in una stored procedure, verrà ignorato dalle funzioni e dai comandi seguenti:  
  
-   Le funzioni di catalogo, ad esempio [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) e [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ignoreranno il nuovo percorso e continueranno a fare riferimento al percorso specificato dall'origine dati in [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) o [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Comandi quali SELECT, INSERT, UPDATE, DELETE e CREATE TABLE ignoreranno il nuovo percorso e continueranno a fare riferimento al percorso specificato dall'origine dati in **SQLPrepare** o **SQLExecDirect**.  
  
 Se si rilascia SET PATH in una stored procedure e successivamente non si imposta il percorso allo stato originale, altre connessioni al database utilizzeranno il nuovo percorso (poiché SET PATH non ha come ambito le sessioni dati).  
  
 Se si desidera creare, selezionare o aggiornare tabelle in una directory diversa da quella specificata dall'origine dati, specificare il percorso completo del file con il comando.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Installazione di ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (driver ODBC di Visual FoxPro)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (driver ODBC di Visual FoxPro)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (driver ODBC Visual FoxPro)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
