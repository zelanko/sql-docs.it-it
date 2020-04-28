---
title: SQLExtendedFetch (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ecff538198a2b517f980cc63acfc97d29a9f162
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298651"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello 2  
  
 Simile a [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ma restituisce più righe usando una matrice per ogni colonna. Il set di risultati è scorrevole per lo scorrimento avanti e può essere reso di scorrimento a ritroso se il cursore è definito come statico, non solo in avanti.  
  
 Per impostazione predefinita, il driver ODBC Visual FoxPro non restituisce righe contrassegnate come eliminate in una tabella di FoxPro. Le righe contrassegnate per l'eliminazione ma non ancora rimosse da una tabella non sono incluse nel cursore del set di risultati. È possibile modificare questo comportamento usando il comando [set Deleted](../../odbc/microsoft/set-deleted-command.md) .  
  
 Per ulteriori informazioni, vedere [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) in *ODBC Programmer ' s Reference*.
