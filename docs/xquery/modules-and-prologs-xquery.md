---
title: Moduli e proregistri (XQuery) | Microsoft Docs
description: Informazioni sulle specifiche non supportate quando si dichiara uno spazio dei nomi in un prologo XQuery.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
author: rothja
ms.author: jroth
ms.openlocfilehash: c7d982e8c944ff1c596dfa4178ce613ec3be709e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759491"
---
# <a name="modules-and-prologs-xquery"></a>Moduli e prologhi (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Il [prologo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) è una serie di dichiarazioni dello spazio dei nomi. Se si dichiara lo spazio dei nomi nel prologo, è possibile specificare l'associazione di un prefisso a uno spazio dei nomi e utilizzare il prefisso nel corpo della query.  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Le specifiche di XQuery seguenti non sono supportate in questa implementazione:  
  
-   Dichiarazione del modulo (`version`)  
  
-   Dichiarazione del modulo (`module namespace`)  
  
-   Xmpspacedeclaration ( `xmlspace` )  
  
-   Dichiarazione delle regole di confronto predefinite (`declare default collation`)  
  
-   Dichiarazione dell'URI di base (`declare base-uri`)  
  
-   Dichiarazione della costruzione (`declare construction`)  
  
-   Dichiarazione dell'ordinamento predefinito (`declare ordering`)  
  
-   Importazione di schema (`import schema namespace`)  
  
-   Importazione di modulo (`import module`)  
  
-   Dichiarazione di variabile nel prologo (`declare variable`)  
  
-   Dichiarazione di funzione (`declare function`)  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Prologo di una query XQuery](../xquery/modules-and-prologs-xquery-prolog.md)  
 Descrive il prologo di una query XQuery.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
