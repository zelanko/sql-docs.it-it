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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd748884575791d5f170e95bc5aa465b61624b7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299201"
---
# <a name="stored-procedure-parameter-limitations"></a>Limitazioni dei parametri delle stored procedure
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Quando si eseguono stored procedure Oracle che utilizzano 10 o più parametri di output, la chiamata stored procedure avrà esito negativo, causando un errore di violazione di accesso o di ActiveX Data Objects (ADO). Questo problema può verificarsi quando si utilizza Microsoft ODBC driver for Oracle con le versioni 8.0.4.0.0 e 8.0.4.0.4 del software client Oracle.  
  
 Per risolvere il problema, è necessario aggiornare il software client Oracle alla versione 8.0.4.2.0 o successiva. Per ulteriori informazioni sulle [patch](../../odbc/microsoft/oracle-software-patches.md), contattare Oracle Corporation.  
  
> [!NOTE]  
>  Questo problema non si verifica con la versione iniziale della versione del software client Oracle 8.0.3.0.0.
