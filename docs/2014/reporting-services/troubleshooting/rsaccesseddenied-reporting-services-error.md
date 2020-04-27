---
title: rsAccessedDenied - Errore di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bfaad65431cc71c8fa7a6ec5ba24e13fa7692e99
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099227"
---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied - Errore di Reporting Services
  L'errore di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**rsAccessedDenied** si verifica quando un utente non dispone dell'autorizzazione per eseguire un'azione, ad esempio non dispone di un'assegnazione di ruolo che consenta di aprire un report o non ha aperto il browser con le autorizzazioni necessarie.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa &#124; modalità SharePoint|  
  
-   Se l'errore si è verificato durante l'accesso diretto al server di report tramite URL, verrà eseguito il mapping tra l'eccezione e un errore HTTP 401.  
  
-   Se si è verificato durante l'utilizzo di Gestione report o un altro strumento, l'errore verrà visualizzato in un'apposita pagina.  
  
-   Se si è verificato durante un'operazione, una sottoscrizione o un recapito pianificato, l'errore verrà indicato solo nel file di log del server di report.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|**Nome prodotto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**ID evento**|rsAccessedDenied|  
|**Origine evento**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|**Componente**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**Testo del messaggio**|Le autorizzazioni concesse all'utente 'mydomain\myAccount' non sono sufficienti per eseguire questa operazione. (rsAccessDenied) (ReportingServicesLibrary)|  
  
## <a name="user-action"></a>Azione dell'utente  
 Le autorizzazioni che consentono di accedere al contenuto e alle operazioni del server di report vengono concesse tramite assegnazioni di ruolo. In una nuova installazione solo gli amministratori locali possono accedere a un server di report. Per concedere l'accesso ad altri utenti, l'amministratore locale deve creare un'assegnazione di ruolo che specifica un account di gruppo o un account utente di dominio, uno o più ruoli che definiscono le attività eseguibili dall'utente, nonché un ambito, ovvero in genere la cartella Home o il nodo radice della gerarchia di cartelle del server di report. Per creare le assegnazioni di ruolo, è possibile usare Gestione report. Per altre informazioni, cercare "assegnazioni di ruolo" nella documentazione online di SQL Server.  
  
 Questo errore viene causato anche dall'amministratore locale del server di report. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Assegnazioni di ruolo](../security/role-assignments.md)   
 [Concessione di autorizzazioni in un server di report in modalità nativa](../security/granting-permissions-on-a-native-mode-report-server.md)   
 [Ruoli e autorizzazioni &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)  
  
  
