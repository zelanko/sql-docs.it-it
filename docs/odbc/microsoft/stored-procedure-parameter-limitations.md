---
title: Limitazioni del parametro della stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f1c5a18eb9f0b1939a2c3602f1ebe7695741f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948820"
---
# <a name="stored-procedure-parameter-limitations"></a>Limitazioni dei parametri delle stored procedure
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Quando si eseguono stored procedure Oracle che utilizzano 10 o più parametri di output, la chiamata stored procedure avrà esito negativo, causando un errore di violazione di accesso o di ActiveX Data Objects (ADO). Questo problema può verificarsi quando si utilizza Microsoft ODBC driver for Oracle con le versioni 8.0.4.0.0 e 8.0.4.0.4 del software client Oracle.  
  
 Per risolvere il problema, è necessario aggiornare il software client Oracle alla versione 8.0.4.2.0 o successiva. Per ulteriori informazioni sulle [patch](../../odbc/microsoft/oracle-software-patches.md), contattare Oracle Corporation.  
  
> [!NOTE]  
>  Questo problema non si verifica con la versione iniziale della versione del software client Oracle 8.0.3.0.0.
