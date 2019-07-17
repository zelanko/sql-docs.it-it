---
title: Le voci del Registro di sistema per le origini dati | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b9d101395a3276f92f3ccf49e36effc65420f7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093883"
---
# <a name="registry-entries-for-data-sources"></a>Voci del Registro di sistema per le origini dati
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 Il programma di installazione DLL mantiene le informazioni nel Registro di sistema su ogni origine dati. In Microsoft Windows NT o Windows 2000 e Microsoft Windows 95 o 98, queste informazioni vengono archiviate in altra sottochiave di una delle seguenti due chiavi del Registro di sistema:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 Odbc.ini  
  
 HKEY_CURRENT_USER  
  
 SOFTWARE  
  
 ODBC  
  
 Odbc.ini  
  
 La chiave utilizzata dipende dal fatto che l'origine dati è un *origine dati di sistema,* disponibile per tutti gli utenti, o una *origine dati dell'utente,* che è disponibile solo per l'utente corrente. Origini dati di sistema vengono archiviate nell'albero di HKEY_LOCAL_MACHINE e le origini dati utente vengono archiviate nella struttura HKEY_CURRENT_USER. Tutti gli altri aspetti, origini dati di sistema e le origini dati utente sono identiche.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Sottochiave ODBC Data Sources](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Sottochiavi di specifica dell'origine dati](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Sottochiave Default](../../../odbc/reference/install/default-subkey.md)  
  
-   [Sottochiave ODBC](../../../odbc/reference/install/odbc-subkey.md)
