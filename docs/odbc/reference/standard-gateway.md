---
title: Gateway Standard Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67551845c0dd8c6a28c0c4bc1c50f54ee8232df1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280074"
---
# <a name="standard-gateway"></a>Gateway standard
Un *gateway* è un software che fa sì che un DBMS assomigli a un altro. Ovvero, il gateway accetta l'interfaccia di programmazione, la grammatica SQL e il protocollo del flusso di dati di un singolo DBMS e lo converte nell'interfaccia di programmazione, nella grammatica SQL e nel protocollo del flusso di dati del sistema DBMS nascosto. Ad esempio, le applicazioni scritte per l'utilizzo di Microsoft® SQL Server™ possono accedere ai dati DB2 anche tramite il gateway Db2 Micro Decisionware; questo prodotto fa sì che DB2 per assomigliare a SQL Server. Quando si utilizzano i gateway, è necessario scrivere un gateway diverso per ogni database di destinazione.  
  
 Sebbene i gateway siano limitati dalle differenze architetturali tra dbM, sono un buon candidato per la standardizzazione. Tuttavia, se tutti i DBMS devono standardizzare l'interfaccia di programmazione, la grammatica SQL e il protocollo del flusso di dati di un singolo DBMS, il cui DBMS deve essere scelto come standard? Certamente nessun fornitore dbMS commerciale è probabile che accetti di standardizzare il prodotto di un concorrente. E se vengono sviluppati un'interfaccia di programmazione standard, la grammatica SQL e il protocollo del flusso di dati, non è necessario alcun gateway.
