---
title: Autenticazione di Active Directory per SQL Server in Linux
titleSuffix: SQL Server
description: Questo articolo offre una panoramica dell'autenticazione di Active Directory per SQL Server in Linux.
author: rothja
ms.date: 04/01/2019
ms.author: jroth
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 906dd961bcfbb7ea6d8868fdf6eb51cc7bc814aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713601"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Autenticazione di Active Directory per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo offre una panoramica dell'autenticazione di Active Directory (AD) per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux. L'autenticazione di Active Directory è detta anche autenticazione integrata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

## <a name="ad-authentication-overview"></a>Panoramica dell'autenticazione AD

L'autenticazione di AD consente ai client aggiunti a un dominio in Windows o Linux per l'autenticazione a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando le credenziali di dominio e il protocollo Kerberos.

L'autenticazione AD offre i vantaggi seguenti su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticazione:

- Gli utenti di eseguire l'autenticazione tramite single sign-on, senza che venga richiesta una password.   
- Tramite la creazione di account di accesso per gruppi di Active Directory, è possibile gestire l'accesso e autorizzazioni in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite l'appartenenza a gruppi di Active Directory.  
- Ogni utente dispone di una singola identità dell'organizzazione, quindi non è necessario tenere traccia di quali [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gli account di accesso corrispondono alle quali gli utenti.   
- Active Directory consente di applicare i criteri password centralizzati all'interno dell'organizzazione.   

## <a name="configuration-steps"></a>Passaggi di configurazione

Per usare l'autenticazione di Active Directory, è necessario disporre di un Controller di dominio Active Directory (Windows) nella rete.

Nell'esercitazione, vengono forniti i dettagli per informazioni su come configurare l'autenticazione AD [esercitazione: Usare l'autenticazione di Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md). Nell'elenco seguente offre un riepilogo con un collegamento a ogni sezione nell'esercitazione:

1. [Aggiungere un host di SQL Server a un dominio di Active Directory](sql-server-linux-active-directory-join-domain.md).
1. [Creare un utente di AD per SQL Server e impostare ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser).
1. [Configurare keytab il servizio SQL Server](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Proteggere il file keytab](sql-server-linux-active-directory-authentication.md#securekeytab).
1. [Configurare SQL Server per usare il file keytab per l'autenticazione Kerberos](sql-server-linux-active-directory-authentication.md#keytabkerberos).
1. [Creare gli account di accesso di SQL Server basata su Active Directory in Transact-SQL](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [Connettersi a SQL Server Usa l'autenticazione AD](sql-server-linux-active-directory-authentication.md#connect).

## <a name="known-issues"></a>Problemi noti

- A questo punto, l'unico metodo di autenticazione supportato per l'endpoint del mirroring è certificato. Metodo di autenticazione di WINDOWS verrà abilitato nelle versioni future.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come implementare l'autenticazione di Active Directory per SQL Server in Linux, vedere [esercitazione: Usare l'autenticazione di Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md).
