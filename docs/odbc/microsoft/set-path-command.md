---
title: SET PATH (comando) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3d810e66249779b2d3706e92ea39f89a0f87cff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159255"
---
# <a name="set-path-command"></a>SET PATH (comando)
Specifica un percorso per la ricerca di file. Per informazioni specifiche del driver, vedere la sezione Osservazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argomenti  
 TO [ *Path*]  
 Specifica le directory in cui che si desidera eseguire la ricerca di Visual FoxPro. Utilizzare virgole o punti e virgola per separare le directory.  
  
## <a name="remarks"></a>Note  
 SET PATH consente di specificare i percorsi di ricerca per altri programmi Visual FoxPro che possono essere chiamati all'interno di stored procedure. SET PATH non verrà modificato il percorso dell'origine dati specificato per la connessione.  
  
 Imposta percorso a senza emettere *percorso* per ripristinare il percorso di directory o cartella predefinita.  
  
## <a name="driver-remarks"></a>Sezione Osservazioni di driver  
 Se si esegue percorso impostato in una stored procedure, verrà ignorato per i comandi e le funzioni seguenti:  
  
-   Funzioni di catalogo, ad esempio [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) e [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ignorerà il nuovo percorso e continuare a fare riferimento al percorso specificato dall'origine dei dati nelle [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) o[ SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Ignorerà il nuovo percorso e continuare a fare riferimento al percorso specificato dall'origine dei dati in comandi, ad esempio SELECT, INSERT, UPDATE, DELETE e CREATE TABLE **SQLPrepare** oppure **SQLExecDirect**.  
  
 Se si rilascia percorso impostato in una stored procedure e successivamente non imposta il percorso allo stato originale, altre connessioni al database utilizza il nuovo percorso (poiché SET PATH non ha l'ambito per le sessioni di data).  
  
 Se si desidera creare, selezionare o aggiornare le tabelle in una directory diversa da quella specificata dall'origine dati, specificare il percorso completo del file con il comando.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Configurazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Driver ODBC Visual FoxPro)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (driver ODBC Visual FoxPro)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
