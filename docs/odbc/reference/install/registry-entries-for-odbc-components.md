---
title: Le voci del Registro di sistema per i componenti ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e7adeb2649575b96fbd8dc7101db93ab3332e06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093875"
---
# <a name="registry-entries-for-odbc-components"></a>Voci del Registro di sistema per i componenti ODBC
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 Il programma di installazione DLL mantiene le informazioni nel Registro di sistema su ogni componente ODBC installati. Nei computer che eseguono Microsoft Windows NT e Microsoft Windows 95 o 98, queste informazioni vengono archiviate nelle sottochiavi della chiave del Registro di sistema seguente:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 Odbcinst.ini  
  
 Trattandosi di Odbcinst. ini una sottochiave dell'albero HKEY_LOCAL_MACHINE, le informazioni sui componenti ODBC sono disponibile per tutti gli utenti del computer.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Sottochiave ODBC Core](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [Sottochiave ODBC Drivers](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [Sottochiavi di specifica del driver](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [Sottochiave Default Driver](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [Sottochiave ODBC Translators](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [Sottochiavi di specifica delle funzioni di conversione](../../../odbc/reference/install/translator-specification-subkeys.md)
