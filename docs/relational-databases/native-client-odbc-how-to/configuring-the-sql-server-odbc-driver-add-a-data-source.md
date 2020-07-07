---
title: Aggiungere un'origine dati (ODBC) | Microsoft Docs
description: Viene illustrato come SQL Server driver ODBC chiama stored procedure come stored procedure remote in SQL Server utilizzando il meccanismo di chiamata stored procedure remoto.
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 499ca3cbd3c751e3f5a29260f46a5a4cfe8a6dce
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009530"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Configurazione del driver ODBC di SQL Server - Aggiungere un'origine dati
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Prima di utilizzare le applicazioni ODBC con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive, è necessario essere in grado di aggiornare la versione delle stored procedure del catalogo nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nonché aggiungere, eliminare e testare le origini dati.  
  
  È possibile aggiungere un'origine dati tramite amministratore ODBC, a livello di codice (tramite [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)) o creando un file.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Per aggiungere un'origine dati tramite Amministratore ODBC.  
  
1.  Dal **Pannello di controllo**, accedere a **strumenti di amministrazione** e quindi alle origini dati **ODBC (64 bit)** o alle **origini dati ODBC (32-bit)**. In alternativa, è possibile richiamare odbcad32.exe.  
  
2.  Fare clic sulla scheda **DSN utente**, **DSN di sistema**o **DSN su file** e quindi fare clic su **Aggiungi**.  
  
3.  Fare clic su **SQL Server**, quindi fare clic su **fine**.  
  
4.  Completare i passaggi nella procedura guidata **Crea una nuova origine dati per SQL Server** .  
  
### <a name="to-add-a-data-source-programmatically"></a>Per aggiungere un'origine dati a livello di programmazione  
  
1.  Chiamare [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) con il secondo parametro impostato su ODBC_ADD_DSN o ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Per aggiungere un 'origine dati file  
  
1.  Chiamare [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) con un parametro SAVEFILE = file_name nella stringa di connessione. Se la connessione viene eseguita correttamente, il driver ODBC crea un'origine dati file con i parametri di connessione nel percorso a cui punta il parametro SAVEFILE.  
  
## <a name="see-also"></a>Vedere anche  
[Eliminare un'origine dati &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
