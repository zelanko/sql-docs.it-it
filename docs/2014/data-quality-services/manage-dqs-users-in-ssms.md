---
title: Gestione di utenti DQS in SSMS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d8d7e0c31b1e022445006598f791716d765b98c9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027982"
---
# <a name="manage-dqs-users-in-ssms"></a>Gestione di utenti DQS in SSMS
  In questo argomento viene descritto come creare utenti aggiuntivi nell'istanza di SQL Server utilizzando SQL Server Management Studio e come assegnare loro ruoli [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) nel database DQS_MAIN.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 L'account utente di Windows deve essere un membro del ruolo predefinito del server appropriato, ad esempio securityadmin, serveradmin o sysadmin, per creare account di accesso SQL e assegnare a questi i ruoli DQS appropriati.  
  
##  <a name="GrantRoles"></a> Creare un account di accesso SQL e concessione del ruolo DQS  
  
1.  Avviare Microsoft SQL Server Management Studio.  
  
2.  In Microsoft SQL Server Management Studio espandere l'istanza di SQL Server, quindi espandere **Sicurezza**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Sicurezza** scegliere **Nuovo**, quindi selezionare **Account di accesso**.  
  
4.  Nella casella **Nome account di accesso** della finestra di dialogo **Account di accesso - Nuovo** specificare il nome di un utente di Windows, il tipo di autenticazione come **Autenticazione di Windows**e fare clic su **Cerca** per convalidare l'utente.  
  
    > [!NOTE]  
    >  DQS supporta sola l'autenticazione di Windows; l'autenticazione di SQL Server non è supportata.  
  
5.  Al termine della convalida dell'utente, nel riquadro sinistro fare clic su **Mapping utenti** .  
  
6.  Nel riquadro di destra, selezionare la casella di controllo sotto le **mappa** colonna per il **DQS_MAIN** del database e quindi selezionare il **dqs_administrator**, **dqs_kb_editor** , o **dqs_kb_operator** casella di controllo di **Database l'appartenenza al ruolo per: Database DQS_MAIN** riquadro, a seconda del livello di accesso necessario per l'utente.  
  
7.  Nella finestra di dialogo **Account di accesso - Nuovo** fare clic su **OK** per applicare le modifiche.  
  
    > [!NOTE]  
    >  Se si concede il ruolo **dqs_administrator** a un utente, applicare le modifiche, quindi verificare di nuovo le autorizzazioni utente. Risulteranno selezionate anche le altre due caselle di controllo dei ruoli DQS, cioè**dq_kb_editor** e **dqs_kb_operator**.  
  
  
