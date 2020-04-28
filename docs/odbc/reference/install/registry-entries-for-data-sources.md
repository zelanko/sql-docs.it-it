---
title: Voci del registro di sistema per le origini dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c73ea704b091bc37afb1ac42b520304022d929c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296271"
---
# <a name="registry-entries-for-data-sources"></a>Voci del Registro di sistema per le origini dati
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 La DLL del programma di installazione mantiene le informazioni nel registro di sistema relative a ogni origine dati. In Microsoft Windows NT/Windows 2000 e Microsoft Windows 95/98 queste informazioni vengono archiviate in sottochiavi in una delle due chiavi seguenti del registro di sistema:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 La chiave utilizzata varia a seconda che l'origine dati sia un'origine dati di *sistema,* disponibile per tutti gli utenti, o un' *origine dati utente,* disponibile solo per l'utente corrente. Le origini dati di sistema vengono archiviate nell'albero HKEY_LOCAL_MACHINE e le origini dati dell'utente vengono archiviate nell'albero di HKEY_CURRENT_USER. In tutti gli altri aspetti, le origini dati di sistema e le origini dati utente sono identiche.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Sottochiave ODBC Data Sources](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Sottochiavi di specifica dell'origine dati](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Sottochiave Default](../../../odbc/reference/install/default-subkey.md)  
  
-   [Sottochiave ODBC](../../../odbc/reference/install/odbc-subkey.md)
