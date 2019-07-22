---
title: Uso della crittografia SSL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c9cd99d8fd8a54c96a9301ac3a050b54614c17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003963"
---
# <a name="using-ssl-encryption"></a>Utilizzo della crittografia SSL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La crittografia SSL (Secure Sockets Layer) consente la trasmissione di dati crittografati attraverso la rete tra un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e un'applicazione client.  
  
SSL (Secure Sockets Layer) è un protocollo che consente di stabilire un canale di comunicazione sicuro per impedire l'intercettazione di informazioni critiche o riservate attraverso la rete e altre comunicazioni Internet. SSL consente al client e al server di autenticare l'identità reciproca. Dopo che i partecipanti sono stati autenticati, SSL fornisce connessioni crittografate tra di essi per una trasmissione sicura dei messaggi.  
  
In [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è disponibile un'infrastruttura per abilitare e disabilitare la crittografia in una particolare connessione in base alle proprietà di connessione specificate dall'utente e alle impostazioni server e client. L'utente può specificare il percorso e la password dell'archivio certificati, un nome host da utilizzare per convalidare il certificato e quando crittografare il canale di comunicazione.  
  
L'abilitazione della crittografia SSL contribuisce alla sicurezza del traffico di dati in rete tra le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni, ma comporta un rallentamento delle prestazioni.  
  
Negli argomenti di questa sezione viene descritto il supporto della crittografia SSL in [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e vengono illustrate le nuove proprietà di connessione e le modalità disponibili per la configurazione dell'archivio di attendibilità sul lato client.  
  
> [!NOTE]  
> È consigliabile utilizzare la proprietà di connessione **hostNameInCertificate** per convalidare un certificato SSL.  

## <a name="in-this-section"></a>Contenuto della sezione  

| Argomento                                                                                                        | Descrizione                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Informazioni sul supporto SSL](../../connect/jdbc/understanding-ssl-support.md)                                 | Viene descritto il supporto della crittografia SSL in [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].                                              |
| [Connessione tramite la crittografia SSL](../../connect/jdbc/connecting-with-ssl-encryption.md)                       | Viene descritto come connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando le nuove proprietà di connessione specifiche di SSL. |
| [Configurazione del client per la crittografia SSL](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md) | Viene descritto come configurare l'archivio di attendibilità predefinito sul lato client e come importare un certificato privato nell'archivio di attendibilità del computer client.   |
  
## <a name="see-also"></a>Vedere anche

[Protezione delle applicazioni del driver JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
