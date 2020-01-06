---
title: Autenticazione di Azure Active Directory per SQL Server in Linux
titleSuffix: SQL Server
description: Questo articolo offre una panoramica dell'autenticazione di Active Directory per SQL Server in Linux.
ms.date: 04/01/2019
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 9f2e5632b073f96faf530db56d052d71f4a143f4
ms.sourcegitcommit: f9286d02025ee1e15d0f1c124e951e8891fe3cc2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/23/2019
ms.locfileid: "75329963"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Autenticazione di Azure Active Directory per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo offre una panoramica dell'autenticazione di Active Directory (AD) per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux. L'autenticazione di AD in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è nota anche come autenticazione integrata. 

## <a name="ad-authentication-overview"></a>Panoramica dell'autenticazione di AD

L'autenticazione di AD consente ai client aggiunti a un dominio in Windows o Linux di eseguire l'autenticazione a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando le proprie credenziali di dominio e il protocollo Kerberos.

Rispetto all'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], l'autenticazione di AD presenta i vantaggi seguenti:

- Gli utenti eseguono l'autenticazione tramite Single Sign-On e non devono specificare la password.   
- Creando account di accesso per i gruppi AD, è possibile gestire l'accesso e le autorizzazioni in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite le appartenenze a tali gruppi.  
- Ogni utente ha un'unica identità in tutta l'organizzazione. Non è quindi necessario tenere traccia della corrispondenza tra gli account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e ciascun utente.   
- AD consente di applicare criteri centralizzati per le password in tutta l'organizzazione.   

## <a name="configuration-steps"></a>Passaggi di configurazione

Per usare l'autenticazione di Active Directory, è necessaria la presenza di un controller di dominio di Active Directory (Windows) all'interno della rete.

I dettagli sulla configurazione dell'autenticazione di Active Directory sono disponibili in [Esercitazione: Usare l'autenticazione di Azure Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md). L'elenco seguente offre un riepilogo e un collegamento a ogni sezione dell'esercitazione:

1. [Aggiungere un host di SQL Server a un dominio di Active Directory](sql-server-linux-active-directory-join-domain.md).
1. [Creare un utente di AD per SQL Server e impostare ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser).
1. [Configurare il file keytab del servizio SQL Server](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Proteggere il file keytab](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Configurare SQL Server per l'uso del file keytab per l'autenticazione Kerberos](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Creare account di accesso di SQL Server basati su AD in Transact-SQL](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [Connettersi a SQL Server usando l'autenticazione di Active Directory](sql-server-linux-active-directory-authentication.md#connect).

## <a name="known-issues"></a>Problemi noti

- L'unico metodo di autenticazione attualmente supportato per l'endpoint di mirroring del database è CERTIFICATE. Il metodo di autenticazione WINDOWS verrà abilitato in una versione futura.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come implementare l'autenticazione di Active Directory per SQL Server in Linux, vedere [Esercitazione: Usare l'autenticazione di Azure Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md).
