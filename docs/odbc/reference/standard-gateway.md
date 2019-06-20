---
title: Gateway standard | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c70a558b065765dd9f8c0895345959e8aa22ebfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232090"
---
# <a name="standard-gateway"></a>Gateway standard
Oggetto *gateway* è un componente software che provoca un DBMS simile a un altro. Vale a dire, il gateway accetta l'interfaccia di programmazione, grammatica SQL e protocollo di DBMS singolo del flusso di dati e lo converte per l'interfaccia di programmazione, grammatica SQL, e protocollo del sistema DBMS nascosto del flusso di dati. Ad esempio, le applicazioni scritte per l'utilizzo di Microsoft® SQL Server™ accessibile anche dati DB2 tramite il Gateway di DB2 Decisionware Micro; Questo prodotto provoca DB2 simile a SQL Server. Quando i gateway vengono usati, un altro gateway deve essere scritto per ogni database di destinazione.  
  
 Anche se i gateway sono limitati dalle differenze di architettura tra DBMS, sono un buon candidato per la standardizzazione. Tuttavia, se tutti i DBMS sono di standardizzare l'interfaccia di programmazione, grammatica SQL e dati protocollo del flusso di un singolo DBMS cui DBMS è necessario scegliere come standard? Certamente non commerciale fornitore DBMS è probabile che accettano di standardizzare il prodotto. E se un'interfaccia di programmazione standard, grammatica SQL e il protocollo di flusso di dati vengono sviluppate, non è necessario alcun gateway.
