---
title: Mapping di SQLInstallTranslator Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ab5ebccaac7ccf6374971c1d21040ad15fb3e55
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300583"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapping di SQLInstallTranslator
Quando un'applicazione ODBC *2.x* chiama **SQLInstallTranslator** tramite un driver ODBC *3.x,* Gestione Driver esegue il mapping della chiamata a **SQLInstallTranslatorEx**. Un'applicazione non deve chiamare **SQLInstallTranslator** in Gestione Driver ODBC *3.x* con l'argomento *lpszInfFile* impostato su un valore diverso da NULL. Il file ODBC. Il file INF utilizzato in ODBC *2.x* non è più supportato in ODBC *3.x*, anche per compatibilità con le versioni precedenti.
