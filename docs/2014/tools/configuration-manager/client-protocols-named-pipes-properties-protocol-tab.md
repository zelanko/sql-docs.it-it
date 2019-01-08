---
title: Protocolli client - Proprietà Named pipe (scheda Protocollo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fe7bb05afc8e0814ddb3d872a810759aae2a678
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52746844"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>Protocolli client - Proprietà - Named pipe (scheda Protocollo)
  In Gestione configurazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzare la scheda **Protocollo** della finestra di dialogo delle proprietà **Named Pipes** per visualizzare o modificare la descrizione della pipe predefinita. Per connettersi a una pipe diversa, digitarne il nome nella casella **Pipe predefinita** . Per ulteriori informazioni sulle stringhe di connessione, vedere [Creazione di una stringa di connessione valida tramite named pipe](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md).  
  
## <a name="options"></a>Opzioni  
 **Pipe predefinita**  
 Specifica la pipe predefinita usata dalla libreria di rete Named Pipes per tentare la connessione all'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in ascolto su: `\\.\pipe\sql\query`  
  
 Per connettersi alla pipe predefinita, immettere `sql\query`  
  
 **Abilitata**  
 I valori possibili sono **Sì** e **No**.  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di un protocollo di rete](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
