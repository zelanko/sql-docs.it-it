---
title: Metadati del parametro con valori di tabella per le istruzioni preparate | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43ef41affecd131626da17ec7d608249437abed6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62626515"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>Metadati del parametro con valori di tabella per le istruzioni preparate
  Un'applicazione può ottenere i metadati per una chiamata di procedura preparata tramite SQLNumParams e SQLDescribeParam. Per i parametri con valori di tabella, *DataTypePTR* è impostato su SQL_SS_TABLE. I metadati aggiuntivi sono disponibili tramite SQLGetDescField per SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME.  
  
 È possibile utilizzare SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME con SQLColumns per ottenere i metadati della colonna per i tipi di tabella associati ai parametri con valori di tabella. In questo caso, SQL_SOPT_SS_NAME_SCOPE necessario impostare su SQL_SS_NAME_SCOPE_TABLE_TYPE prima di chiamare SQLColumns. Impostare nuovamente SQL_SOPT_SS_NAME_SCOPE sul valore predefinito SQL_SS_NAME_SCOPE_TABLE al termine del recupero dei metadati della colonna per i parametri con valori di tabella.  
  
 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME e SQL_CA_SS_SCHEMA_NAME possono inoltre essere utilizzati con i parametri dei tipi CLR definiti dall'utente.  
  
 Non è possibile ottenere i metadati del parametro con valori di tabella per istruzioni preparate che non siano chiamate a stored procedure. Se si tenta di eseguire questa operazione, l'applicazione restituisce SQL_ERROR con SQLSTATE 42000 e il messaggio indicante un errore di sintassi o una violazione dell'accesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;&#41;ODBC](table-valued-parameters-odbc.md)  
  
  
