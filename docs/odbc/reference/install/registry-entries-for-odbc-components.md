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
manager: craigg
ms.openlocfilehash: 3d0a654b70fb93020bbb0dcfde159b4884cb15c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280968"
---
# <a name="registry-entries-for-odbc-components"></a>Voci del Registro di sistema per i componenti ODBC
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows.  Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
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
