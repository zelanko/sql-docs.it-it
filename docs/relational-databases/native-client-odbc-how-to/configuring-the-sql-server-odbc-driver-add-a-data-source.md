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
ms.openlocfilehash: 95fa469c021b345a5c792659998e4f7acbdd493b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939622"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Configurazione del driver ODBC di SQL Server - Aggiungere un'origine dati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Prima di utilizzare le applicazioni ODBC con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive, è necessario essere in grado di aggiornare la versione delle stored procedure del catalogo nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nonché aggiungere, eliminare e testare le origini dati.  
  
  È possibile aggiungere un'origine dati tramite Amministratore ODBC, a livello di programmazione (tramite [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)), o creando un file.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Per aggiungere un'origine dati tramite Amministratore ODBC.  
  
1.  Dal **Pannello di controllo**, accesso **strumenti di amministrazione** e quindi selezionare **origini dati ODBC (64 bit)** o **origini dati ODBC (32 bit)** . In alternativa, è possibile richiamare odbcad32.exe.  
  
2.  Scegliere il **DSN utente**, **DSN di sistema**, o **DSN su File** scheda e quindi fare clic su **Aggiungi**.  
  
3.  Fare clic su **SQL Server**, quindi fare clic su **fine**.  
  
4.  Completare i passaggi nel **creare una nuova origine dati a SQL Server** procedura guidata.  
  
### <a name="to-add-a-data-source-programmatically"></a>Per aggiungere un'origine dati a livello di programmazione  
  
1.  Chiamare [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) con il secondo parametro impostato su ODBC_ADD_DSN o ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Per aggiungere un 'origine dati file  
  
1.  Chiamare [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) con SAVEFILE = nome_file parametro nella stringa di connessione. Se la connessione viene eseguita correttamente, il driver ODBC crea un'origine dati file con i parametri di connessione nel percorso a cui punta il parametro SAVEFILE.  
  
## <a name="see-also"></a>Vedere anche  
[Eliminare un'origine dati &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
