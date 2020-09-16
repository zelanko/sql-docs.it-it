---
title: Proprietà - Protocolli per MSSQLSERVER (scheda Certificato)
description: Selezionare un certificato per SQL Server o visualizzare le proprietà del certificato usando la scheda Certificato della finestra di dialogo Proprietà - Protocolli per MSSQLSERVER.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
f1_keywords:
- sql13.swb.computermgr.cert.general.f1
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 776addd6-25f3-4875-9a71-064035787090
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 89373613f18b760ab3aa55af1e9ede889c06aa5c
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901215"
---
# <a name="protocols-for-mssqlserver-properties-certificate-tab"></a>Proprietà - Protocolli per MSSQLSERVER (scheda Certificato)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Usare la scheda **Certificato** della finestra di dialogo **Proprietà - Protocolli per MSSQLSERVER** per selezionare un certificato per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o visualizzare le proprietà di un certificato. Tutti i campi sono vuoti se non è selezionato alcun certificato.  
  
 I certificati per gli utenti vengono archiviati nel computer locale. Per caricare un certificato da utilizzare con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario eseguire Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con lo stesso account utente del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="page-header"></a>Intestazione di pagina  
 **Visualizza**  
 Consente di accedere a ulteriori dettagli sul certificato. Non è disponibile se non è selezionato alcun certificato nella casella **Certificato** . Per ulteriori informazioni sui dettagli dei certificati, vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Cancella**  
 Rimuove la selezione dalla casella **Certificato** .  
  
 **Certificate**  
 Nome del certificato come stabilito dal provider di sicurezza. Selezionare un certificato per visualizzarne i dettagli nella griglia delle proprietà.  
  
## <a name="options"></a>Opzioni  
 Data scadenza  
 Data finale del periodo in cui il certificato è valido.  
  
 Nome descrittivo  
 Nome descrittivo o comune dell'individuo o dell'autorità di certificazione a cui viene rilasciato il certificato.  
  
 Rilasciato da  
 Informazioni sull'autorità di certificazione che ha rilasciato il certificato.  
  
 Rilasciato a  
 Informazioni sul destinatario del certificato.  
  
  
