---
title: Aggiungere un'origine dati (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 784c08ea9a251587d156de9f2d209308c6fda5e7
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73781694"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Configurazione del driver ODBC di SQL Server - Aggiungere un'origine dati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Prima di utilizzare le applicazioni ODBC con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive, è necessario essere in grado di aggiornare la versione delle stored procedure del catalogo nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nonché aggiungere, eliminare e testare le origini dati.  
  
  È possibile aggiungere un'origine dati tramite amministratore ODBC, a livello di codice (tramite [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)) o creando un file.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Per aggiungere un'origine dati tramite Amministratore ODBC.  
  
1.  Dal **Pannello di controllo**, accedere a **strumenti di amministrazione** e quindi alle origini dati **ODBC (64 bit)** o alle **origini dati ODBC (32-bit)** . In alternativa, è possibile richiamare odbcad32.exe.  
  
2.  Fare clic sulla scheda **DSN utente**, **DSN di sistema**o **DSN su file** e quindi fare clic su **Aggiungi**.  
  
3.  Fare clic su **SQL Server**, quindi fare clic su **fine**.  
  
4.  Completare i passaggi nella procedura guidata **Crea una nuova origine dati per SQL Server** .  
  
### <a name="to-add-a-data-source-programmatically"></a>Per aggiungere un'origine dati a livello di programmazione  
  
1.  Chiamare [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) con il secondo parametro impostato su ODBC_ADD_DSN o ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Per aggiungere un 'origine dati file  
  
1.  Chiamare [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) con un parametro SAVEFILE = file_name nella stringa di connessione. Se la connessione viene eseguita correttamente, il driver ODBC crea un'origine dati file con i parametri di connessione nel percorso a cui punta il parametro SAVEFILE.  
  
## <a name="see-also"></a>Vedere anche  
[Eliminare un'origine &#40;dati ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
