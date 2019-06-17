---
title: Origine di dati guidata schermata 2 (Driver ODBC per SQL Server) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 2c41b9215979488cbec9ebda89d98bb0f464d11a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797813"
---
# <a name="data-source-wizard-screen-2"></a>Creazione guidata origine dati - Schermata 2

Specificare il metodo di autenticazione e configurare le voci del client avanzato di Microsoft SQL Server, nonché l'account di accesso e la password usati dal driver ODBC per SQL Server per connettersi a SQL Server durante la configurazione dell'origine dati.

## <a name="options"></a>Opzioni

### <a name="with-integrated-windows-authentication"></a>Autenticazione Windows integrata

Specifica che il driver richiede una connessione protetta (o trusted) a un Server SQL. Se si seleziona questa opzione, in SQL Server verrà utilizzata la sicurezza degli accessi integrata per stabilire connessioni con questa origine dati, indipendentemente dalla modalità di sicurezza degli accessi corrente del server. Qualsiasi password o ID di accesso specificato viene ignorato. L'amministratore di sistema di SQL Server deve avere associato l'account di accesso di Windows con un ID di accesso di SQL Server (ad esempio, usando SQL Server Management Studio).

È inoltre possibile specificare un nome SPN per il server.

### <a name="with-active-directory-integrated-authentication"></a>Con autenticazione integrata di Active Directory

Specifica che il driver di eseguire l'autenticazione a SQL Server usando Azure Active Directory. Se si seleziona questa opzione, SQL Server usa la sicurezza degli accessi integrata di Azure Active Directory per stabilire una connessione tramite questa origine dati, indipendentemente dalla modalità di protezione degli accessi corrente nel server.

### <a name="with-sql-server-authentication"></a>Autenticazione di SQL Server

Specifica che il driver di eseguire l'autenticazione in SQL Server usando un ID di accesso e una password.

### <a name="with-active-directory-password-authentication"></a>Con autenticazione della password di Active Directory

Specifica che il driver di eseguire l'autenticazione in SQL Server usando un ID di accesso di Azure Active Directory e una password.

### <a name="with-active-directory-interactive-authentication"></a>Con autenticazione interattiva di Active Directory

Specifica che il driver di eseguire l'autenticazione a SQL Server utilizzando la modalità interattiva Azure Active Directory, fornendo l'ID di accesso. Verrà attivata la finestra di dialogo dei messaggi di richiesta di autenticazione di Windows Azure.

### <a name="login-id"></a>ID accesso

Specifica l'ID di accesso nel driver vengono utilizzate quando ci si connette a SQL Server se **con autenticazione di SQL Server usando un ID di accesso e una password immessi dall'utente** o **l'autenticazione con Password di Active Directory usando un ID di accesso e la password immessa dall'utente** oppure **autenticazione con Active Directory Interactive usando un ID di accesso immessi dall'utente** sia selezionata. Si applica solo alla connessione effettuata per determinare le impostazioni predefinite del server. Non si applica invece alle connessioni successive effettuate utilizzando l'origine dati dopo la relativa creazione.

### <a name="password"></a>Password

Specifica la password nel driver vengono utilizzate quando ci si connette a SQL Server se **con autenticazione di SQL Server usando un ID di accesso e una password immessi dall'utente** o **l'autenticazione con Password di Active Directory usando un ID di accesso e la password immessa dall'utente** sia selezionata. Si applica solo alla connessione effettuata per determinare le impostazioni predefinite del server. Non si applica invece alle connessioni successive effettuate utilizzando la nuova origine dati.

Entrambi i **ID di accesso** e **Password** finestre sono disabilitate se **l'autenticazione con Windows integrata** o **con integrata di Active Directory autenticazione** sia selezionata.

### <a name="next"></a>Avanti

Procede alla schermata successiva della procedura guidata.

### <a name="back"></a>Indietro

Tornare alla schermata precedente della procedura guidata.

## <a name="next-steps"></a>Passaggi successivi

[Creazione guidata origine dati - Schermata 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[Creazione guidata origine dati - Schermata 3](../../../connect/odbc/windows/dsn-wizard-3.md)

