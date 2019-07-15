---
title: Protocolli client - Proprietà Named pipe (scheda Protocollo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 1b7b2ce455571b5c588db86b3df6f469dd930e11
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732871"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>Protocolli client - Proprietà - Named pipe (scheda Protocollo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  In Gestione configurazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzare la scheda **Protocollo** della finestra di dialogo delle proprietà **Named Pipes** per visualizzare o modificare la descrizione della pipe predefinita. Per connettersi a una pipe diversa, digitarne il nome nella casella **Pipe predefinita** . Per ulteriori informazioni sulle stringhe di connessione, vedere [Creating a Valid Connection String Using Named Pipes](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f).  
  
## <a name="options"></a>Opzioni  
 **Pipe predefinita**  
 Specifica la pipe predefinita usata dalla libreria di rete Named Pipes per tentare la connessione all'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in ascolto su: `\\.\pipe\sql\query`  
  
 Per connettersi alla pipe predefinita, immettere `sql\query`  
  
 **Abilitata**  
 I valori possibili sono **Sì** e **No**.  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di un protocollo di rete](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
