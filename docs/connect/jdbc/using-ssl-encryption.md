---
description: Uso della crittografia
title: Uso della crittografia
ms.custom: Learn how to establish secure communication channels using TLS encryption with your SQL database connections.
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86a36cec5930630c00501796e9c2340106cfa6c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414577"
---
# <a name="using-encryption"></a>Uso della crittografia

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La crittografia TLS (Transport Layer Security) consente la trasmissione di dati crittografati attraverso la rete tra un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e un'applicazione client.  
  
TLS (Transport Layer Security) è un protocollo che consente di stabilire un canale di comunicazione sicuro per impedire l'intercettazione di informazioni critiche o riservate attraverso la rete e altre comunicazioni Internet. TLS consente al client e al server di autenticare l'identità reciproca. Dopo che i partecipanti sono stati autenticati, TLS fornisce connessioni crittografate tra di essi per una trasmissione sicura dei messaggi.  
  
In [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è disponibile un'infrastruttura per abilitare e disabilitare la crittografia in una particolare connessione in base alle proprietà di connessione specificate dall'utente e alle impostazioni server e client. L'utente può specificare il percorso e la password dell'archivio certificati, un nome host da utilizzare per convalidare il certificato e quando crittografare il canale di comunicazione.  
  
L'abilitazione della crittografia TLS contribuisce alla sicurezza del traffico di dati in rete tra le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni. ma comporta un rallentamento delle prestazioni.  
  
Negli argomenti di questa sezione viene descritto il supporto della crittografia TLS in [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e vengono illustrate le nuove proprietà di connessione e le modalità disponibili per la configurazione dell'archivio di attendibilità sul lato client.  
  
> [!NOTE]  
> Per convalidare un certificato TLS, è consigliabile usare la proprietà di connessione **hostNameInCertificate**.  

## <a name="in-this-section"></a>Contenuto della sezione  

| Argomento                                                                                                        | Descrizione                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Informazioni sul supporto della crittografia](../../connect/jdbc/understanding-ssl-support.md)                                 | Viene descritto il supporto della crittografia TLS in [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].                                              |
| [Connessione tramite la crittografia](../../connect/jdbc/connecting-with-ssl-encryption.md)                       | Viene descritto come connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando le nuove proprietà di connessione specifiche di TLS. |
| [Configurazione del client per la crittografia](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md) | Viene descritto come configurare l'archivio di attendibilità predefinito sul lato client e come importare un certificato privato nell'archivio di attendibilità del computer client.   |
  
## <a name="see-also"></a>Vedere anche

[Protezione delle applicazioni del driver JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
