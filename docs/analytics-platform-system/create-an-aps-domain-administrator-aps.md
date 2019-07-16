---
title: Creare un amministratore di dominio - sistema di piattaforma Analitica | Microsoft Docs
description: Alcune operazioni richiedono privilegi di amministratore di sistema di piattaforma Analitica dominio. Questo spiega come creare gli amministratori di dominio appliance aggiuntivi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 51ed729cda33b5d68a4d115c71f712e2b81d1a65
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961099"
---
# <a name="create-an-aps-domain-administrator"></a>Creare un amministratore di dominio APS
Alcune operazioni richiedono privilegi di amministratore di sistema di piattaforma Analitica dominio. Questo spiega come creare gli amministratori di dominio appliance aggiuntivi.  
  
## <a name="create-a-domain-administrator"></a>Creare un amministratore di dominio  
Disporre delle autorizzazioni sufficienti per configurare tutti i nodi di punti di accesso, l'utente che esegue la **APS Configuration Manager** (`dwconfig.exe`) deve essere un membro del **Domain Admins** gruppo. Per avviare e arrestare i servizi di piattaforma di strumenti analitici, l'utente deve essere un membro del **PdwControlNodeAccess** gruppo.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Per aggiungere un utente al gruppo Domain Admins  
  
1.  Accedere al nodo AD attivo **(_appliance\_domain_-AD01** oppure  **_appliance\_dominio_-AD02**) usando un account di amministratore di dominio appliance esistente.  
  
2.  Nel menu Start fare clic su **Esegui**. Nel **aperto** , digitare **DSA. msc**. Fare clic su **OK**.  
  
3.  Nel **Active Directory Users and Computers** programma, fare doppio clic su **utenti**, scegliere **New**e quindi fare clic su **utente**.  
  
4.  Nel **nuovo oggetto - utente** completare la descrizione del nuovo utente nella finestra di dialogo e quindi fare clic su **successivo**.  
  
    Completare la finestra di dialogo password e quindi fare clic su **successivo**.  
  
    > [!WARNING]  
    > SQL Server PDW non supporta il carattere di segno di dollaro ($) nell'amministratore di dominio o le password di amministratore locale. Una password contenente un segno di dollaro sarà valida e utilizzabile, ma possono bloccare le attività di aggiornamento e manutenzione  
  
    Confermare la nuova descrizione utente e quindi fare clic su **fine**.  
  
5.  Nell'elenco di utenti, fare doppio clic sul nuovo utente per aprire la finestra di dialogo delle proprietà utente.  
  
6.  Nel **membro di** scheda, fare clic su **Add**.  
  
    Tipo **Domain Admins; PdwControlNodeAccess** e quindi fare clic su **Controlla nomi**. Fare clic su **OK**.  
  
    Verrà aggiunto il nuovo utente per il **Domain Admins** gruppo e il **PdwControlNodeAccess** gruppo. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
[Avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md)  
  
