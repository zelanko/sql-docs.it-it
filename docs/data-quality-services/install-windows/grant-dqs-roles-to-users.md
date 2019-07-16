---
title: Concedere ruoli DQS agli utenti | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: afb445b5-bdbe-4bfe-844f-344766cdc2b2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ab6554acd249e119c054754f5b6b6f5196071322
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935211"
---
# <a name="grant-dqs-roles-to-users"></a>Concedere ruoli DQS agli utenti

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento si descrive come creare account di accesso SQL in un'entità di Windows e come assegnare i ruoli [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) nel database DQS_MAIN.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   È necessario aver completato l'installazione di [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] tramite l'esecuzione del file DQSInstaller.exe. Per altre informazioni, vedere [Eseguire DQSInstaller.exe per completare l'installazione del server DQS](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
-   L'account utente di Windows deve essere un membro del ruolo predefinito del server appropriato, ad esempio securityadmin, serveradmin o sysadmin, per creare account di accesso SQL e assegnare loro ruoli DQS.  
  
### <a name="to-create-sql-login-and-grant-dqs-roles"></a>Per creare account di accesso SQL e concedere ruoli DQS  
  
1.  Avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere l'istanza di SQL Server, quindi espandere **Sicurezza**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Sicurezza** scegliere **Nuovo**, quindi selezionare **Account di accesso**.  
  
4.  Nella casella **Nome account di accesso** della finestra di dialogo **Account di accesso - Nuovo** specificare il nome di un utente di Windows, il tipo di autenticazione come **Autenticazione di Windows**e fare clic su **Cerca** per convalidare l'utente.  
  
5.  Al termine della convalida dell'utente, nel riquadro sinistro fare clic su **Mapping utenti** .  
  
6.  Nel riquadro destro selezionare la casella di controllo nella colonna **Mappa** per il database **DQS_MAIN** e quindi selezionare la casella di controllo **dqs_administrator**, **dqs_kb_editor** o **dqs_kb_operator** nel riquadro **Appartenenza a ruoli del database per: DQS_MAIN**, a seconda del livello di accesso necessario per l'utente. Per informazioni su questi tre ruoli DQS, vedere [DQS Sicurezza](../../data-quality-services/dqs-security.md).  
  
7.  Nella finestra di dialogo **Account di accesso - Nuovo** fare clic su **OK** per applicare le modifiche.  
  
    > [!NOTE]  
    >  Se si concede il ruolo **dqs_administrator** a un utente, applicare le modifiche, quindi verificare di nuovo le autorizzazioni utente. Risulteranno selezionate anche le altre due caselle di controllo dei ruoli DQS, cioè**dq_kb_editor** e **dqs_kb_operator**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Provare ad accedere a [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] utilizzando l'account utente di Windows per cui è stato appena creato un account di accesso SQL e a cui è stato concesso un ruolo DQS.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Creazione di un account di accesso](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  
