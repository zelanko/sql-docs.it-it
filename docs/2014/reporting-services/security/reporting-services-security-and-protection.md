---
title: Sicurezza e protezione di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0f8c7a4186c5236260fb27d8de107ce8c97bd363
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101966"
---
# <a name="reporting-services-security-and-protection"></a>Sicurezza e protezione di Reporting Services
  È possibile usare le informazioni contenute in questa sezione per ottenere altre informazioni sulle caratteristiche di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Questa sezione descrive inoltre i modelli di autorizzazione e i provider di autenticazione supportati in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="extended-protection-for-authentication"></a>Protezione estesa per l'autenticazione  
 A partire da [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], è disponibile il supporto per la protezione estesa per l'autenticazione. La caratteristica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'uso del binding di canale e dell'associazione al servizio per migliorare la protezione dell'autenticazione. Le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere utilizzate con un sistema operativo che supporti la protezione estesa. Per altre informazioni, vedere [Protezione estesa per l'autenticazione con Reporting Services](extended-protection-for-authentication-with-reporting-services.md).  
  
## <a name="authentication-and-authorization"></a>Autenticazione e autorizzazione  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] offre diversi tipi di autenticazione per utenti e applicazioni client da autenticare con il server di report. L'utilizzo del tipo di autenticazione corretto per il server di report consente all'organizzazione di ottenere il livello di sicurezza appropriato richiesto dall'organizzazione. Per altre informazioni, vedere [Autenticazione con il server di report](authentication-with-the-report-server.md).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa inoltre ruoli e autorizzazioni per controllare l'accesso dell'utente al contenuto nel catalogo del server di report (in altre parole chi può accedere a che cosa e in che modo può accedervi). Per altre informazioni, vedere [Ruoli e autorizzazioni &#40;Reporting Services&#41;](roles-and-permissions-reporting-services.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizioni delle attività|Collegamenti|  
|-----------------------|-----------|  
|Configurare Secure Socket Layer (SSL) per proteggere le connessioni client al server di report.|[Configurare connessioni SSL in un server di report in modalità nativa](configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
