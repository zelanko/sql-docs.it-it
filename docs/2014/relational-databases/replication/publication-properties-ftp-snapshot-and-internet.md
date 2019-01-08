---
title: Proprietà pubblicazione, Snapshot FTP e Internet | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.internetsynchronization.f1
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 72d53ea0cf2d1abff25b7b97a1fe66cc9d9646b7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52784843"
---
# <a name="publication-properties-ftp-snapshot-and-internet"></a>Proprietà pubblicazione, Snapshot FTP e Internet
  Questa pagina consente di:  
  
-   Impostare le proprietà per il recapito dello snapshot tramite FTP (File Transfer Protocol). Per altre informazioni, vedere [trasferire snapshot tramite FTP](transfer-snapshots-through-ftp.md) documentazione di Windows per altre informazioni.  
  
    > [!NOTE]  
    >  Le modifiche apportate a qualsiasi impostazione relativa al protocollo FTP richiedono la generazione di un nuovo snapshot.  
  
-   Impostare le proprietà per la sincronizzazione Web per la replica di tipo merge in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, in modo da consentire la sincronizzazione delle sottoscrizioni tramite il protocollo HTTPS. Per utilizzare la sincronizzazione Web è necessario configurare un server [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS). Per altre informazioni, vedere [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
## <a name="options"></a>Opzioni  
 **Accedi ai file di snapshot tramite FTP**  
 Selezionare **I Sottoscrittori possono scaricare i file di snapshot utilizzando FTP (File Transfer Protocol)** e specificare **Nome server FTP**, **Numero di porta**, **Percorso dalla cartella radice FTP**, **Account di accesso**e **Password**per consentire ai Sottoscrittori l'utilizzo del protocollo FTP per il recapito di snapshot.  
  
 La selezione di questa opzione consente ai Sottoscrittori di utilizzare il protocollo FTP per recuperare i file di snapshot, senza tuttavia imporne l'obbligo di utilizzo. Se si seleziona questa opzione, l'impostazione predefinita per la Creazione guidata nuova sottoscrizione viene impostata per consentire al Sottoscrittore di recuperare file di snapshot tramite FTP. Per modificare l'impostazione utilizzare la finestra di dialogo **Proprietà sottoscrizione** . Se si consente ai Sottoscrittori l'accesso ai file di snapshot tramite FTP, specificare la cartella FTP come posizione per i file di snapshot nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione** . In tal modo l'agente snapshot aggiornerà automaticamente i file nella cartella FTP quando viene generato un nuovo snapshot. Se la posizione non è impostata sulla cartella FTP, sarà necessario aggiornare i file manualmente ogni volta che vengono generati nuovi snapshot. Per altre informazioni, vedere [Recapitare uno snapshot tramite FTP](publish/deliver-a-snapshot-through-ftp.md).  
  
 **Sincronizzazione Web**  
 Solo per la replica di tipo merge. Selezionare **I Sottoscrittori possono eseguire la sincronizzazione tramite connessione a un server Web**e specificare l'indirizzo di un server Web per consentire ai Sottoscrittori della replica di tipo merge di utilizzare la sincronizzazione Web. È necessario che il server Web usi SSL (Secure Sockets Layer) e che l'indirizzo Web sia completo, ad esempio https://server.domain.com/synchronize. Per altre informazioni, vedere [Configure Web Synchronization](configure-web-synchronization.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
 [Visualizzare e modificare le proprietà delle sottoscrizioni pull](view-and-modify-pull-subscription-properties.md)   
 [Visualizzare e modificare le proprietà delle sottoscrizioni push](view-and-modify-push-subscription-properties.md)   
 [Creare e applicare lo snapshot iniziale](create-and-apply-the-initial-snapshot.md)   
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)  
  
  
