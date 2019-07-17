---
title: Sicurezza dell'integrazione CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
author: rothja
ms.author: jroth
ms.openlocfilehash: 7cfcc3f4d65901da34152a6fce21b436750c15fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118506"
---
# <a name="clr-integration-security"></a>Sicurezza per l'integrazione con CLR

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Il modello di sicurezza dell'integrazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con CLR (Common Language Runtime) di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] gestisce e protegge l'accesso tra i diversi tipi di oggetti CLR e non CLR in esecuzione in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Tali oggetti possono essere chiamati dall'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] o da un altro oggetto CLR in esecuzione nel server. Le chiamate tra gli oggetti vengono definite collegamenti. I tipi di controllo della sicurezza eseguiti su questi oggetti dipendono dai tipi di collegamento utilizzati.  
  
 Il modello di sicurezza dell'integrazione con CLR presenta gli obiettivi seguenti:  
  
-   Per impostazione predefinita, l'esecuzione del codice utente gestito in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non deve compromettere l'integrità e la stabilità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. L'esecuzione di operazioni che potenzialmente compromettono l'affidabilità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve essere protetta grazie alle autorizzazioni di livello elevato appropriate.  
  
-   Non è consigliabile concedere al codice utente gestito l'accesso non autorizzato ai dati dell'utente o ad altro codice dell'utente nel database. Il codice definito dall'utente deve essere eseguito nel contesto di sicurezza della sessione utente che lo ha richiamato e con i privilegi corretti per il contesto di sicurezza in questione.  
  
-   È necessario effettuare controlli per limitare al codice utente l'accesso alle risorse esterne al server consentendone l'utilizzo esclusivamente per il calcolo e l'accesso ai dati locali.  
  
-   Non è consigliabile concedere al codice definito dall'utente l'accesso non autorizzato alle risorse di sistema solo perché è in esecuzione nel processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] integra ora il modello di sicurezza basato sull'utente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con il modello di sicurezza basato sull'accesso al codice di CLR. Alcuni dei vantaggi di questo approccio combinato alla sicurezza vengono esaminati nella presente sezione.  
  
 Nella tabella seguente vengono elencati gli argomenti disponibili in questa sezione.  
  
 [Sicurezza dall'accesso di codice dell'integrazione con CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
 Viene illustrato il modello di sicurezza da accesso di codice (CAS, Code Access Security) per il codice gestito.  
  
 [Attributi di protezione host e programmazione dell'integrazione con CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 Vengono fornite informazioni sui valori di attributi di protezione host che non sono consentiti negli assembly SAFE e EXTERNAL_ACCESS.  
  
 [Collegamenti nella sicurezza per l'integrazione con CLR](https://msdn.microsoft.com/library/168efd01-d12e-4bdf-a1b3-0b5c76474eaf)  
 Viene illustrato come parti del codice utente possano chiamarsi reciprocamente in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Rappresentazione e sicurezza per l'integrazione con CLR](https://msdn.microsoft.com/library/1495a7af-2248-4cee-afdb-9269fb3a7774)  
 Viene illustrato con il codice gestito acceda a risorse esterne utilizzando la rappresentazione.  
  
 [Accettazione di chiamanti parzialmente attendibili](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
 Vengono illustrati i problemi che si verificano quando un metodo gestito richiama un metodo di una classe contenuta in un altro assembly.  
  
 [Domini applicazione e sicurezza per l'integrazione con CLR](/sql/database-engine/dev-guide/allowing-partially-trusted-callers?view=sql-server-2014)  
 Viene descritto come caricare gli assembly nei domini applicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli assembly dell'integrazione con CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
  
  
