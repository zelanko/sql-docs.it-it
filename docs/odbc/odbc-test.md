---
description: Il test ODBC è un'applicazione abilitata per ODBC che è possibile utilizzare per testare i driver ODBC e gestione driver ODBC.
title: Test ODBC
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC test [ODBC]
- ODBC drivers [ODBC], testing
- gtrtst32.dll
- gtrts32w.dll [ODBC]
- odbct32w.exe [ODBC]
- odbcte32.exe [ODBC]
- testing ODBC drivers [ODBC]
ms.assetid: 7f13894c-5697-436c-be3d-fe16e1a02325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39869fe1230be75d9a76e13b8ba3938ec31ee5ee
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288246"
---
# <a name="odbc-test"></a>Test ODBC

## <a name="about"></a>Informazioni

Microsoft® ODBC test è un'applicazione abilitata per ODBC che è possibile utilizzare per testare i driver ODBC e ODBC driver Manager. Il test ODBC è incluso nell'ambito di [Microsoft Data Access Components (MDAC) 2,8 Software Development Kit](https://www.microsoft.com/download/details.aspx?id=21995).

ODBC 3,51 include le versioni ANSI e abilitate per Unicode del test ODBC. I file corrispondenti sono i seguenti:

- `Odbcte32.exe``Gtrtst32.dll`per la versione ANSI.

- `Odbct32w.exe``Gtrts32w.dll`per la versione Unicode.

Per utilizzare il test ODBC, è necessario conoscere l'API ODBC, il linguaggio C e SQL. Per ulteriori informazioni sull'API ODBC, vedere [ODBC Programmer ' s Reference](../odbc/reference/odbc-programmer-s-reference.md).

Gli argomenti della guida precedentemente inclusi in questa sezione della documentazione sono ora contenuti nel programma di test ODBC. Aprire `Odbcte32.exe` o `Odbct32w.exe` , aprire il menu **Guida** , quindi fare clic su **Guida**.

Si noti che le versioni a 64 bit di queste applicazioni, destinate a sistemi operativi Microsoft Windows a 64 bit, hanno gli stessi nomi delle versioni a 32 bit, anche se si tratta di file distinti. ovvero, il nome della versione Unicode della versione a 64 bit del test ODBC è `odbct32w.exe` .

## <a name="open-source"></a>Open source

Il test ODBC è open source. Per visualizzare il codice e compilare la versione più recente del test ODBC, passare al [repository GitHub per il test ODBC](https://github.com/microsoft/ODBCTest).
