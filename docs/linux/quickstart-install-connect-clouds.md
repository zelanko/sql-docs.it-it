---
title: Introduzione a SQL Server (on Linux) nel Cloud
titleSuffix: SQL Server
description: Questa Guida introduttiva illustra come eseguire SQL Server in Linux nel cloud di propria scelta.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/25/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 28d95ab15da9d5eccce7c8b9fc4be4741b12305a
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775584"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>Avvio rapido: Eseguire SQL Server nel cloud
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In questa Guida introduttiva si installerà SQL Server su Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) o Ubuntu nel cloud di propria scelta. Passare a [effettuare il provisioning di una macchina virtuale Linux di SQL Server nel portale di Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json) per eseguire SQL Server su Linux in Azure.

> [!NOTE]
> Se si sceglie di eseguire un'edizione a pagamento di SQL Server, quindi è necessario utilizzare la propria licenza (BYOL).

## <a name="amazon-web-services"></a>Amazon Web Services
1.  Creare un AMI Linux con almeno 2 GB di memoria da marketplace 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Connettersi alla finestra di Rispostarli con ssh
1.  Attenersi alla Guida introduttiva per la distribuzione Linux che scelta: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configurare connessioni remote: 
    * Aprire il [console di Amazon EC2]( https://console.aws.amazon.com/ec2/)
    * Nel riquadro di spostamento, scegliere **gruppi di sicurezza**. 
    * Scegliere **in ingresso, modifica, aggiungere una regola**
    * Aggiungere una regola in ingresso per consentire il traffico sulla porta su cui SQL Server è in ascolto (porta TCP predefinita 1433)

    
## <a name="digital-ocean"></a>Digital Ocean
1. Accedi per il [Pannello di controllo](https://cloud.digitalocean.com/login) e fare clic su Crea un droplet
1. Scegliere un droplet Ubuntu 16.04 con almeno 2 GB di memoria
1. Connettersi al droplet con ssh
1. Seguire il [avvio rapido di Ubuntu](quickstart-install-connect-ubuntu.md)
1. Configurare connessioni remote:
    * Nella parte superiore del Pannello di controllo, seguire le **Networking** collegamento e quindi selezionare **firewall**
    * Aggiungere una regola in ingresso per consentire il traffico sulla porta su cui SQL Server è in ascolto (porta TCP predefinita 1433)
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  Creare un'immagine Linux con almeno 2 GB di memoria di avvio di Cloud 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Connettersi all'immagine con ssh
1.  Attenersi alla Guida introduttiva per la distribuzione Linux che scelta: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configurare connessioni remote: 
    * Andare alla [regole del Firewall](https://console.cloud.google.com/networking/firewalls)
    * Aggiungere una regola in ingresso per consentire il traffico sulla porta su cui è in ascolto SQL Server (default tcp: 1433)
