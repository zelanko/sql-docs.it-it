---
title: Creare un amministratore di dominio
description: Per alcune operazioni è necessario disporre dei privilegi di amministratore di dominio di sistema di Analytics. Viene illustrato come creare altri amministratori di dominio Appliance.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1a0d50e485f0e8f48de11b2e5a3c27c9f9be047e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401237"
---
# <a name="create-an-aps-domain-administrator"></a>Creare un amministratore di dominio APS
Per alcune operazioni è necessario disporre dei privilegi di amministratore di dominio di sistema di Analytics. Viene illustrato come creare altri amministratori di dominio Appliance.  
  
## <a name="create-a-domain-administrator"></a>Creazione di un amministratore di dominio  
Per disporre di autorizzazioni sufficienti per la configurazione di tutti i nodi APS, l'utente che`dwconfig.exe`esegue il Configuration Manager di **APS** () deve essere un membro del gruppo **Domain Admins** . Per avviare e arrestare i servizi APS, l'utente deve essere membro del gruppo **PdwControlNodeAccess** .  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Per aggiungere un utente al gruppo Domain Admins  
  
1.  Accedere al nodo Active AD **(_Appliance\_Domain_-ad01** o ** _Appliance\_Domain_-ad02**) usando un account di amministratore di dominio del dispositivo esistente.  
  
2.  Dal menu Start fare clic su **Esegui**. Nella casella **Apri** Digitare **DSA. msc**. Fare clic su **OK**.  
  
3.  Nel programma **Active Directory utenti e computer** , fare clic con il pulsante destro del mouse su **utenti**, scegliere **nuovo**, quindi fare clic su **utente**.  
  
4.  Nella finestra di dialogo **nuovo oggetto-utente** , completare la descrizione del nuovo utente, quindi fare clic su **Avanti**.  
  
    Completare la finestra di dialogo password e quindi fare clic su **Avanti**.  
  
    > [!WARNING]  
    > SQL Server PDW non supporta il simbolo di dollaro ($) nelle password di amministratore di dominio o di amministratore locale. Una password contenente un segno di dollaro sarà valida ed utilizzabile, ma può bloccare le attività di aggiornamento e manutenzione  
  
    Confermare la descrizione del nuovo utente, quindi fare clic su **fine**.  
  
5.  Nell'elenco di utenti, fare doppio clic sul nuovo utente per aprire la finestra di dialogo Proprietà utente.  
  
6.  Nella scheda **Membro di** fare clic su **Aggiungi**.  
  
    Digitare **Domain Admins; PdwControlNodeAccess** , quindi fare clic su **Controlla nomi**. Fare clic su **OK**.  
  
    Il nuovo utente verrà aggiunto al gruppo **Domain Admins** e al gruppo **PdwControlNodeAccess** . Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
[Avviare la piattaforma Configuration Manager &#40;Analytics System&#41;](launch-the-configuration-manager.md)  
  
