---
title: Schermata 2 di Creazione guidata origine dati (driver ODBC per SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
ms.openlocfilehash: 4ab8be02351a23c78251a99ca707e946ee8944c8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "70152572"
---
# <a name="data-source-wizard-screen-2"></a>Creazione guidata origine dati - Schermata 2

Specificare il metodo di autenticazione e configurare le voci del client avanzato di Microsoft SQL Server, nonché l'account di accesso e la password usati dal driver ODBC per SQL Server per connettersi a SQL Server durante la configurazione dell'origine dati.

## <a name="options"></a>Opzioni

### <a name="with-integrated-windows-authentication"></a>Autenticazione Windows integrata

Indica che il driver richiede una connessione protetta (o trusted) a un SQL Server. Se si seleziona questa opzione, in SQL Server verrà utilizzata la sicurezza degli accessi integrata per stabilire connessioni con questa origine dati, indipendentemente dalla modalità di sicurezza degli accessi corrente del server. Qualsiasi password o ID di accesso specificato viene ignorato. L'amministratore di sistema di SQL Server deve associare l'account di accesso di Windows a un ID di accesso di SQL Server (ad esempio tramite SQL Server Management Studio).

È inoltre possibile specificare un nome SPN per il server.

### <a name="with-active-directory-integrated-authentication"></a>Con autenticazione integrata di Active Directory

Specifica che il driver esegue l'autenticazione SQL Server tramite Azure Active Directory. Se si seleziona questa opzione, SQL Server usa la sicurezza degli accessi integrata di Azure Active Directory per stabilire una connessione tramite questa origine dati, indipendentemente dalla modalità di protezione degli accessi corrente nel server.

### <a name="with-sql-server-authentication"></a>Autenticazione di SQL Server

Specifica che il driver esegue l'autenticazione SQL Server tramite un ID di accesso e una password.

### <a name="with-active-directory-password-authentication"></a>Con autenticazione della password di Active Directory

Specifica che il driver esegue l'autenticazione SQL Server tramite un ID di accesso di Azure Active Directory e una password.

### <a name="with-active-directory-interactive-authentication"></a>Con autenticazione interattiva di Active Directory

Specifica che il driver esegue l'autenticazione SQL Server tramite la modalità interattiva di Azure Active Directory fornendo un ID di accesso. In questo modo verrà attivata la finestra di dialogo di richiesta di autenticazione di Azure.

### <a name="login-id"></a>ID accesso

Specifica l'ID di accesso usato dal driver per la connessione a SQL Server se viene selezionata l'opzione **Autenticazione SQL Server tramite ID e password di accesso immessi dall'utente** o **Con autenticazione della password di Active Directory mediante ID di accesso e password immessi dall'utente** o **Con autenticazione interattiva di Active Directory mediante un ID di accesso immesso dall'utente**. Si applica solo alla connessione effettuata per determinare le impostazioni predefinite del server. Non si applica invece alle connessioni successive effettuate utilizzando l'origine dati dopo la relativa creazione.

### <a name="password"></a>Password

Specifica la password usata dal driver per la connessione a SQL Server se viene selezionata l'opzione **Autenticazione SQL Server tramite ID e password di accesso immessi dall'utente** o **Con autenticazione della password di Active Directory mediante ID di accesso e password immessi dall'utente**. Si applica solo alla connessione effettuata per determinare le impostazioni predefinite del server. Non si applica invece alle connessioni successive effettuate utilizzando la nuova origine dati.

Le caselle **ID di accesso** e **Password** sono entrambe disabilitate se è selezionata l'opzione **Autenticazione Windows integrata** o **Autenticazione integrata di Active Directory**.

### <a name="next"></a>Avanti

Consente di passare alla schermata successiva della procedura guidata.

### <a name="back"></a>Indietro

Consente di tornare alla schermata precedente della procedura guidata.

## <a name="next-steps"></a>Passaggi successivi

[Creazione guidata origine dati - Schermata 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[Creazione guidata origine dati - Schermata 3](../../../connect/odbc/windows/dsn-wizard-3.md)

