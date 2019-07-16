---
title: Supporto per colonne di tipo sparse (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bd4c9321b0d8ae841fe3f099870d65b87a1f95b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913145"
---
# <a name="sparse-columns-support-odbc"></a>Supporto per colonne di tipo sparse (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In questo argomento viene descritto il supporto ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per le colonne di tipo sparse. Per un esempio che illustra il supporto ODBC per colonne di tipo sparse, vedere [chiamare SQLColumns in una tabella con colonne di tipo Sparse](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md). Per altre informazioni sulle colonne di tipo sparse, vedere [supporto per colonne di tipo Sparse in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md).  
  
## <a name="statement-metadata"></a>Metadati di istruzione  
 Il campo di descrizione del parametro dell'applicazione (APD) e l'attributo dell'istruzione SQL_SOPT_SS_NAME_SCOPE accettano i valori aggiuntivi SQL_SS_NAME_SCOPE_EXTENDED e SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET. Questi valori specificano quali colonne sono incluse nel set di risultati restituito da [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md). Per altre informazioni su SQL_SOPT_SS_NAME_SCOPE, vedere [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Un nuovo descrittore riga di implementazione (IRD), un campo SQLSMALLINT di sola lettura denominato SQL_CA_SS_IS_COLUMN_SET, può essere utilizzato per determinare se una colonna è un file XML **column_set** valore. SQL_CA_SS_IS_COLUMN_SET accetta i valori SQL_TRUE e SQL_FALSE.  
  
## <a name="catalog-metadata"></a>Metadati del catalogo  
 Due [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] colonne specifiche (SS_IS_SPARSE e SS_IS_COLUMN_SET) sono stati aggiunti al set di risultati [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="odbc-function-support-for-sparse-columns"></a>Supporto della funzione ODBC per colonne di tipo sparse  
 Sono state aggiornate le funzioni ODBC seguenti per supportare colonne di tipo sparse in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
