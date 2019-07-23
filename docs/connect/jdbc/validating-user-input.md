---
title: Convalida dell'input utente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2d890c4471dfeb85c1dd4f8f6f614a3b28cff90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003902"
---
# <a name="validating-user-input"></a>Convalida dell'input utente

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando si costruisce un'applicazione che accede ai dati, è necessario presupporre che ogni input utente possa essere dannoso fino a quando non viene dimostrato il contrario. In caso contrario, l'applicazione può essere vulnerabile agli attacchi. Uno tipo di attacco che può verificarsi è detto attacco intrusivo nel codice SQL e in questo tipo di attacco il codice dannoso viene aggiunto a stringhe che successivamente vengono passate a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per essere analizzate ed eseguite. Per evitare questo tipo di attacco, è necessario utilizzare stored procedure con parametri, dove possibile, e convalidare sempre l'input utente.

La convalida dell'input utente nel codice client è importante per evitare di eseguire round trip al server non necessari. È altrettanto importante convalidare i parametri delle stored procedure nel server per intercettare l'input non valido e che ignora la convalida sul lato client.

Per altre informazioni sugli attacchi intrusivi nel codice SQL e su come evitarli, vedere l'argomento relativo a questo tipo di attacchi nella documentazione in linea di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni sulla convalida dei parametri delle stored procedure, vedere "Stored procedure ( [!INCLUDE[ssDE](../../includes/ssde_md.md)] )" e gli argomenti subordinati nella documentazione in linea di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="see-also"></a>Vedere anche

[Protezione delle applicazioni del driver JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)
