---
title: Configurare un Server per l'ascolto su una Pipe alternativa (Gestione configurazione SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- listening [SQL Server], pipes
- pipes [SQL Server], alternate
- alternate pipes [SQL Server]
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 68b082d125650d150676d545cfdf6ab27bd25da2
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640459"
---
# <a name="configure-a-server-to-listen-on-an-alternate-pipe-sql-server-configuration-manager"></a>Configurazione di un server per l'attesa su una pipe alternativa (Gestione configurazione SQL Server)
  In questo argomento viene illustrato come configurare un server per l'ascolto su una pipe alternativa in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando Gestione configurazione SQL Server. Per impostazione predefinita, l'istanza predefinita di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] è in attesa sulla named pipe \\\\.\pipe\sql\query. Le istanze denominate del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e [!INCLUDE[ssEW](../../includes/ssew-md.md)] sono in attesa su altre pipe.  
  
 È possibile connettersi a una named pipe specifica mediante un'applicazione client in tre modi differenti:  
  
-   Avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser sul server.  
  
-   Creare un alias nel client, specificando la named pipe.  
  
-   Programmare il client affinché si connetta utilizzando una stringa di connessione personalizzata.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-configure-the-named-pipe-used-by-the-sql-server-database-engine"></a>Per configurare l'utilizzo della named pipe mediante il Motore di database di SQL Server  
  
1.  Nel riquadro della console di Gestione configurazione SQL Server, espandere **Configurazione di rete SQL Server** e **Protocolli per** *\<nome istanza>*.  
  
2.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Named pipe**, quindi scegliere **Proprietà**.  
  
3.  Nel riquadro **Nome pipe** della scheda **Protocollo** , specificare la pipe su cui si desidera che il [!INCLUDE[ssDE](../../includes/ssde-md.md)] sia in attesa e quindi fare clic su **OK**.  
  
4.  Nel riquadro della console fare clic su **Servizi di SQL Server**.  
  
5.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **SQL Server (**\<<nome istanza>**)** e scegliere **Riavvia**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà arrestato e riavviato.  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in attesa su una pipe alternativa, è possibile connettersi a una named pipe specifica mediante un'applicazione client in tre modi differenti:  
  
-   Avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser sul server.  
  
-   Creare un alias nel client, specificando la named pipe.  
  
-   Programmare il client affinché si connetta utilizzando una stringa di connessione personalizzata.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare o eliminare un alias server per l'uso da parte di un client &#40;Gestione configurazione SQL Server Manager&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [Configurazione di rete del server](server-network-configuration.md)  
  
  
