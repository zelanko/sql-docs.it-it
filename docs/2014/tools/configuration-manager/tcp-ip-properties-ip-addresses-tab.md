---
title: Le proprietà TCP / IP (scheda indirizzi IP) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], listening on
- listening [SQL Server], on ports
ms.assetid: 4c17ed45-9da7-4bec-bce6-970109fe7365
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: afb62458cb76a1187dce06efadeca00fc8a382f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151440"
---
# <a name="tcp-ip-properties-ip-addresses-tab"></a>Proprietà TCP / IP (scheda indirizzi IP)
  La finestra di dialogo **Proprietà TCP/IP** (scheda Indirizzi IP) consente di configurare le opzioni del protocollo TCP/IP per un indirizzo IP specifico. Solo le opzioni **Porte dinamiche TCP** e **Porta TCP** possono essere configurate contemporaneamente per tutti gli indirizzi selezionando **IPAll**.  
  
 Le modifiche hanno effetto dopo il riavvio di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni sull'avvio e arresto del servizio SQL Server Browser, vedere Procedura: Avviare e arrestare il servizio SQL Server Browser nella documentazione Online.  
  
## <a name="static-vs-dynamic-ports"></a>Porte statiche e Porte dinamiche  
 L'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resta in attesa di connessioni in ingresso sulla porta 1433. È possibile cambiare la porta per ragioni di sicurezza oppure per soddisfare i requisiti di un'applicazione client. Per impostazione predefinita, le istanze denominate, incluso SQL Server Express, sono configurate per l'attesa su porte dinamiche. Per configurare una porta statica, lasciare vuota la casella **Porte dinamiche TCP** e fornire un numero di porta disponibile nella casella **Porta TCP** . Per ulteriori informazioni sull'apertura di porte nel firewall, vedere Configurazione di Windows Firewall per consentire l'accesso a SQL Server nella documentazione online.  
  
## <a name="dynamic-ports"></a>Porte dinamiche  
 All'avvio, quando un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurata per restare in attesa sulle porte dinamiche, verifica che nel sistema operativo sia disponibile una porta e apre un endpoint per tale porta. Per eseguire la connessione, le connessioni in ingresso devono specificare il numero di quella porta. Poiché il numero della porta può variare a ogni avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene offerto il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, che esegue il monitoraggio delle porte e indirizza le connessioni in ingresso alla porta corrente per l'istanza. L'utilizzo di porte dinamiche rende più complessa la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite un firewall, poiché il numero di porta può cambiare al riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la conseguente necessità di modificare le impostazioni del firewall. Per evitare problemi di connessione tramite un firewall, configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utilizzo di una porta statica.  
  
## <a name="options"></a>Opzioni  
 **Attiva**  
 Indica che l'indirizzo IP è attivo sul computer. Non disponibile per **IPAll**.  
  
 **Abilitata**  
 Se la proprietà **Attesa su tutti** nella finestra di dialogo **Proprietà TCP/IP** (scheda Protocollo) è impostata su **No**, questa proprietà indica se SQL Server è in attesa sull'indirizzo IP. Se la proprietà **Attesa su tutti** nella finestra di dialogo **Proprietà TCP/IP** (scheda Protocollo) è impostata su **Sì**, questa proprietà viene ignorata. Non disponibile per **IPAll**.  
  
 **Indirizzo IP**  
 Consente di visualizzare o modificare l'indirizzo IP utilizzato per la connessione. Elenca gli indirizzi IP utilizzati dal computer e l'indirizzo IP di loopback, 127.0.0.1. Non disponibile per **IPAll**. L'indirizzo IP può essere in formato IPv4 o IPv6.  
  
 **Porte dinamiche TCP**  
 Se le porte dinamiche non sono abilitate, la casella è vuota. Per attivare le porte dinamiche, impostare su 0.  
  
 Per **IPAll**, visualizza il numero della porta dinamica usata.  
  
 **Porta TCP**  
 Consente di visualizzare o modificare la porta sulla quale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resta in attesa. Per impostazione predefinita, l'istanza predefinita di [!INCLUDE[ssDE](../../includes/ssde-md.md)] resta in attesa sulla porta 1433.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] può restare in attesa su più porte sullo stesso indirizzo IP. Elencare le porte separandole con una virgola, nel formato 1433,1500,1501. La lunghezza massima del campo è 2047 caratteri.  
  
 Per configurare un unico indirizzo IP per l'attesa su più porte è inoltre necessario impostare il parametro **Attesa su tutti** su **No**nella **scheda Protocolli** della finestra di dialogo **Proprietà TCP/IP** . Per altre informazioni, vedere "procedura: Configurare il motore di Database per l'attesa su più porte TCP"in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="adding-or-removing-ip-addresses"></a>Aggiunta o rimozione di indirizzi IP  
 Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] visualizza gli indirizzi IP disponibili al momento dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aggiungendo o modificando schede di rete, alla scadenza di un indirizzo IP assegnato dinamicamente, quando si riconfigura la struttura della rete o quando si sposta fisicamente il computer, ad esempio quando un computer portatile si connette alla rete in un edificio diverso, gli indirizzi IP disponibili cambiano. Per modificare un indirizzo IP, modificare la casella **Indirizzo IP**, quindi riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di un protocollo di rete](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Creazione di una stringa di connessione valida con TCP/IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Servizio SQL Server Browser](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  
