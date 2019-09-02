---
title: Schermata 2 della creazione guidata origine dati (driver ODBC per SQL Server) | Microsoft Docs
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
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152572"
---
# <a name="data-source-wizard-screen-2"></a>Creazione guidata origine dati - Schermata 2

Specificare il metodo di autenticazione e configurare le voci del client avanzato di Microsoft SQL Server, nonché l'account di accesso e la password usati dal driver ODBC per SQL Server per connettersi a SQL Server durante la configurazione dell'origine dati.

## <a name="options"></a>Opzioni

### <a name="with-integrated-windows-authentication"></a>Autenticazione Windows integrata

Specifica che il driver richiede una connessione protetta (o trusted) a una SQL Server. Se si seleziona questa opzione, in SQL Server verrà utilizzata la sicurezza degli accessi integrata per stabilire connessioni con questa origine dati, indipendentemente dalla modalità di sicurezza degli accessi corrente del server. Qualsiasi password o ID di accesso specificato viene ignorato. L'amministratore di sistema SQL Server deve avere associato l'account di accesso di Windows a un ID di accesso SQL Server, ad esempio utilizzando SQL Server Management Studio.

È inoltre possibile specificare un nome SPN per il server.

### <a name="with-active-directory-integrated-authentication"></a>Con autenticazione integrata di Active Directory

Specifica che il driver esegue l'autenticazione SQL Server utilizzando Azure Active Directory. Se si seleziona questa opzione, SQL Server usa la sicurezza degli accessi integrata di Azure Active Directory per stabilire una connessione tramite questa origine dati, indipendentemente dalla modalità di protezione degli accessi corrente nel server.

### <a name="with-sql-server-authentication"></a>Autenticazione di SQL Server

Specifica che il driver esegue l'autenticazione per SQL Server utilizzando un ID di accesso e una password.

### <a name="with-active-directory-password-authentication"></a>Con autenticazione della password di Active Directory

Specifica che il driver esegue l'autenticazione SQL Server utilizzando un ID di accesso Azure Active Directory e una password.

### <a name="with-active-directory-interactive-authentication"></a>Con autenticazione interattiva di Active Directory

Specifica che il driver esegue l'autenticazione per SQL Server utilizzando Azure Active Directory modalità interattiva fornendo l'ID di accesso. Verrà attivata la finestra di dialogo di richiesta di autenticazione di Azure.

### <a name="login-id"></a>ID accesso

Specifica l'ID di accesso utilizzato dal driver per la connessione a SQL Server se **con l'autenticazione SQL Server utilizzando un ID di accesso e una password immessi dall'utente** o **con Active Directory l'autenticazione della password utilizzando un ID di accesso e una password immessi dall'utente** oppure **con Active Directory l'autenticazione interattiva utilizzando un ID di accesso immesso dall'utente** è selezionata. Si applica solo alla connessione effettuata per determinare le impostazioni predefinite del server. Non si applica invece alle connessioni successive effettuate utilizzando l'origine dati dopo la relativa creazione.

### <a name="password"></a>Password

Specifica la password utilizzata dal driver per la connessione a SQL Server se **con l'autenticazione SQL Server utilizzando un ID di accesso e una password immessi dall'utente** o **con Active Directory l'autenticazione della password utilizzando un ID di accesso e una password immessi dall'utente** è selezionata. Si applica solo alla connessione effettuata per determinare le impostazioni predefinite del server. Non si applica invece alle connessioni successive effettuate utilizzando la nuova origine dati.

Entrambe le **caselle ID di accesso** e **password** sono disabilitate se è selezionata l'opzione **con autenticazione integrata di Windows** o **con Active Directory autenticazione integrata** .

### <a name="next"></a>Avanti

Consente di passare alla schermata successiva della procedura guidata.

### <a name="back"></a>Indietro

Torna alla schermata precedente della procedura guidata.

## <a name="next-steps"></a>Passaggi successivi

[Creazione guidata origine dati - Schermata 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[Creazione guidata origine dati - Schermata 3](../../../connect/odbc/windows/dsn-wizard-3.md)

