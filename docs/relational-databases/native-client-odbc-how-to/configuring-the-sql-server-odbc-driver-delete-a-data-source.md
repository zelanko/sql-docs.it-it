---
title: Eliminare un'origine dati (ODBC) | Documenti di Microsoft
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e8c4447413468fe01370ad67c16da0209fcee359
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67584579"
---
# <a name="configuring-the-sql-server-odbc-driver---delete-a-data-source"></a>Configurazione del driver ODBC di SQL Server - Eliminare un'origine dati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Prima di utilizzare le applicazioni ODBC con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive, è necessario essere in grado di aggiornare la versione delle stored procedure del catalogo nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nonché aggiungere, eliminare e testare le origini dati.  
  
  È possibile eliminare un'origine dati tramite Amministratore ODBC, a livello di programmazione (tramite [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)), o eliminando un file (se un nome di origine dati di file).  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>Per eliminare un'origine dati tramite Amministratore ODBC.  
  
1.  Nella **Pannello di controllo**, aprire **strumenti di amministrazione**, quindi fare doppio clic su uno **origini dati ODBC (64 bit)** o **origini dati ODBC (32 bit)** . In alternativa, è possibile eseguire odbcad32.exe dal prompt dei comandi.  
  
2.  Scegliere il **DSN utente**, **DSN di sistema**, o **DSN su File** scheda.  
  
3.  Selezionare l'origine dati da eliminare.  
  
4.  Fare clic su **rimuovere**e quindi confermare l'eliminazione.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="example"></a>Esempio  
 Per eliminare a livello di codice un'origine dati, chiamare [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) utilizzando ODBC_REMOVE_DSN o ODBC_REMOVE_SYS_DSN come secondo parametro.  
  
 Nell'esempio seguente viene illustrato come è possibile eliminare un'origine dati a livello di programmazione.  
  
```  
// remove_odbc_data_source.cpp  
// compile with: ODBCCP32.lib user32.lib  
#include <iostream>  
#include \<windows.h>  
#include \<odbcinst.h>  
  
int main() {   
   LPCSTR provider = "SQL Server";   // Windows SQL Server Driver  
   LPCSTR provider = "SQL Server";   // Windows SQL Server driver  
   LPCSTR provider2 = "SQL Server Native Client 11.0";   // SQL Server 2012 Native Client driver  
   LPCSTR dsnname = "DSN=data2";  
   BOOL retval = SQLConfigDataSource(NULL, ODBC_REMOVE_DSN, provider, dsnname);  
   std::cout << retval;   // 1 if successful  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere un'origine dati &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-add-a-data-source.md)  
  
  
