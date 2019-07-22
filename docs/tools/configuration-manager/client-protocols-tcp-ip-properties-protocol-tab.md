---
title: Protocolli client - Proprietà TCP IP (scheda Protocollo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], client protocols
- client protocols [SQL Server]
ms.assetid: d04f1bce-069c-4a02-b561-c87c3282be36
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 81afd532b0bf79e3ea5d9208077fccd474519297
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010209"
---
# <a name="client-protocols---tcp-ip-properties-protocol-tab"></a>Protocolli client - Proprietà TCP IP (scheda Protocolli)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  In Gestione configurazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usare la scheda **Protocollo** della finestra di dialogo **Proprietà TCP/IP** per visualizzare o specificare le opzioni illustrate di seguito. Per eseguire la connessione a una porta diversa, digitare il numero della porta nella casella **Porta predefinita** . Per altre informazioni sulle stringhe di connessione, vedere [Creazione di una stringa di connessione valida tramite TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md).  
  
## <a name="options"></a>Opzioni  
 **Porta predefinita**  
 Specifica la porta utilizzata dalla libreria di rete TCP/IP per tentare la connessione all'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La porta predefinita è la 1433.  
  
 Quando esegue la connessione a un'istanza predefinita di [!INCLUDE[ssDE](../../includes/ssde-md.md)], il client utilizza questo valore. Se un'istanza predefinita è stata configurata per restare in attesa su una porta diversa, modificare il valore della porta impostando 1433.  
  
 Quando esegue la connessione a un'istanza denominata di [!INCLUDE[ssDE](../../includes/ssde-md.md)], il client tenta di ottenere il numero di porta dal servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser in esecuzione nel computer server. Se il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser non è in esecuzione, è necessario fornire il numero di porta mediante questa impostazione o come parte della stringa di connessione.  
  
 **Abilitata**  
 I valori possibili sono **Sì** e **No**.  
  
 **Keep-alive**  
 Questo parametro determina l'intervallo in millisecondi fra i tentativi effettuati da TCP per verificare l'integrità di una connessione inattiva mediante l'invio di un pacchetto **KEEPALIVE** . Il valore predefinito è 30000 millisecondi.  
  
 **Intervallo keep-alive**  
 Questo parametro determina l'intervallo in millisecondi tra le ritrasmissioni **KEEPALIVE** finché non viene ricevuta una risposta. Il valore predefinito è 1000 millisecondi.  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di un protocollo di rete](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Nuovo alias &#40;scheda Alias&#41;](../../tools/configuration-manager/new-alias-alias-tab.md)   
 [Proprietà &#60;Alias&#62; &#40;scheda Alias&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md)  
  
  
