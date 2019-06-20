---
title: Proprietà - Configurazione SQL Server Native Client (scheda Flag) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bf95081d3c4657dd147e06ae54d413dd96c4c18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028302"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>Proprietà - Configurazione SQL Server Native Client (scheda Flag)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in questo computer comunicano con i server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite i protocolli disponibili nel file della libreria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Questa scheda consente di configurare il computer client in modo che richieda una connessione crittografata mediante SSL (Secure Sockets Layer). Se non è possibile ottenere una connessione crittografata, la connessione non viene stabilita.  
  
 Il processo di accesso viene sempre crittografato. Le opzioni riportate di seguito si applicano solo a dati crittografati. Per altre informazioni su come [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue la crittografia delle comunicazioni e per istruzioni su come configurare il client per considerare attendibile l'autorità radice del certificato del server, vedere "Crittografia delle connessioni a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" e "Procedura: Attivazione di connessioni crittografate al [!INCLUDE[ssDE](../../includes/ssde-md.md)] (Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opzioni  
 **ForceEncryption**  
 Richiede una connessione mediante SSL.  
  
 **TrustServerCertificate**  
 Se è impostato su **No**, il processo client tenta di convalidare il certificato server. Sia il client che il server devono disporre di un certificato emesso da un'autorità di certificazione pubblica. Se il certificato non è presente nel computer client o se non viene convalidato, la connessione viene terminata.  
  
 Se è impostato su **Sì**, il client non convalida il certificato server e pertanto consente di usare un certificato autofirmato.  
  
 **Certificato server attendibile** è disponibile solo se **Forza crittografia protocollo** è impostato su **Sì**.  
  
  
