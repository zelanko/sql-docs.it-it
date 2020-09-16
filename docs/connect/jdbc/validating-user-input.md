---
description: Convalida dell'input utente
title: Convalida dell'input utente | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cbe5ef27b46481eeb32478eaee9866a73ce11802
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450105"
---
# <a name="validating-user-input"></a>Convalida dell'input utente

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando si costruisce un'applicazione che accede ai dati, è necessario presupporre che ogni input utente possa essere dannoso fino a quando non viene dimostrato il contrario. In caso contrario, l'applicazione può essere vulnerabile agli attacchi. Uno tipo di attacco che può verificarsi è detto attacco intrusivo nel codice SQL e in questo tipo di attacco il codice dannoso viene aggiunto a stringhe che successivamente vengono passate a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per essere analizzate ed eseguite. Per evitare questo tipo di attacco, è necessario utilizzare stored procedure con parametri, dove possibile, e convalidare sempre l'input utente.

La convalida dell'input utente nel codice client è importante per evitare di eseguire round trip al server non necessari. È altrettanto importante convalidare i parametri delle stored procedure nel server per intercettare l'input non valido e che ignora la convalida sul lato client.

Per altre informazioni sugli attacchi intrusivi nel codice SQL e su come evitarli, vedere l'argomento relativo a questo tipo di attacchi nella documentazione in linea di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni sulla convalida dei parametri delle stored procedure, vedere "Stored procedure ( [!INCLUDE[ssDE](../../includes/ssde_md.md)] )" e gli argomenti subordinati nella documentazione in linea di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="see-also"></a>Vedere anche

[Protezione delle applicazioni del driver JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)
